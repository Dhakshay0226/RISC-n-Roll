# Resettable Flip-Flop

Design a 8-bit parameterized flip-flop with asynchronous reset.

### Module Specification

```SystemVerilog
module flopr #(parameter WIDTH = 8) (
    input  logic [WIDTH-1:0] d,
    input  logic             clk,
    input  logic             reset,
    output logic [WIDTH-1:0] q
);
    always_ff @(posedge clk or posedge reset) begin
        if (reset)
            q <= '0;
        else
            q <= d;
    end
endmodule
```

### Working

- Asynchronous reset: sets `q` to `0` when `reset` is high.
- Clocked behavior: updates output `q` with input `d` on the rising edge of `clk`.

> [!TIP] 
> Ensure the reset takes priority over normal data capture in the `always_ff` block.

### Fixed Interface

> [!IMPORTANT]
> The module name, port list, and port widths shown above are a fixed contract for this course. Do not rename the module, rename/reorder/add/remove ports, or change port widths.
