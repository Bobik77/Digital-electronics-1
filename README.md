# Digital-electronics-1
**Name:** Vaněk Pavel,
**ID:** 221072,
## Emphasis example:
**bold**,
*italic*,
***bold/italic***,
## Lists examples:
### Ordered
1. Základy digitálních obvodů a kombinační logiky
2. Principy sekvenčních obvodů a konečných automatů
3. Psaní kódu ve VHDL
4. Navrhování testbench ve VHDL
5. Navrhování obvodů pro FPGA
### Unordered
* DE1
    * Bool algebra
    * VHDL
    * ...
* AE1
* AUD
## Link example:
[This repository](https://github.com/Bobik77/Bobik77-Digital-electronics-1) was made for usage of  Lecture BPC-DE1;  BUT 2021.
## Table example
 | Col1  | Col2 |
 | :--: | :--: |
 | Row2 |  Row2 |
 | Row3 |  Row3 |
 | Row4 |  Row4 |
 ## Code example in VHDL:
```vhdl
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