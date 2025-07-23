# 🚦 Traffic Light Controller using FSM (Verilog)

This project implements a Finite State Machine (FSM)-based traffic light controller using Verilog. It prioritizes highway traffic and only allows country way traffic when vehicles are detected.

# Essence of the Project
I have implemented a (FSM)-based Traffic Light Controller for a road system with:

➤Highway road

➤Country way (crossroad or less priority road)

The traffic controller:

➤Gives priority to the Highway

➤Changes lights to Country way only when a vehicle is detected (x = 1) on that road

➤Manages timing for light transitions (GREEN → YELLOW → RED) with internal counters

## 🔁  State Transitions
Handled via always block triggered on clock and reset (clr):

`s0` → `s1`: When x == 1 (vehicle on country road)

`s1` → `s2`: After 3 clock cycles (timer)

`s2` → `s3`: After 2 clock cycles

`s3` → `s4`: When x == 0 (no more vehicles)

`s4` → `s0`: After 3 clock cycles

I have used a 4-bit timer counter to delay transitions where needed.

##  State Descriptions

| State | Highway Light | Country Road Light | Description |
|-------|---------------|--------------------|-------------|
| s0    | Green         | Red                | Default state |
| s1    | Yellow        | Red                | Transition to stop highway |
| s2    | Red           | Red                | All stop (transitional) |
| s3    | Red           | Green              | Allow country road |
| s4    | Red           | Yellow             | Prepare to stop country |


## 💡  Light Encoding
Using 2-bit values:

00 – RED 🔴

01 – YELLOW 🟡

10 – GREEN 🟢

## ⏳ Delay Mechanism

Delays are implemented using a **4-bit timer register**, incremented on every clock cycle.

| Transition Type           | FSM State | Duration (Clock Cycles) | Purpose                                      |
|---------------------------|-----------|--------------------------|----------------------------------------------|
| Highway Yellow → Red (Y2R)     | `s1`      | 3                        | Time to stop highway before going RED        |
| Red → Country Green (R2G) | `s2`      | 2                        | Safety transition where both roads are RED   |
| Country Yellow → Red (Y2R)     | `s4`      | 3                        | Time to stop country traffic                 |

## Testbench Behavior
Simulates real traffic conditions:

- Initially no vehicles (x = 0)

- Vehicle arrives at country road (x = 1)

- Waits, then vehicle leaves (x = 0)

- Another vehicle arrives again
## ✅ Observations:
- FSM correctly responds to vehicle presence (x = 1).

- Delays between states are respected:

      Yellow lights → 3 clock cycles

      All-red state → 2 clock cycles

- Highway has default priority, and control is only transferred when needed.

(Check out the Block diagram,FSM diagram and Simulation waveforms in the `.zip`file along with codes)
