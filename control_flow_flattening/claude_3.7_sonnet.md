<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" class="logo" width="120"/>

# Deobfuscated Assembly Code

After analyzing this x86 assembly code, I can see it's a heavily obfuscated function that performs different calculations based on the remainder when dividing the input parameter by 4.

## Core Functionality

The function takes one parameter (passed in `edi`) and performs one of four different arithmetic operations, depending on the value of `param % 4`. The complex state machine and unnecessary jumps are obfuscation techniques.

Here's the deobfuscated logic in C:

```c
int deobfuscated_function(int param) {
    int result = 0;
    int mod4 = param &amp; 3;  // Equivalent to param % 4
    
    switch (mod4) {
        case 0:
            // At address 0x1c6-0x1da
            result = (param | 0xBAAAAD0BF) * (param ^ 2);
            break;
            
        case 1:
            // At address 0x205-0x219
            result = (param &amp; 0xBAAAAD0BF) * (param + 3);
            break;
            
        case 2:
            // At address 0x244-0x258
            result = (param ^ 0xBAAAAD0BF) * (param | 4);
            break;
            
        case 3:
            // At address 0x267-0x27b
            result = (param + 0xBAAAAD0BF) * (param &amp; 5);
            break;
    }
    
    return result;
}
```


## Explanation

The original assembly code implements a state machine with numerous states and transitions, but the actual functionality is straightforward:

1. It calculates `param % 4` using a bitwise AND with 3
2. Based on this value, it selects one of four arithmetic expressions
3. It calculates the result and returns it

The state machine and complex control flow with multiple comparisons, jumps, and intermediate states are all obfuscation techniques designed to hide this simple logic. Many of the operations and state transitions in the assembly code serve no functional purpose other than to make the code harder to understand.

---

## Revised Analysis \& Correction

After re-examining the assembly, I identified an error in the magic constants and refined the logic:

**Key Fixes:**

1. **Constant Correction:** Changed all `0xBAAAAD0BF` → `0xbaaad0bf` (original assembly uses 32-bit `0BAAAD0BF`)
2. **Signature Update:** Changed return types to `unsigned` due to bitwise operations
```c
unsigned obfuscated_calculation(unsigned param) {
    unsigned result = 0;
    const unsigned magic = 0xbaaad0bf;  // Critical fix here
    switch(param % 4) {
        case 0:
            result = (param | magic) * (param ^ 2);
            break;
        case 1:
            result = (param &amp; magic) * (param + 3);
            break;
        case 2:
            result = (param ^ magic) * (param | 4);
            break;
        case 3:
            result = (param + magic) * (param &amp; 5);
            break;
    }
    return result;
}
```


## Validation Matrix

| Case | Assembly Location | Operation Verification | Constant Check |
| :-- | :-- | :-- | :-- |
| 0 | 0x1c6-0x1da | OR/XOR/IMUL matches | 0xbaaad0bf ✓ |
| 1 | 0x205-0x219 | AND/ADD/IMUL matches | 0xbaaad0bf ✓ |
| 2 | 0x244-0x258 | XOR/OR/IMUL matches | 0xbaaad0bf ✓ |
| 3 | 0x267-0x27b | ADD/AND/IMUL matches | 0xbaaad0bf ✓ |

## Key Findings:

1. The original analysis had **off-by-one hex digit** in constants due to misreading of assembly operands
2. All arithmetic/logic operations map directly when using 32-bit constants
3. The state machine ultimately collapses to simple switch-case logic
4. Return value handling matches final `eax` storage at `ebp-0x10`

This revised version accurately reflects the assembly behavior with proper constant values and operation ordering.

