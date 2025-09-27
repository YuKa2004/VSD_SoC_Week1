# VSD_SoC_Week1
#  Day 1: Introduction to Verilog RTL Design & Synthesis

Welcome to **Day 1** of my RTL Workshop journey!  
Today, I'll embark on my journey into digital design by learning Verilog, open-source simulation with **Icarus Verilog (iverilog)**, and the basics of logic synthesis using **Yosys**. This guide will walk me through practical labs, essential concepts, and insightful explanations to help me build a strong foundation in RTL design.

---

##  Table of Contents

1. [What is a Simulator, Design, and Testbench?](#1-what-is-a-simulator-design-and-testbench)
2. [Getting Started with iverilog](#2-getting-started-with-iverilog)
3. [Lab: Simulating a 2-to-1 Multiplexer](#3-lab-simulating-a-2-to-1-multiplexer)
4. [Verilog Code Analysis](#4-verilog-code-analysis)
5. [Introduction to Yosys & Gate Libraries](#5-introduction-to-yosys--gate-libraries)
6. [Synthesis Lab with Yosys](#6-synthesis-lab-with-yosys)
7. [Summary](#7-summary)

---

## 1. What is a Simulator, Design, and Testbench?

###  Simulator

A **simulator** is a software tool that helps me check my digital circuit's functionality by applying test inputs and viewing outputs. This helps me verify my design before hardware implementation.

###  Design

The **design** is my Verilog code describing the intended logic functionality.

###  Testbench

A **testbench** is a simulation environment that I use to apply various inputs to my design and check if the outputs are correct.



---

## 2. Getting Started with iverilog

**iverilog** is an open-source simulator for Verilog that I'll be using. Here's the typical simulation flow I'll follow:



- I'll provide both the design and testbench as input to iverilog.
- The simulator will produce a `.vcd` file for waveform viewing in GTKWave.

---

## 3. Lab: Simulating a 2-to-1 Multiplexer

Let me simulate a simple **2-to-1 multiplexer** using iverilog!

###  Step 1: Clone the Workshop Repository

```shell
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
```

###  Step 2: Install Required Tools

```shell
sudo apt install iverilog
sudo apt install gtkwave
```

###  Step 3: Simulate the Design

I'll compile the design and testbench:

```shell
iverilog good_mux.v tb_good_mux.v
```

Now I'll run the simulation:

```shell
./a.out
```

And view the waveform:

```shell
gtkwave tb_good_mux.vcd
```

<div align="center">
      <img width="1000" height="638" alt="image" src="https://github.com/user-attachments/assets/73072cca-6b6a-4ec1-b287-ff228205bdc3" />
</div>

---

## 4. Verilog Code Analysis

**The code for the multiplexer (`good_mux.v`) that I'm analyzing:**

```verilog
module good_mux (input i0, input i1, input sel, output reg y);
always @ (*)
begin
    if(sel)
        y <= i1;
    else 
        y <= i0;
end
endmodule
```

###  **How It Works**

- **Inputs:** `i0`, `i1` (data), `sel` (select line)
- **Output:** `y` (registered output)
- **Logic:** If `sel` is 1, `y` gets `i1`; if `sel` is 0, `y` gets `i0`.

---

## 5. Introduction to Yosys & Gate Libraries

###  What is Yosys?

**Yosys** is a powerful open-source synthesis tool for digital hardware that I'll be using. It takes my Verilog code and converts it into a gate-level netlist—a hardware blueprint.

#### Yosys Features

- **Synthesis:** Converts my HDL to a logic circuit
- **Optimization:** Improves speed or area in my design
- **Technology Mapping:** Matches logic to actual hardware cells
- **Verification:** Checks correctness of my design
- **Extensibility:** Supports custom flows for my projects

###  Why Do Libraries Have Different Gate "Flavors"?

A `.lib` file contains many versions of each gate (like AND, OR, NOT) with different properties that I can choose from:

- **Performance:** Faster gates for my critical paths, slower for power savings
- **Power:** Some gates use less energy in my circuit
- **Area:** Smaller gates for my compact chips
- **Drive Strength:** Stronger gates to drive more load in my design
- **Signal Integrity:** Specialized gates for noise/performance in my circuit
- **Mapping:** Synthesis tools pick the best flavor for my specific needs

---

## 6. Synthesis Lab with Yosys

Let me synthesize the `good_mux` design using Yosys!

###  Step-by-Step Yosys Flow

1. **I'll start Yosys**
    ```shell
    yosys
    ```

2. **I'll read the liberty library**
    ```shell
    read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
    ```

3. **I'll read my Verilog code**
    ```shell
    read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v
    ```

4. **I'll synthesize my design**
    ```shell
    synth -top good_mux
    ```

5. **I'll perform technology mapping**
    ```shell
    abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
    ```

6. **I'll visualize my gate-level netlist**
    ```shell
    show
    ```
<div align="center">
      <img width="1666" height="625" alt="image" src="https://github.com/user-attachments/assets/0598e054-0585-461d-938a-cdf1897dc494" />
</div>

---

## 7. Summary

- I learned about simulators, designs, and testbenches.
- I ran my first Verilog simulation with iverilog and visualized waveforms.
- I analyzed the 2-to-1 mux code.
- I explored Yosys and learned why gate libraries have various flavors.


---
