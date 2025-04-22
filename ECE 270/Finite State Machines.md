# Finite State Machines
## Basic Setup
Finite State Machines are used to represent sequential logic in digital circuit design. In previous engineering classes, you may have worked with flowcharts to understand how a process works, or how a program should function. While these work at a high level for sequential logic design, we frequently need an even more detailed mechanism to design our sequential logic.
Thus, instead of using flowcharts for complete design of digital logic, we have FSMs, which use **current inputs** to update the **next state** of the machine, and then use some combination of **current inputs** and **current state** to create the **outputs** of the machine. This process is shown in a small RTL diagram below.



## Moore vs. Mealy
There are two main types of FSM, Moore and Mealy. The fundamental difference between Moore and Mealy state machines is how the outputs of the state machine are determined.

In a **Moore** state machine, outputs are determined solely by the current state of the FSM. In a **Mealy** machine, outputs are determined by a combination of the current state of the FSM and the current inputs to the FSM.
When FSMs are used as a theoretical/mathematical tool, there is no specific benefit to using one type over the other. In practical use, however, Moore state machines are typically preferred, as slight noise on the input won't cause noise on the output.

### Example Moore Machine - 101 Sequence Detector

![Moore 101 Sequence Detector](assets/Moore101SeqDet.png)

### Example Mealy Machine - 101 Sequence Detector

![ealy 101 Sequence Detector](assets/Mealy101SeqDet.png)

As you can see from the two different FSM diagrams, the Moore machine has its outputs defined within the states themselves, while the Mealy machine has its outputs defined on transition edges.
