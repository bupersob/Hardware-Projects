# RTL and verification learning plan

Eight modules broken into small sections, each a checklist of to-dos. Every design you build goes into GitHub in its own folder, with its testbench and a README. Work at your own pace. Alongside the modules, do one hour of LeetSilicon every day.

Mark a to-do done by changing `- [ ]` to `- [x]`.

## How this works

The goal is competence in RTL design and verification: writing synthesizable SystemVerilog you can predict gate by gate, writing testbenches that show it works, and understanding a system well enough to design your own large projects. Testbenches, assertions, coverage, and formal proofs stay central because they are how you know a design works. UVM, the class library that industrial DV teams build on, is cut to a short introduction. Learn it in depth only if you later choose DV as a career.

**Daily practice:** one hour of LeetSilicon every day, on top of module work. It builds speed and fluency on short RTL problems; the modules build depth on complete designs. It has no checkboxes here.

Each section lists why it matters, its materials, and to-dos in order. The repo holds only designs you build, one folder per design. HDLBits solutions, readings, and small demos that only show how a language feature or tool behaves stay out of it. Each module has a target date to keep a steady pace, but nothing else is tied to a calendar.

SystemVerilog runs through every module. Module 1 teaches its design subset, which describes hardware. Module 2 teaches its verification subset, which tests hardware. Modules 1 and 2 are the structured language course: Harris & Harris for design, Spear & Tumbush for verification, and the IEEE 1800-2023 standard as the reference. Module 3 covers formal verification, which proves properties mathematically instead of testing examples.

HDLBits comes first, in module 0. Verification means judging whether hardware behaves correctly, so it depends on logic design skill, and HDLBits drills that skill. Module 1 does not repeat any circuit HDLBits already had you build. It covers what HDLBits leaves out: timing, synthesis, simulator scheduling, resets and clock domain crossing, memories and FIFOs, real testbenches, and hardware. Nothing builds on an HDLBits solution. When a to-do needs a circuit you already wrote there, you write it again from scratch.

There is no note-taking in this plan. When a concept matters, a to-do has you build something that shows it.

Items marked **Hardware** run on your Arty A7.

## Tools and hardware

| Tool | Use it for |
| --- | --- |
| Lab ChipVerify | Everyday RTL work: simulation with waveforms, lint, code coverage, FSM diagrams, synthesis to real gates, and short formal checks. The free tier allows 20 simulations a day. |
| EDA Playground | Class-based testbenches, covergroups, and UVM. Aldec Riviera-PRO supports SystemVerilog and UVM and needs no account validation. Synopsys VCS and Cadence simulators need a validated institutional email, which your utexas.edu address provides. |
| Local Icarus, Verilator, SymbiYosys | Long regressions, deeper formal proofs, cocotb, and RISC-V tools. Use Linux, WSL, or macOS. |
| Vivado (free Standard edition) | Building and programming the Arty A7. |

### Hardware: Digilent Arty A7

DV itself is done in simulation before a chip exists, so hardware is not required. A board still helps in three ways. Hardware exposes problems that simulation hides, such as unsynchronized button inputs and real timing. It gives you post-silicon-style bring-up experience, which matters for validation roles. It also turns your projects into something you can demo.

The Arty A7 is built around an AMD Artix-7 FPGA (the 35T or 100T, depending on your variant) with a 100 MHz board clock. For user I/O it has four switches, four buttons, four green LEDs, and four RGB LEDs, plus Pmod headers for add-on modules. It has no seven-segment display, so the hardware items use the LEDs instead. Its micro-USB port carries both programming and a USB-UART bridge, which lets the UART project talk directly to your laptop. It works with the free Standard edition of Vivado.

## GitHub

The repo holds only designs you build. HDLBits solutions and small demos that only show how a language feature or tool behaves never go in it.

Each design gets its own folder, named for the design in lowercase with hyphens, such as `carry-lookahead-adder` or `sync-fifo`. Every planned design already has a placeholder folder with a README template, so the repo shows the work ahead. Each README starts with a status line; change it from "not started" as you go, and update the matching row in the top-level README. The design and its verification live together: RTL (register-transfer level code, the synthesizable SystemVerilog) in `rtl/`, testbenches, assertions, and formal properties in `tb/`. Commit whenever something works.

```
hardware-projects/
  README.md                  table of every design with plan sections and status
  .gitignore
  sync-fifo/
    README.md                design and verification writeup
    rtl/
    tb/
    images/                  only if a waveform or schematic shows a bug or result
```

