# Sign Extender

This module generates a 32-bit immediate value from instruction fields, depending on the type of instruction (I-type, S-type, B-type, or J-type).

### Module Specification

```SystemVerilog
module extend(
    input  logic [31:7] instr,
    input  logic [1:0]  immsrc,
    output logic [31:0] immext
);
    always_comb begin
        case (immsrc)
            2'b00: immext = {{20{instr[31]}}, instr[31:20]};                         // I-type
            2'b01: immext = {{20{instr[31]}}, instr[31:25], instr[11:7]};             // S-type
            2'b10: immext = {{19{instr[31]}}, instr[31], instr[7], instr[30:25],
                             instr[11:8], 1'b0};                                     // B-type
            2'b11: immext = {{11{instr[31]}}, instr[31], instr[19:12], instr[20],
                             instr[30:21], 1'b0};                                    // J-type
            default: immext = '0;
        endcase
    end
endmodule
```

### Working

- `immsrc = 2'b00` → **I-type**    
- `immsrc = 2'b01` → **S-type**
- `immsrc = 2'b10` → **B-type**
- `immsrc = 2'b11` → **J-type** 

>[!TIP]  
> Think about which bits of the instruction correspond to each immediate type and how to extend the **sign bit** to fill 32 bits.

### Notes

- `immext` is always **sign-extended to 32 bits**, regardless of immediate type.
- **B-type** and **J-type** immediates are used as PC-relative offsets: they are shifted left by 1 when forming the branch/jump target address (`PC + (ImmExt << 1)`).

### Fixed Interface

> [!IMPORTANT]
> The module name, port list, and port widths shown above are a fixed contract for this course. Do not rename the module, rename/reorder/add/remove ports, or change port widths.
