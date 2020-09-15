---
layout: post
title: Notes on Computer Architecture
comment: true

---

## Introduction 

Computer architecture is about designing a computer that is well suited for its purpose. For e.g. desktop computer, laptops, mobile phones etc. have different applications due to which they require a different design approach. The aim of computer architects is to:
1. Improve performance - Speed, Battery, Life, Size, Weight, Energy efficiency etc.
2. Improve capabilities - 3D graphics rendering, Debugging Support, Security etc.

A computer design involves anticipation of technology trends for design of futuristic computers. If you do design a computer with current technology without any anticipation of technology trends, the computer might become obsolete by the time the design is complete. For e.g. if the trend dictates speed of computers increasing by 10% each year, the designers must accommodate the advancement in their designs.

One of the most famous technology trends has been **Moore's law**. Moore's law states that every 18-24 months, we will be able to fit twice the number of transistors in the same chip area. For computer architects, this simply translates into following meanings:
1. Doubling the processing speed or instructions per second
2. Reducing energy consumption by half (due to reduced size of transistors)
3. Doubling the memory capacity in case of a memory chip

In this way the Moore's law serves as a guiding light illuminating what the technology is expected to do and what architects might be able to achieve with that technology. There are speculations that Moore's law is coming to an end. This [article](http://www.extremetech.com/computing/165331-intels-former-chief-architect-moores-law-will-be-dead-within-a-decade) provides a discussion on the same.

### Memory Wall

As we said, instruction/sec and memory capacity would 2x every two years. But it has been observed that the memory latency (time taken to do a memory operation) is increasing by only 1.1x every two years. Over the time as processor gets more faster that the memory, this gap widens. As processors have to access memory for operations a slow memory often limits the speed. This is known as the **Memory wall**. Modern computers use cache which is faster memory to counter this. More on this later.

### Processor

A processor broadly has 3 constraints i.e. speed, cost and power. A job of a computer architect is to figure out the value of each of these constraints for a specific use. For e.g. a mobile phone processor can have a decent speed and should be affordable but it should not consume high power which can reduce battery life of the device.

**Power Consumption** of a processor is one of the important parameters. There are two types of power consumed by a processor:

1. Dynamic Power: This is power consumed by an active circuit and is given by the following expression.

$$
\begin{align*}
  & P = 1/2* C * V^2* f* \alpha\\
\end{align*}
$$

where, $$C$$ is the capacitance of the circuit, $$V$$ is voltage of the power supply, $$f$$ is the clock frequency and $$\alpha$$ is the activity factor which is indicative of fraction of transistors active in a given clock cycle. 

2. Static Power: This is power consumed when processor is powered on but idle. We can think our transistor to be water taps with voltage being the control knob. If voltage is reduce some water leaks out of the tap. This is leaked power.

Cost of processor depends on the fabrication process. The fabrication process involves preparation of chips on a circular semiconductor wafer. Out of all fabrication chips, some are defective which reduces the **fabrication yield** and thus increases the overall cost per chip. The yield can vary due to defects in the wafer or defect in manufacturing process.


## Metrics and Evaluation

Before we learn how to make better computers, we need to know what 'better' actually means and how to measure it.

### Performance

When we talk about performance of a computer, we generally think about speed. Yet there are two aspect of performance:
1. Latency: time taken to finish something started.
2. Throughput: number of instructions per second.

It is thought that throughput is 1/(latency). However, this is not true always the case. Usually a computer may do several other tasks along a given task which makes latency and throughput different.

Now that we know how to measure the performance of a system, we want something to compare it. Something using which we can say-- *'X is N times faster than Y'*. This is known as **Speedup (N)**.

$$
\begin{align*}
  & N = \frac{Speed(X)}{Speed(Y)}= \frac{Latency(Y)}{Latency(X)}= \frac{Throughput(X)}{Throughput(Y)}\\
\end{align*}
$$

Speedup(N) > 1 signifies improved performance, while a value < 1 outlines degraded performance than before.

Further, to measure these values for each computer some standard workloads i.e. programs and inputs are used that everyone has agreed upon. These standard workloads are known as **Benchmarks**. Benchmarks can be of following type:
1. Real applications such a video rendering software etc. (most difficult to set up)
2. Kernels 
3. Synthetic Benchmarks (behavior similar to kernels but easy to compile)
4. Peak performance (good for marketing)

Some benchmark standards in the industry are TPC, EEMBC, SPEC etc.

### Iron Law of Performance

CPU time= Number of instructions in the program x Cycles per instruction x Clock cycle time. 

Here, number of instructions generally depend of efficiency of the compiler and the instruction set designed for the processor. Cycles per instruction again depends on the instruction and processor design. The clock cycle time depends upon processor/circuit design and transistor physics.

### AMDAHL's Law

This law is used to calculate speed up of the entire program when we apply speed up only to portion of the program. The overall speed up is given as:

$$
\begin{align*}
  & Speedup_{overall} = \frac{1}{(1-Frac_{enhanced})+(\frac{Frac_{enhanced}}{Speedup_{enhanced}})}\\
\end{align*}
$$

where, $$Frac_{enhanced}$$ is the portion of program that was improved. It is the fraction of original *execution time* affected by the enhancement. The $$Speedup_{enhanced}$$ is the improvement done to a portion of the program.

The implication of this law can be seen by considering these two following examples:
#### Scenario 1:
Let's say we have a speed up of 20 for 10% of the execution time. The overall speedup would be:

$$
\begin{align*}
  & Speedup_{overall} = \frac{1}{(1-0.1)+(\frac{0.1}{20})}= 1.105\\
\end{align*}
$$

#### Scenario 2:
Let's say we have a speed up of 1.6 for 80% of the execution time. The overall speedup would be:

$$
\begin{align*}
  & Speedup_{overall} = \frac{1}{(1-0.8)+(\frac{0.8}{1.6})}= 1.43\\
\end{align*}
$$

As evident from above scenarios, small speedup for most common tasks results in significant overall speedup. Even if we do infinite speedup for scenario 1, the overall speedup will be less that scenario 2. Hence, one should focus of boosting the speed of most common tasks and should not focus on stuff that consumes very less of our execution time.

Another famous law jokingly known as LHADMA's law (AMDAHL in reverse) states that although you should focus on making the most common case fast, you should also not mess up the uncommon cases to badly. Let's see this below:

#### Scenario 3:
Let's say we have a speed up of 2 for 90% of the execution time but also a slow down of 10x for 10% of the execution time. The overall speedup would be:

$$
\begin{align*}
  & Speedup_{overall} = \frac{1}{(\frac{0.1}{0.1})+(\frac{0.9}{2})}= 0.68\\
\end{align*}
$$

Here, we see that even if there is speed up for 90% of the execution the, the slow down has resulted in an overall slowdown.

### Pipelining

A processor performs various operation in a sequential manner. The operations can be broadly listed as:
1. Fetch the instruction from the memory.
2. Decode the instruction.
3. Execute the instruction.
4. Store the result back in memory.

In a pipeline once an instruction moves from fetch to decode step, another instruction is fetched. Similarly, when an instruction moves to execute step, fetched instruction moves to decode state and so on. This makes possible for pipelining to ideally achieve 1 cycle per instruction (CPI) ones the first instruction completes the step. This is similar to having an assembly line of car.

However, CPI in not '1' due to following reasons:
1. There are initial steps involved (though as number of instructions increase these initial steps become negligible).
2. Pipeline stalls: Sometime one of the steps in the pipeline might take longer than expected. This can happen in instances where an instruction needs to read a register which may have right values at some point later. This delay increases the CPI.
3. Pipeline flushes: In case of branch and Jump instructions, by the time instruction is decoded, subsequent instructions are already fetched. But due to the fact that a jump instruction altogether leads to a different address with different instructions, previous instructions in fetch and decode needs to be flushed by the processor.

Broadly, **hazards** occur in a pipeline when there is a dependency that can cause operation to be executed with wrong values.
In case the CPU detects a hazard situation it can:
1. Flush dependent instruction (useful in case of control dependencies like jump instruction)
2. Stall dependent instruction (useful in case of data dependencies where we need to wait for the right values to be loaded)
3. Fix values read by dependent instruction

One area to ponder can be the number of stages a pipeline should have. From above discussion for it is evident that the ideal scenario has $$CPI=1$$. If the pipeline has many stages, more instruction needs to be stalled/flushed in case of hazards which can significantly increase the CPI. But a deeper pipeline can also reduce work being done at each stage i.e. the cycle time reduces. As we have seen in iron law which states *CPU time= Number of instructions in the program x Cycles per instruction x Clock cycle time*. This can further enable architects to have high clock frequency. Hence, the graph of execution time vs #no. of stages will be a 'U-shaped' curve. So, for optimal performance, modern processors can have a pipeline which is 30-40 stages deep. But, we also need to consider power. In case of reduced cycle time, we have more pipeline latches consuming energy holding temporary results. Hence, power consumption linearly increases with no. of stages. If we take both performance and power we end up having 10-15 stages in modern processors.