Each design README covers what the design does, its inputs and outputs, and a verification section: the reference model, what the testbench covers, how to run it, and the bugs you injected and which check caught each. Record bugs you hit while building it, since those show how you debug. When a later section extends an existing design, such as adding a receive FIFO to the UART, update that design's folder instead of making a new one.

The empty `rtl/` and `tb/` folders contain a `.gitkeep` file, an empty placeholder that makes git keep the folder. Delete it once the folder has real files. If you build a design the plan doesn't list, add a folder and a row for it.

## Module 0: HDLBits and setup

*Finish HDLBits first, then spend a few sessions on setup*

Finish every HDLBits problem, then get every tool working and set up the GitHub repo your projects will live in.

### Finish HDLBits

HDLBits covers the Verilog language and the standard combinational and sequential circuits. Module 1 assumes you have solved all of it and does not make you build those circuits again.

**Materials**

- [HDLBits](https://hdlbits.com/), every track

- [ ] Finish every remaining problem in Verilog Language, including More Verilog Features.
- [ ] Finish every remaining problem in Circuits › Combinational Logic.
- [ ] Finish every remaining problem in Circuits › Sequential Logic: latches and flip-flops, counters, shift registers, more circuits, and finite state machines.
- [ ] Finish every remaining problem in Circuits › Building Larger Circuits.
- [ ] Finish the Verification tracks: Reading Simulations and Writing Testbenches.
- [ ] Go back to any problem you skipped or solved by trial and error and solve it cleanly.

### Tools and repository

Fixing tool problems later costs far more time than fixing them now.

**Materials**

- [Lab ChipVerify](https://lab.chipverify.com/ide.html)
- [EDA Playground](https://www.edaplayground.com/)
- Icarus Verilog, Verilator, and Surfer or GTKWave installed locally
- Vivado Standard edition (free) for the Arty A7

- [ ] Create a GitHub repo named `hardware-projects`, laid out as shown in the “GitHub” section.
- [ ] Set up the repo from the starter zip, which includes a placeholder folder for every planned design. Delete any placeholder for a design the plan no longer includes, such as the UVM environments.
- [ ] Make a Lab ChipVerify account, connect GitHub, and simulate a single AND gate with a waveform.
- [ ] Log in to [EDA Playground](https://www.edaplayground.com/) with your utexas.edu address. Run a hello-world SystemVerilog file on Aldec Riviera-PRO, which needs no account validation.
- [ ] Install Icarus Verilog and Verilator locally (on Linux, WSL, or macOS) and run the same AND gate file.
- [ ] Make a free [Verification Academy](https://verificationacademy.com/topics/systemverilog/) account.
- [ ] Download the free [IEEE 1800-2023 SystemVerilog standard](https://ieeexplore.ieee.org/browse/standards/get-program/page) and bookmark it as your language reference.
- [ ] Install Vivado, download Digilent's Arty A7 master XDC constraints file for your variant (35T or 100T), and blink an LED.

### Done when

- Every HDLBits problem is solved.
- Every tool below runs a test file.
- The repo exists with its top-level README.

## Module 1: Digital design in SystemVerilog

*Aim to finish before Thanksgiving 2026*

Understand the hardware you will verify, and write synthesizable SystemVerilog you can predict gate by gate.

### 1.1 Logic review, lint, and testbench basics

HDLBits taught the language and the combinational circuits. What it skips is the Boolean theory behind them, lint tools, and testbenches that check themselves.

**Materials**

- Harris & Harris ch. 1–2 (skim what 406H already covered; the timing section, 2.9, is assigned in 1.2)
- Harris & Harris section 4.9 (testbenches)

- [ ] Read Harris & Harris chapters 1 and 2 through 2.8, skimming anything 406H already covered. Leave 2.9 on timing for section 1.2.
- [ ] Write a 4-to-2 priority encoder in an `always_comb` block, but leave one output unassigned in one branch. Find the resulting latch with `verilator --lint-only -Wall` and in the Lab's synthesized schematic, then fix it.
- [ ] Read Harris & Harris 4.9. Write a self-checking testbench for the priority encoder that reads its test vectors from a file with `$readmemb`.

### 1.2 Arithmetic circuits and combinational timing

Adders and ALUs appear in every processor, and propagation delay is half of timing analysis.

**Materials**

- Harris & Harris ch. 2 (timing: propagation and contamination delay, glitches)
- Harris & Harris ch. 5 (arithmetic circuits: adders, subtractors, comparators, ALU, shifters)

- [ ] Write a parameterized ripple-carry adder and a carry-lookahead adder from scratch. Synthesize both at 8, 16, and 32 bits and record the cell counts in a table in the README.
- [ ] Give every gate in the 8-bit versions a `#1` delay. Find the input pair that makes the carry ripple through all eight bits, measure the worst-case delay in the waveform, and compare it with the carry-lookahead adder's.
- [ ] Build a 32-bit ALU (add, sub, AND, OR, XOR, SLT, SLTU, shifts) with zero, negative, carry, and overflow flags.
- [ ] Write a self-checking ALU testbench that runs 10,000 random vectors against a reference function in one simulation.
- [ ] Add directed tests to the ALU testbench for all four combinations of signed overflow and unsigned carry-out. For example, `0x7FFFFFFF + 1` overflows without a carry, and `0xFFFFFFFF + 1` carries without overflowing.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 1.3 Flip-flops, resets, and nonblocking assignment

Most real bugs involve state, and most beginner RTL bugs come from misunderstanding how simulators schedule assignments.

**Materials**

- Harris & Harris ch. 3 (latches, flip-flops, synchronous logic design)
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “Nonblocking Assignments in Verilog Synthesis, Coding Styles That Kill!” (SNUG 2000)
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings & Mills, “Synchronous Resets? Asynchronous Resets? I am so confused!” (SNUG 2002)
- [IEEE 1800-2023 SystemVerilog standard](https://ieeexplore.ieee.org/browse/standards/get-program/page): the clause on scheduling semantics (event regions)

- [ ] Build an SR latch, a D latch, and a master-slave D flip-flop from gate primitives with small delays. Simulate each through a clock cycle and confirm in the waveform where each one is transparent.
- [ ] Read the nonblocking assignment paper.
- [ ] Read the scheduling semantics clause of the standard. Write a short simulation in which `$display` and `$strobe` print different values for the same nonblocking assignment, and add a `#0` case that shows the inactive region.
- [ ] Build a 3-stage shift register with blocking assignments, capture the broken waveform, then fix it.
- [ ] Read the resets paper. Write an 8-bit register with synchronous reset and one with asynchronous reset, synthesize both, and record which flip-flop cells each uses.
- [ ] Build a reset synchronizer (asynchronous assert, synchronous release).
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 1.4 Clock enables and an exhaustive check

Timers, baud generators, and slow logic all run off clock enables, and checking every reachable state is the simplest form of complete verification.

**Materials**

- Harris & Harris ch. 5 (sequential building blocks)
- [Mutlu, DDCA (ETH Zürich, Spring 2025)](https://safari.ethz.ch/ddca/spring2025/): sequential logic lectures

- [ ] Write a clock-enable generator that pulses once every N cycles. Use it to build a 1 Hz LED blinker, then build a second blinker that clocks its flip-flop from a counter bit instead. Run both through Vivado and compare the `check_timing` reports: the divided clock leaves its flip-flops with no defined clock, so timing analysis never checks them.
- [ ] Write a parameterized LFSR from scratch and configure it at 16 bits with a maximal-length tap set. Write a testbench that confirms in one simulation that it visits all 65,535 nonzero states.
- [ ] **Hardware:** Show a 4-bit counter on the Arty A7's green LEDs, advancing once per second from your clock-enable generator. Add a debouncer on the button that resets it.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 1.5 Finite state machines

Protocol controllers are FSMs, and FSM corner cases are common in DV interviews.

**Materials**

- Harris & Harris ch. 3 (finite state machines)
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “Coding and Scripting Techniques for FSM Designs with Synthesis-Optimized, Glitch-Free Outputs” (SNUG 2000)

- [ ] Read the FSM coding paper.
- [ ] Build a traffic light controller with a timer and a pedestrian request input, written with `enum`, `always_ff`, and `always_comb` as the FSM paper recommends. Check it against the Lab's FSM analyzer diagram.
- [ ] Decide what the controller does if its state register lands in an unused encoding. Test it by forcing the state register into each unused encoding in simulation.
- [ ] **Hardware:** Run the traffic light controller on the Arty A7, using the RGB LEDs as the lights and a button as the pedestrian request.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 1.6 Sequential timing, metastability, and clock domain crossing

Timing is where hardware stops behaving like software, and clock domain crossing (CDC) bugs are among the costliest to find after fabrication.

**Materials**

- Harris & Harris ch. 3 (timing of sequential logic, clock skew, metastability, synchronizers)
- [Mutlu, DDCA (ETH Zürich, Spring 2025)](https://safari.ethz.ch/ddca/spring2025/): timing and verification lecture
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “Clock Domain Crossing (CDC) Design & Verification Techniques Using SystemVerilog” (SNUG 2008), synchronizer and multi-bit sections

- [ ] Read the CDC paper's synchronizer sections.
- [ ] Build a 2-flop synchronizer, a pulse synchronizer, and a toggle handshake.
- [ ] Add metastability injection to the 2-flop synchronizer's testbench: when the input changes within a few time units of the clock edge, let the first flip-flop randomly settle to either value. Confirm the synchronized output is always a clean 0 or 1, arriving at most one cycle later than without injection.
- [ ] Pass a 4-bit binary counter into a second clock domain through four independent 2-flop synchronizers, with injection on. Write a checker that catches the values the counter never held. Then switch to a Gray-coded counter and show the checker passes.
- [ ] Synthesize a register-adder-register path and estimate its maximum frequency by hand.
- [ ] **Hardware:** Implement the same path in Vivado, read its timing report, and compare with your hand estimate.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 1.7 Memory arrays and FIFOs

FIFOs are the classic verification target: simple to describe and full of edge cases.

**Materials**

- Harris & Harris ch. 5 (memory arrays)
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “Simulation and Synthesis Techniques for Asynchronous FIFO Design” (SNUG 2002)
- [ZipCPU beginner's tutorial](https://zipcpu.com/tutorial/): FIFO lesson

- [ ] Build a register file and a synchronous single-port RAM.
- [ ] Build a synchronous FIFO with parameterized depth, full, empty, and count.
- [ ] Write a testbench that forces full, empty, simultaneous read and write, and reset during traffic.
- [ ] Inject three bugs (off-by-one full, read allowed when empty, count wrap) and confirm the testbench catches each.
- [ ] Push line coverage above 95% with the Lab's coverage report.
- [ ] Read the asynchronous FIFO paper and build its asynchronous FIFO, with Gray-coded pointers. Test it with unrelated read and write clock frequencies and metastability injection on the pointer synchronizers.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 1.8 Project: UART with a first formal proof

A complete peripheral combines counters, FSMs, and FIFOs, and it is your first portfolio project.

**Materials**

- [ZipCPU beginner's tutorial](https://zipcpu.com/tutorial/): serial port transmitter and receiver lessons
- [ZipCPU formal methods courseware](https://zipcpu.com/tutorial/formal.html): first lessons on basic properties and bounded model checking

- [ ] Build a UART transmitter, using your clock-enable generator from 1.4 for the baud rate.
- [ ] Build a UART receiver from scratch with a 2-flop input synchronizer, 16× oversampling, and mid-bit sampling.
- [ ] Connect TX to RX in loopback and send 10,000 random bytes in one simulation.
- [ ] Add a FIFO on the receive side.
- [ ] Write three formal properties for the transmitter (idle high, start bit low, busy for exactly one frame) and run them with the Lab's formal tool.
- [ ] Write the project README: design, testbench, coverage, formal results, and one bug each method found.
- [ ] **Hardware:** Run the UART on the Arty A7 through its USB-UART bridge. Type in a serial terminal on your laptop and echo characters back. Record any bug that appeared on hardware but not in simulation in the README.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### Done when

- You can design and test a small FSM from a written spec without notes.
- You can compute maximum clock frequency and explain setup, hold, and metastability from first principles.
- You can explain nonblocking assignment in terms of the simulation event queue.
- The UART runs on hardware or in a complete loopback simulation, with its README complete.

## Module 2: SystemVerilog for verification

*Aim to finish by mid-February 2027*

Build class-based testbenches with constrained randomization, functional coverage, and assertions.

### 2.1 Verification planning

A verification engineer's first product is a plan, not code.

**Materials**

- Spear & Tumbush ch. 1 (verification guidelines)
- [Verification Academy](https://verificationacademy.com/topics/systemverilog/): the NC State functional verification course track, opening sessions

- [ ] Read Spear & Tumbush ch. 1.
- [ ] Watch the opening sessions of the NC State track.
- [ ] Write a verification plan for your FIFO: features, checks, stimulus, and coverage items.
- [ ] Add a section to the FIFO plan listing what your module 1 FIFO testbench never tested.
- [ ] **Document:** add the plan to the README of the design it covers.

### 2.2 Data types and routines

Testbench code depends on queues, associative arrays, and structs far more than RTL does.

**Materials**

- Spear & Tumbush ch. 2 (data types) and ch. 3 (procedural statements and routines)
- [IEEE 1800-2023 SystemVerilog standard](https://ieeexplore.ieee.org/browse/standards/get-program/page): data types and aggregate data types clauses, as reference

- [ ] Read ch. 2 and type every array example, predicting output before running.
- [ ] Replace the FIFO checker's expected values with a queue-based reference model.
- [ ] Read ch. 3.
- [ ] Write a small checker library: a compare task with time and values, and a pass/fail summary.
- [ ] Write a task with a local variable and call it from two threads at once with `fork`. Run it as a static task, then as `automatic`, and show the static version corrupting its local variable.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.3 Interfaces, clocking blocks, and races

Races between testbench and design cause the most confusing testbench failures.

**Materials**

- Spear & Tumbush ch. 4 (connecting the testbench and design)
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “Applying Stimulus & Sampling Outputs: UVM Verification Testing Techniques” (SNUG 2016)

- [ ] Read ch. 4.
- [ ] Add a clocking block to your 1.3 scheduling demo and print when it samples inputs and drives outputs relative to the clock edge.
- [ ] Build a FIFO interface with driver and monitor clocking blocks, and route all testbench access through it.
- [ ] Read the driving and sampling sections of the stimulus paper.
- [ ] Create a testbench race on purpose, show it in Icarus and Verilator, and fix it.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.4 Object-oriented programming

UVM is a class library, so every UVM concept depends on OOP.

**Materials**

- Spear & Tumbush ch. 5 (basic OOP) and ch. 8 (advanced OOP)
- [Verification Academy](https://verificationacademy.com/topics/systemverilog/): “SystemVerilog OOP for UVM Verification” sessions
- [EDA Playground](https://www.edaplayground.com/) with Riviera-PRO for class-based code

- [ ] Read ch. 5.
- [ ] Write a packet class with `display`, `compare`, and `copy`. Demonstrate shallow vs. deep copy with a nested object.
- [ ] Watch the Verification Academy OOP sessions.
- [ ] Read ch. 8.
- [ ] Store base and derived transactions in one queue of base handles and call a virtual method on each. Recover the derived type with `$cast`.
- [ ] Show what breaks when the method is not virtual.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.5 Constrained randomization

Random stimulus finds bugs nobody thought to write a test for.

**Materials**

- Spear & Tumbush ch. 6 (randomization)

- [ ] Read ch. 6 first half.
- [ ] Write a FIFO operation class with constraints on operation, burst length, and idle gap.
- [ ] Weight toward full and empty with `dist`. Write a fill-completely test with an inline `with` constraint.
- [ ] Read ch. 6 second half.
- [ ] Print a histogram of generated values and check it matches your weights.
- [ ] Write an unsolvable constraint and read the simulator's error.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.6 Threads and the layered testbench

The layered testbench is the structure UVM formalizes.

**Materials**

- Spear & Tumbush ch. 7 (threads and interprocess communication) and ch. 11 (a complete testbench)

- [ ] Read ch. 7. Write examples of `fork…join_any`, `disable fork`, and a bounded mailbox.
- [ ] Split the FIFO testbench into generator, driver, monitor, scoreboard, and environment classes connected by mailboxes.
- [ ] Read ch. 11 for structure.
- [ ] Add an end-of-test mechanism that waits until every transaction is checked.
- [ ] Swap in a second generator without editing any other class.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.7 Functional coverage

Coverage tells you when to stop testing and how much of the plan you have exercised.

**Materials**

- Spear & Tumbush ch. 9 (functional coverage)
- [Verification Academy: UVM topics](https://verificationacademy.com/topics/uvm-universal-verification-methodology/): Coverage Cookbook

- [ ] Read ch. 9.
- [ ] Write a FIFO covergroup: fill-level bins, operation type, and operation crossed with full and empty.
- [ ] Read the Coverage Cookbook section on building a coverage model from a plan.
- [ ] Map every coverage item to a line in your section 2.1 plan.
- [ ] Run until coverage stops rising, change constraints to close holes, and record what you changed.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.8 SystemVerilog Assertions (SVA)

Assertions catch bugs where they happen instead of many cycles later.

**Materials**

- Spear & Tumbush ch. 4 section on assertions
- [IEEE 1800-2023 SystemVerilog standard](https://ieeexplore.ieee.org/browse/standards/get-program/page): assertions clause, as reference
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “SystemVerilog Assertions Design Tricks and SVA Bind Files” (SNUG 2009)

- [ ] Read the assertion material: immediate vs. concurrent, sequences, `|->` and `|=>`, `$rose`, `$past`, `disable iff`.
- [ ] Read the Cummings SVA paper.
- [ ] Write 10 concurrent assertions for the FIFO and UART in a bind file.
- [ ] Inject a bug for each assertion and confirm it fires.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.9 Project: verify an APB register block

APB is the simplest real bus, and register blocks are common DV work.

**Materials**

- [Arm AMBA APB specification](https://developer.arm.com/documentation/ihi0024/latest/)
- [ZipCPU formal blog posts](https://zipcpu.com/formal/formal.html): bus slave verification posts, for property ideas

- [ ] Read the APB specification.
- [ ] Design an APB slave with a read/write control register, read-only status, write-1-to-clear interrupt, and a counter.
- [ ] Write the verification plan.
- [ ] Write APB protocol assertions from the specification.
- [ ] Build the layered testbench with a register reference model in the scoreboard.
- [ ] Add constrained-random sequences including invalid addresses and back-to-back transfers.
- [ ] Add coverage, inject five bugs, and record which checks caught each.
- [ ] Write the project README.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 2.10 cocotb

Many teams write testbenches in Python.

**Materials**

- [cocotb docs](https://docs.cocotb.org/)

- [ ] Install cocotb locally with Icarus or Verilator.
- [ ] Write a cocotb test for the APB block with a Python reference model.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### Done when

- You can write a layered class-based testbench from a blank file.
- You can write constraints, covergroups, and concurrent assertions without looking up syntax.
- The APB project catches every injected bug and reports functional coverage.

## Module 3: Formal verification

*Aim to finish by early March 2027*

Prove properties mathematically instead of testing examples, using SymbiYosys.

### 3.1 Bounded model checking

Formal tools check every input sequence up to a depth, and many DV teams use them alongside simulation.

**Materials**

- [ZipCPU formal methods courseware](https://zipcpu.com/tutorial/formal.html): slides and exercises on basic formal and bounded model checking
- [Lab ChipVerify](https://lab.chipverify.com/ide.html) user guide: Formal Verification section
- SymbiYosys installed locally for proofs deeper than the Lab's free-tier depth of 10

- [ ] Work through the basic formal lessons and exercises.
- [ ] Install SymbiYosys locally.
- [ ] Prove that the counter in your 1.4 clock-enable generator never exceeds its terminal count.
- [ ] Add a bug to that counter that only shows up after 20 cycles. Show bounded model checking passes at depth 10 and fails at depth 25.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 3.2 Induction and interface properties

Induction turns a bounded check into a full proof.

**Materials**

- [ZipCPU formal methods courseware](https://zipcpu.com/tutorial/formal.html): induction and interface property lessons
- [ZipCPU formal blog posts](https://zipcpu.com/formal/formal.html)

- [ ] Work through the induction lessons.
- [ ] Prove the FIFO count invariant with induction.
- [ ] Write `assume` properties for APB inputs and `assert` properties for outputs.
- [ ] Run a full proof on the APB block locally and fix anything it finds.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### Done when

- You can explain bounded model checking and induction.
- The FIFO and APB block have formal proofs, with any bugs formal found documented.

## Module 4: UVM, a first look

*Aim to finish by late March 2027*

See how UVM formalizes the layered testbench you built in module 2.

### 4.1 UVM foundations

UVM is the industry-standard testbench framework. A short look lets you read industrial testbenches and decide later whether to go deeper.

**Materials**

- [Verification Academy: UVM Basics](https://verificationacademy.com/courses/basic-uvm)
- Salemi, *The UVM Primer*: early chapters
- [EDA Playground](https://www.edaplayground.com/) with Riviera-PRO and UVM selected, or local Verilator 5.052 or newer

- [ ] Watch the UVM Basics sessions.
- [ ] Read the early UVM Primer chapters.
- [ ] Run a hello world test with `uvm_info` at several verbosity levels.
- [ ] Write a transaction with field macros and one without, and compare.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 4.2 Phases and the factory

Phases decide when things happen and the factory decides what gets built.

**Materials**

- Salemi, *The UVM Primer*: factory and phases chapters
- [Sunburst Design papers](http://www.sunburst-design.com/papers/): Cummings, “The OVM/UVM Factory & Factory Overrides: How They Work, Why They Are Important” (SNUG 2012)

- [ ] Read the factory chapters and the Cummings factory paper.
- [ ] Build an environment that prints in every phase and confirm the order.
- [ ] Use a type override to swap in an error-injecting transaction without editing the environment.
- [ ] Use an instance override that affects one of two identical components.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### Done when

- You can explain what UVM phases and the factory do and how they map onto your module 2 testbench.

## Module 5: Design a RISC-V core

*Aim to finish by late May 2027*

Build the design your flagship verification project will target.

### 5.1 RISC-V instruction set and tools

You will design and verify a RISC-V core, so you need the instruction set cold.

**Materials**

- Harris & Harris ch. 6 (architecture)
- [RISC-V ratified specifications](https://riscv.org/specifications/ratified/): RV32I base chapter
- [Mutlu, DDCA (ETH Zürich, Spring 2025)](https://safari.ethz.ch/ddca/spring2025/): instruction set architecture lectures
- [Spike](https://github.com/riscv-software-src/riscv-isa-sim)

- [ ] Read Harris & Harris ch. 6.
- [ ] Write a Python script that encodes and decodes RV32I instructions in every format. Check it against the toolchain's `objdump` on 20 instructions.
- [ ] Install the RISC-V GNU toolchain and Spike locally.
- [ ] Compile a C program and run it on Spike with commit logging on.

### 5.2 Single-cycle core

A single-cycle core is the simplest correct processor and your reference for the pipeline.

**Materials**

- Harris & Harris ch. 7 (single-cycle processor)
- [Mutlu, DDCA (ETH Zürich, Spring 2025)](https://safari.ethz.ch/ddca/spring2025/): microarchitecture lectures

- [ ] Draw the full datapath for the README before coding.
- [ ] Implement the datapath, reusing your ALU and register file.
- [ ] Implement the main and ALU decoders.
- [ ] Run an array-sum program assembled with your 5.1 encoder.
- [ ] Lint and synthesize with zero warnings.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 5.3 Running real programs

riscv-tests is the official per-instruction suite.

**Materials**

- [riscv-tests](https://github.com/riscv-software-src/riscv-tests)

- [ ] Build riscv-tests and convert binaries to memory files.
- [ ] Run all rv32ui tests and fix failures one at a time.
- [ ] Run a compiled C program.
- [ ] Start a bug log: symptom, root cause, fix.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 5.4 Pipelining

Pipelines create the hazards that make processor verification hard.

**Materials**

- Harris & Harris ch. 7 (pipelined processor)
- [Mutlu, DDCA (ETH Zürich, Spring 2025)](https://safari.ethz.ch/ddca/spring2025/): pipelining and hazard lectures

- [ ] Draw the five-stage pipeline, with every pipeline register, for the README.
- [ ] Convert to five stages with no hazard handling and write programs that break it.
- [ ] Add forwarding.
- [ ] Add load-use stalls.
- [ ] Add branch and jump flushing.
- [ ] Pass all rv32ui tests again.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 5.5 Peripheral and hardware bring-up

A real system has peripherals, and running on hardware exposes problems simulation hides.

**Materials**

- Your UART and APB designs
- [Digilent Arty A7 reference](https://digilent.com/reference/programmable-logic/arty-a7/start)

- [ ] Memory-map the UART.
- [ ] Write a C program that prints over UART and decode the output in the testbench.
- [ ] Synthesize the full system and record resource use.
- [ ] **Hardware:** Run the core on the Arty A7 and print “hello” to your laptop's serial terminal. Record every issue that appeared only on hardware in the README.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### Done when

- The pipelined core passes the RV32I riscv-tests.
- A C program prints through your UART, in simulation and on hardware if you have the board.

## Module 6: Verify your core

*Aim to finish by mid-July 2027*

Verify your core against a reference model with random programs, coverage, and assertions, and document the results.

### 6.1 Verification plan

Industrial CPU verification starts with a plan.

**Materials**

- [Ibex documentation](https://ibex-core.readthedocs.io/): verification section

- [ ] Read how Ibex is verified.
- [ ] Write the plan: features, trace-comparison checking, stimulus sources.
- [ ] Define the coverage model: every opcode, every register as source and destination, branch outcomes crossed with stall and flush.
- [ ] Get the plan reviewed by your mentor or dad.
- [ ] **Document:** add the plan to the README of the design it covers.

### 6.2 Testbench and trace comparison

Comparing against a reference model checks every instruction.

**Materials**

- [Spike](https://github.com/riscv-software-src/riscv-isa-sim)
- [Ibex documentation](https://ibex-core.readthedocs.io/)

- [ ] Build a class-based SystemVerilog or cocotb testbench around the core with a memory model.
- [ ] Write a monitor that logs every committed instruction.
- [ ] Write a script that compares your log with Spike's and reports the first mismatch.
- [ ] Insert a bug and confirm the report points to it.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 6.3 Random instruction generation

Random programs hit combinations nobody writes by hand.

**Materials**

- [riscv-dv](https://github.com/chipsalliance/riscv-dv): README and user guide

- [ ] Set up riscv-dv and generate RV32I programs.
- [ ] Run them on Spike and your core.
- [ ] Automate generate, compile, run, and compare over hundreds of seeds.
- [ ] Fix the bugs it finds and log them.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 6.4 Coverage, assertions, and formal on the core

Coverage proves the random programs hit what the plan requires.

**Materials**

- Your module 2 and 3 notes

- [ ] Implement the coverage model.
- [ ] Add assertions: x0 reads zero, flushed instructions never commit, legal PC changes.
- [ ] Prove the forwarding logic formally.
- [ ] Map coverage results to the plan.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 6.5 Closure and bug injection

Measured results separate a verification project from a design project.

**Materials**

- No new reading

- [ ] Run large regressions and close coverage holes.
- [ ] Inject 10 realistic bugs and measure which check caught each and how fast.
- [ ] Publish a results table.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 6.6 Package the project

The project only helps if you can explain it.

**Materials**

- Your design READMEs

- [ ] Write the final README with architecture diagram, approach, results, and bug log.
- [ ] Put the project first on your resume.
- [ ] Practice a 2-minute and a 20-minute explanation out loud.

### Done when

- Trace comparison against Spike runs automatically.
- Random programs from riscv-dv run through the comparison.
- Coverage closure and bug injection results are published.

## Module 7: Your own projects

*Summer 2027 onward*

Take a design from your own idea to a verified, documented result, with no plan telling you what to build.

### 7.1 Choose and specify a project

A project teaches design when you make the decisions a tutorial would have made for you.

**Materials**

- Your core, UART, FIFOs, and APB block as building blocks
- [ZipCPU blog](https://zipcpu.com/), for how one engineer plans and verifies his own designs

- [ ] List five project ideas and write the hardest part of each in one sentence. Candidates that build on this plan: instruction and data caches for your core, a branch predictor, an AXI4-Lite interconnect, a small accelerator such as a matrix-multiply unit on your core's bus, or an SPI or I²C controller for a Pmod module.
- [ ] Pick one you can finish in four to eight weeks. Write a spec: what it does, its interfaces, and what is out of scope.
- [ ] Write a microarchitecture document with a block diagram, every major register, and every FSM before writing any RTL.
- [ ] **Document:** put the spec and microarchitecture document in the design's README.

### 7.2 Build and verify it

On your own project nobody hands you a test plan, so you write one before the RTL.

**Materials**

- Your module 2 and 3 testbenches as templates

- [ ] Write the verification plan from the spec: features, checks, stimulus, and coverage.
- [ ] Build the RTL one block at a time, and give each block a self-checking unit testbench before integrating it.
- [ ] Write a top-level testbench with a reference model, constrained-random stimulus, assertions, and functional coverage.
- [ ] Prove the one or two properties that matter most with SymbiYosys.
- [ ] Inject five bugs and record which check caught each.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### 7.3 Bring up and review

Finishing and explaining a design is the skill that carries into the next one.

**Materials**

- Digilent Arty A7 reference
- Vivado timing reports

- [ ] Synthesize, record resource use and maximum frequency, and fix the critical path if it misses timing.
- [ ] **Hardware:** Run the design on the Arty A7. Record every bug that appeared only on hardware.
- [ ] Write the final README: design, verification approach, results, bug log, and what you would change.
- [ ] Start the next project, larger than this one.
- [ ] **Document:** commit this section's designs to their folders and update each README and status.

### Done when

- One design went from your own idea to a verified, documented result.
- You can explain every block and every check in it without notes.
