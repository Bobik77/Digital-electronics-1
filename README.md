# Digital-electronics-1
## Personal information:
**Name:** Vaněk Pavel,
**ID:** 221072,
## This repository:
[This repository](https://github.com/Bobik77/Bobik77-Digital-electronics-1) was made for usage of  Lecture BPC-DE1,  BUT 2021.
## Examples of styles:
**bold**,
*italic*,
***bold/italic***,
## Code example:
```
signal input_stream : input; signal clk :std_logic; signal parity :bit ;
begin
U1: Parity_Generator1 port map(
input_stream, clk,
input1 : process (clk)
parity => parity );
begin
if clk <= 'U' then clk <= '0' after 1 ns; else clk <= not clk after 1 ns;
end if;
end process;
```
