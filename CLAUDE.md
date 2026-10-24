# hardware-projects

My RTL design and verification portfolio. I'm a first-year ECE student learning SystemVerilog, testbenches, and formal verification by working through the plan in @docs/plan.md.

## Repo rules

- The repo holds only designs I build. HDLBits solutions, readings, and small language or tool demos stay out.
- One folder per design, named in lowercase with hyphens (`sync-fifo`, `carry-lookahead-adder`). Planned designs may already have placeholder folders.
- Inside each design folder:
  - `rtl/`: synthesizable SystemVerilog (`.sv`)
  - `tb/`: testbenches, assertions, and formal properties
  - `images/`: only waveforms or schematics that show a bug or a result
  - `README.md`: starts with a status line; covers what the design does, its inputs and outputs, and verification (reference model, what the testbench covers, how to run it, bugs injected and which check caught each, bugs I hit while building)
- When I finish or change a design, update its README status and the matching row in the top-level README.
- When a later plan section extends an existing design, edit that design's folder instead of making a new one.
- Delete `.gitkeep` from a folder once it has real files.

## Tools

- Local: Icarus Verilog, Verilator (`verilator --lint-only -Wall` for lint), SymbiYosys for formal, Surfer or GTKWave for waveforms.
- Vivado Standard for the Digilent Arty A7.

## How to help me

- I'm learning. Do not write RTL or testbench code for me unless I ask for it explicitly.
- Do: review my code, find bugs, explain simulator and lint errors, run simulations and lint, and explain what a waveform shows.
- When you find a bug, point to where it is and explain why it's wrong before suggesting a fix.
- Explain from first principles, define new terms, and keep answers short.
- Before suggesting a commit, tell me what changed.
