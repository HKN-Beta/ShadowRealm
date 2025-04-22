# ECE 27000 - Finite State Machines

## Overview
In general, Finite State Machines are a mathematical tool that can be used to represent any system that will be shifting through multiple states or phases. They could be used for game design, to represent the different states of a game (in a level, menu, win condition, etc), or for lexical processors to identify whether an input is valid or not.

 - **Motivation:**
    Pure combinational logic can be very useful for specific applications - anything that simply needs to convert an array of instantaneous inputs into a corresponding output can be made of pure combinational logic. There are many applications, however, which cannot run on pure combinational logic. A very simple example might be a digital lock, where we need to detect that a sequence of inputs were pressed in the correct order, and not just that all of the input were pressed simultaneously. A broader example would include all sorts of serial communication protocol interfaces - we need some way to detect the setup, data, and end from a data packet, and ensure that they were all sent in the correct order and format. This cannot be done with combinational logic, as we may be receiving many bytes of data over a singular wire.

## Key Concepts & Definitions
- **Finite State Machine:** In the domain of digital logic design, a finite state machine is a constructed piece of sequential logic that will convert a sequence of inputs into outputs. Finite state machines are more versatile than standard combinational logic, as FSMs have the ability to operate over a sequence of inputs, rather than the instantaneous input that combinational logic uses.
- **Moore Machine:** A classification of finite state machines that determine outputs based solely on the current state of the machine.
- **Mealy Machine:** A classification of finite state machines that determine outputs based on a combination of current state and current inputs to the machine.

## Theory 
Finite State Machines are used to represent sequential logic in digital circuit design. In previous engineering classes, you may have worked with flowcharts to understand how a process works, or how a program should function. While these work at a high level for sequential logic design, we frequently need an even more detailed mechanism to design our sequential logic.
Thus, instead of using flowcharts for complete design of digital logic, we have FSMs, which use **current inputs** to update the **next state** of the machine, and then use some combination of **current inputs** and **current state** to create the **outputs** of the machine. This process is shown in a small RTL diagram below.

![Basic RTL Diagram of a Finite State Machine](assets/FSM_RTL.png)

### Moore vs. Mealy
There are two main types of FSM, Moore and Mealy. The fundamental difference between Moore and Mealy state machines is how the outputs of the state machine are determined.

In a **Moore** state machine, outputs are determined solely by the current state of the FSM. In a **Mealy** machine, outputs are determined by a combination of the current state of the FSM and the current inputs to the FSM.
When FSMs are used as a theoretical/mathematical tool, there is no specific benefit to using one type over the other. In practical use, however, Moore state machines are typically preferred, as slight noise on the input won't cause noise on the output.

### Application
#### Example Moore Machine - 101 Sequence Detector

![Moore 101 Sequence Detector](assets/Moore101SeqDet.png)

#### Example Mealy Machine - 101 Sequence Detector

![ealy 101 Sequence Detector](assets/Mealy101SeqDet.png)

As you can see from the two different FSM diagrams, the Moore machine has its outputs defined within the states themselves, while the Mealy machine has its outputs defined on transition edges.
Both of these FSMs do perform the same function, however, which can be seen by taking an example sequence and tracing through the FSM states. For example, with the example sequence 101, which we know should be detected, both state machines will start in S0, and then progress straight through from S1, to S2, to S3, where the output will be a 1. For an example of 100, however, both state machines will start in S0, move to S1, S2, and then back to S0, as they have both failed to detect a 101 in the input sequence.

While detecting a 101 in a sequence of serial input may not seem like the most exciting thing to use an FSM for, it is a very practical problem, as many types of serial communication protocols will identify the beginning of a data packet with a specific sequence of bits, and receivers for that type of data will need to be able to detect that initial sequence.

#### Example SystemVerilog
```
typedef enum {S0, S1, S2, S3} state_t;

module moore_101_det(
  input logic clk, rst, in,
  output logic out
);

  state_t curr_state, next_state;

  always_comb begin : NEXT_STATE_LOGIC
    case(curr_state)
      S0: next_state = in ? S1 : S0;
      S1: next_state = in ? S1 : S2;
      S2: next_state = in ? S3 : S0;
      S3: next_state = in ? S1 : S2;
    endcase
  end

  //output logic
  assign out = (curr_state == S3);

  always_ff @(posedge clk, posedge rst) begin
    if(rst) curr_state <= S0;
    else curr_state <= next_state;
  end

endmodule
```

### Example Exercises
- Using the above examples, design Moore and Mealy FSMs to detect the sequence 100101. (This will require more states than the examples, but is conceptually similar)
- Edit the example SystemVerilog for a Moore 101 sequence detector to instead reflect a Mealy 101 sequence detector.
- Write SystemVerilog for a 100101 sequence detector based on the FSMs designed in the first example.
