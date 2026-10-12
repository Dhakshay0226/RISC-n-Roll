# 3:1 Multiplexer

Design an 8-bit parameterized 3:1 Multiplexer.

### Module Specification

```SystemVerilog
module mux3 #(parameter WIDTH = 8) (
    input  logic [WIDTH-1:0] d0, d1, d2,
    input  logic [1:0]       s,
    output logic [WIDTH-1:0] y
);
    always_comb begin
        case (s)
            2'b00: y = d0;
            2'b01: y = d1;
            2'b10: y = d2;
            default: y = '0;
        endcase
    end
endmodule
```

### Fixed Interface

> [!IMPORTANT]
> The module name, port list, and port widths shown above are a fixed contract for this course. Do not rename the module, rename/reorder/add/remove ports, or change port widths.
