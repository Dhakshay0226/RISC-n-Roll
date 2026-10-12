# Register File

Design a 32×32 three-ported register file with two read ports and one write port.

The register file contains **32 registers, each 32 bits wide**.

### Module Specification

```SystemVerilog
module regfile(
    input  logic        clk,
    input  logic        we3,
    input  logic [4:0]  a1, a2, a3,
    input  logic [31:0] wd3,
    output logic [31:0] rd1, rd2
);
    logic [31:0] registers [31:0];

    // Write on the rising clock edge when enabled.
    always_ff @(posedge clk) begin
        if (we3)
            registers[a3] <= wd3;
    end

    // Asynchronous reads.
    assign rd1 = registers[a1];
    assign rd2 = registers[a2];
endmodule
```

### Working

- **Read Ports:**
    
    - `rd1` reads `rf[a1]`
        
    - `rd2` reads `rf[a2]`
        
    - Reads are **combinational**, i.e., reflect memory instantly.
        
- **Write Port:**
    
    - `rf[a3] <= wd3` on rising edge of `clk` **if `we3` is high**.
        
- **Register 0:**
    
    - Always hardwired to 0, cannot be written.

### Fixed Interface

> [!IMPORTANT]
> The module name, port list, and port widths shown above are a fixed contract for this course. Do not rename the module, rename/reorder/add/remove ports, or change port widths.
