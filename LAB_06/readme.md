# BPC-DE1 Lab_06
:paperclip: Repository:
[Bobik77](https://github.com/Bobik77) 
/
[Digital-electronic-1](https://github.com/Bobik77/Digital-electronics-1) 
/
[LAB_06](https://github.com/Bobik77/Digital-electronics-1/tree/main/LAB_06)

## 1. Preparation task - timing diagram
![preparationTask](img/wavedrom.png)
## 2. Display driver
### 2.1 p_mux process listing
```vhdl
    p_mux : process(s_cnt, data0_i, data1_i, data2_i, data3_i, dp_i)
    begin
        case s_cnt is
            when "11" =>
                s_hex <= data3_i;
                dp_o  <= dp_i(3);
                dig_o <= "0111";

            when "10" =>
                s_hex <= data2_i;
                dp_o  <= dp_i(2);
                dig_o <= "1011";

            when "01" =>
                s_hex <= data1_i;
                dp_o  <= dp_i(1);
                dig_o <= "1101";

            when others =>
                s_hex <= data0_i;
                dp_o  <= dp_i(0);
                dig_o <= "1110";
        end case;
    end process p_mux;
```
### 2.2 TestBench listing (konečně i s asserty) 
```vhdl
------------------------------------------------------------------------
-- Architecture body for testbench
------------------------------------------------------------------------
architecture testbench of tb_driver_7seg_4digits is

    -- Local constants
    constant c_CLK_100MHZ_PERIOD : time    := 10 ns;

    --Local signals
    signal s_clk_100MHZ : std_logic;
    signal s_reset      : std_logic;
    signal s_data0      : std_logic_vector(3 downto 0);
    signal s_data1      : std_logic_vector(3 downto 0);
    signal s_data2      : std_logic_vector(3 downto 0);
    signal s_data3      : std_logic_vector(3 downto 0);   
    signal s_dpi        : std_logic_vector(3 downto 0);
    signal s_seg        : std_logic_vector(6 downto 0);
    signal s_dig        : std_logic_vector(3 downto 0);
    signal s_dpo        : std_logic;
    
    
begin
    -- Connecting testbench signals with driver_7seg_4digits entity
    -- (Unit Under Test)
    uut_driver_7seg_4digits: entity work.driver_7seg_4digits
        port map(
            clk     => s_clk_100MHZ,
            reset   => s_reset,
            data0_i => s_data0,
            data1_i => s_data1,
            data2_i => s_data2,
            data3_i => s_data3,
            dp_i    => s_dpi,   -- dec. point input
            seg_o   => s_seg,   -- segment A-G output
            dig_o   => s_dig,   -- digit selector
            dp_o    => s_dpo    -- dec point output
            );

    --------------------------------------------------------------------
    -- Clock generation process
    --------------------------------------------------------------------
    p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHZ_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHZ_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;

    --------------------------------------------------------------------
    -- Reset generation process
    --------------------------------------------------------------------
    p_reset : process
    begin
        s_reset <= '1';
        wait for 10 ns;
        s_reset <= '0';
        wait;
    end process p_reset;

    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        s_data3 <= "0011";
        s_data2 <= "0001";
        s_data1 <= "0100";
        s_data0 <= "0010";
        s_dpi   <= "0111";
        
       --------------------------------------------------------------------
       -- Data check process
       --------------------------------------------------------------------
        -- digit is shown for 40ns
        -- clk tick is 5ns long (see clk_en0)
        -- whole refresh is done after 160ns (digits)
        wait for 15 ns; -- reset ofset (10ns + 1 tick)
        assert (s_seg = "0000110") and (s_dig = "0111") and (s_dpo = '0')
        -- test 1.st digit for number 3 and dec. point
        report "1.st digit display failed" severity error;
        
        wait for 40 ns; -- wait for next digit
        assert (s_seg = "1001111") and (s_dig = "1011") and (s_dpo = '1')
        -- test 2.nd digit for number 1 and no dec. point
        report "2.nd digit display failed" severity error;
        
        wait for 40 ns; -- wait for next digit
        assert (s_seg = "1001100") and (s_dig = "1101") and (s_dpo = '1')
        -- test 3.rd digit for number 4 and no dec. point
        report "3.rd digit display failed" severity error;
        
        wait for 40 ns; -- wait for next digit
        assert (s_seg = "0010010") and (s_dig = "1110") and (s_dpo = '1')
        -- test 4.th digit for number 2 and no dec. point
        report "4.th digit display failed" severity error;
        
        wait; 
    end process p_stimulus;

end architecture testbench;
```
### 2.3 Waveform screenshot
![waveform1](img/waveform1.png)
### 2.4 Top layer architecture listing
```vhdl
architecture Behavioral of top is
    -- No internal signals
begin

    --------------------------------------------------------------------
    -- Instance (copy) of driver_7seg_4digits entity
    driver_seg_4 : entity work.driver_7seg_4digits
        port map(
            clk        => CLK100MHZ,
            reset      => BTNC,
            -- each group of 4 sw controls one digit
            -- data0  -- right digit
            data0_i(3) => SW(3),
            data0_i(2) => SW(2),
            data0_i(1) => SW(1),
            data0_i(0) => SW(0),
            -- data1
            data1_i(3) => SW(7),
            data1_i(2) => SW(6),
            data1_i(1) => SW(5),
            data1_i(0) => SW(4),
            -- data2
            data2_i(3) => SW(11),
            data2_i(2) => SW(10),
            data2_i(1) => SW(9),
            data2_i(0) => SW(8),
            -- data3 -- left digit
            data3_i(3) => SW(15),
            data3_i(2) => SW(14),
            data3_i(1) => SW(13),
            data3_i(0) => SW(12),
            -- set fix decimal point
            dp_i => "0111",
            -- Outputs
            seg_o(6)    => CA,
            seg_o(5)    => CB,
            seg_o(4)    => CC,
            seg_o(3)    => CD,
            seg_o(2)    => CE,
            seg_o(1)    => CF,
            seg_o(0)    => CG,
            dp_o        => DP,
            dig_o       => AN(3 downto 0)
        );

    -- Disconnect the top four digits of the 7-segment display
    AN(7 downto 4) <= b"1111";

end architecture Behavioral;
```
## 3. Eight-digit driver scheme
![scheme1](img/scheme.png)