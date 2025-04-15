## Obfuscation Techniques Compilation Flags

1. **Bogus Control Flow (BCF)**: Compiled with flags: `-mllvm -bcf -mllvm -boguscf-prob=100 -mllvm -boguscf-loop=1`
2. **Instruction Substitution (IS)**: Compiled with flags: `-mllvm -sub`
3. **Control Flow Flattening (CFF)**: Compiled with flags: `-mllvm -fla -mllvm -perFLA=100`
4. **Combined Techniques**: Compiled with all flags: `-mllvm -sub -mllvm -fla -mllvm -perFLA=100 -mllvm -bcf -mllvm -boguscf-prob=100 -mllvm -boguscf-loop=1`
