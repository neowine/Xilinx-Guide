RTL : Register Transfer Level
---
하드웨어 레지스터들간에 신호 흐름을 설명해 놓은 것


반도체 설계에 있다보면 "알티엘 알티엘" 하는데 보통은 `VHDL`이나 `Verilog`HDL로 작성한 코드를 RTL 코드 또는 RTL이라고 많이 부르고 있다.



```verilog
wire A_in, B_in, C_in;
reg A_out, B_out, C_out;
always @( posedge clk )
begin
 A_out <= A_in;
 B_out <= A_out + 1;
 C_out <= B_out + 1;
end
```
