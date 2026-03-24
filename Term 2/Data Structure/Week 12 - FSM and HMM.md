# Finite State Machines
Finite-state machines (FSMs) model many computational processes.
An FSM is a reactive system whose response to a particular stimulus varies according to its current 'state'.
FSM typically model stems with a finite number of states and transitions between them. They can be implemented in hardware or software.
![[Pasted image 20260324133642.png]]
## Applications of FSM
- Vending Machines
- Traffic Lights
- Elevators
- Alarm Clock
- Microwave
- Cash Registers
## Formal Definition
A FSM is defined as a **sextuple**:
$$
M= (S,I,f,g,S_0)
$$
S = Set of states
I = Input alphabet
O = Output alphabet
f : S * I -> S (transition function)
g : S * I -> (output function)
$s_0$ = Initial state

Usual finite state machines are represented by a state diagram. A state diagram consist of:
- State nodes: Represents States.
- Transition Arrow: Represent states transitions.
- Input/Output Label: Show input/output for transitions.
## Common Examples
### 8-Puzzle
![[Pasted image 20260324134001.png]]

**Reachability**
A state $s_i \in S$ is reachable if there exists some execution (sequence of state transitions) from the initial state $s_0$ that reaches $s_i$
### Vending Machine
A vending machine accepts nickels (5 cents), dimes (10 cents), and quarters (25 cents). When a total of 30 cents or more have been deposited, the machine immediately returns the amount in excess of 30 cents. When 30 cents has been deposited and any excess refunded, the customer can push an orange button and receive an orange juice or push a red button and receive an apple juice.

If you were to implement this in code, you would probably find that it would get a bit complex and buggy. But the FSM model gives a structured way to think about the problem:
1. States: ${s_1,s_2,S_3,s_4,s_5,s_6}$ ($s_i$ is the state where the machine has collected 5i cents)
2. Inputs: {Nickle, dimes, quarter, orange ,red}
3. Outputs: {return, orange juice, apple juice}
![[Pasted image 20260324134423.png]]

![[Pasted image 20260324134438.png]]

### Summary
Although the concept behind FSMs is simple, they can be used to model complex systems. They are useful abstraction for understanding and designing systems that have a finite number of states and transitions between them. They can be used for highly non-trivial tasks. We have not explored it, but they can be particularly useful when designing a language with a specific grammar. Compiler theory makes use of FSMs to parse code.

# Hidden Markov Models
FSMs appear simplistic but they are useful abstraction which we an extend to more complex models. One such model is the **Hidden Markov Model** (HMM)

A **hidden markov model** is a similar to a finite state machine in that it has a set of states, transitions between states, and outputs. However, the state of the system is not directly observable. By this, we mean that in certain system we might not know the exact state. For example, imagine we want to model a robot's positions. If the input is 'move ahead by 1m', the robot will activate its motors to move forward. However, depending on a variety of factors (e.g. friction, battery level, etc.), the robot might move 0.9m or 1.1 . So we don't know exactly what the new state will be.
## The Markov Assumption
To understand HMMs, we need to first need to understand the Markov Assumption and Markov Chains.

**Markov Assumption**
The Markov Assumption states that the future state of a system depends only on the current state and not on the sequence of events that preceded it:
$$
	P(X_{t+1}|X_{t},X_{t-1},\dots,X_1) = P(X_{t+1}|X_t)
$$

I.e. it doesn't matter how the robot got to its current position. The future state only depends on the current battery level, friction, etc.

## Markov Chains
A Markov Chain is a sequence of random variables $X_1,X_2,\dots,X_n$ where the probability of each variable depends only on the previous variable.

A Markov Chain is defined by the following properties:
- **State space**: A finite set of states $S =\{s_1,s_2,\dots,s_n\}$ 
- **Initial State Distribution**: The probability of starting in each state $s_i$.
- **Transition Probabilities**: The probability of moving from the state $s_i$ to state $s_j: P(X_{t+1} = s_j|X_t=s_i$).
### Representing Markov Chains
A Markov Chain can be represented as a directed graph where the nodes represent states and the edge represent transitions between states. The edges are labelled with the transition probabilities. 
![[Pasted image 20260324135551.png]]

### Using Markov Chains to Write Text
>Can we use Markov Chains to generate text. The idea is that we can model the probability of a word appearing after another word by simply recording relative frequencies.
### Predicting the Future using Markov Chains
>Assume that:
80% of the sons of Harvard men went to Harvard and the rest went to Yale
40% of the sons of Yale went to Yale and the rest of Yale sons were split evenly between Harvard and Darmouth
70% of the sons of Dartmouth men went to Dartmouth, 20% went to Harvard, and the remaining 10% went to Yale

**Question**:Find the probability that he grandson of a man from Harvard went to Harvard.

We can easily compute the answer analytically. The keye is to define the **transition matrix**, which says how  this systems evolves from one state to another (i.e. the i,j entry represents the probability P($X_{t+1} = s_j|X_t = s_i$)).
There are 3 states, Harvard, Dartmouth, Yale. The Transition matrix is applied to the initial state to get the next state (i.e. the proportion of children going to each school). Applying the transition matrix a second time will give the proportion of grandchildren going to each school.
$$P=\begin{bmatrix}
0.8 & 0 & 0.2\\
0.2 & 0.7 & 0.1\\
0.3 & 0.3 & 0.4
\end{bmatrix}
$$

The resulting matrix, $P^2$, gives the proportion of grandchildren going to each school:
$$
P^2 = \begin{bmatrix}
.7&.06&.24\\.33&.52&.15\\.42&.33&.25
\end{bmatrix}
$$

### Modeling Temporal Process with Markov Chains
Markov Chains can be particularly useful for modeling *temporal* processes
(i.e. processes that evolve over time).
![[Pasted image 20260324140901.png]]
## Hidden Markov Models
Hidden Markov Models (HMMs) are an extension of Markov Chains. They are used to model systems where the state of the system is not directly observable.

An HMM is defined by the following components:
- **States**: A set of states $S = \{s_1,s_2,\dots,s_n\}$
- **Observations**: A set of observations $O = \{o_1,o_2,\dots,o_m\}$
- **Transitions Probabilities**: The probability of moving from state $s_i$ to state $s_i$.
- **Emission Probabilities:** The probability of observing $o_k$ given that the system is in the state $s_i$

We can still represent a HMM graphically, but now we have two types of nodes: states and observations. The edges represent transitions between states and the emission/observation probabilities (here we denote using y(t))
![[Pasted image 20260324141307.png]]

The key thing to note here is that we never know the *true* state of the system since it's assumed we can't measure that exactly. But we can make an educated guess based on the observations.
## HMM Example
### Umbrella World Example
>You are the security guard stationed at a secret underground installation. you want to know whether it's raining today, but your only access to the outside wolf occurs each morning when you see the director coming in with, or without, an umbrella. For each day `t`, the set $O_t$ thus contains a single observation/evidence variable $Umbrella_t$ or $U_t$ for short (whether the umbrella appears), and the set $X_t$ contains a single state variable $Rain_t$ or $R_t$ for short (whether it is raining).

Note that there are many real-world examples of this , for example estimating blood sugar levels in diabetic patients using heart rate, blood pressure, etc.
![[Pasted image 20260324141632.png]]
Sensor Model:
$$
	P(U_t|R_t,R_{t-1},\dots,R_1,U_{t-1},U_{t-2},\dots,U_{1}) = P(U_t|R_{t})
$$
Transition Model:
$$
P(R_t|R_{t-1},R_{t-1},R_{1}) = P(R_t|R_{t-1})
$$

Given this set-up, we can now answer many question about the system since we can easily calculate the joint distribution:
$$
P(X_{0:t},E_{1:t}) = P(X_0)\prod_{i=1}^{t}P(X_i|X_{i-1})P(E_i|X_i)
$$

In general, to calculate a joint probability distribution for n discrete random variables with m states each, we need to store $m^n$ values. This is known as the curse of dimensionality. The HMM model is a way to reduce this complexity.

>Given the sequence \[true, true, false, true, true] for the guard's first five days, what is the most likely weather sequence? Does the absence of an umbrella on day 3 mean it wasn't raining, or did the director forget it? If it stayed dry, day 4 might also be dry due to weather persistence, with the director brining an umbrella just in case. With 25 possible weather sequences, can we find the most likely one without checking them all?

### Other Questions that HMMs can Answer
HMMs can answer a variety of other questions about the process it models, such as:
1. What is the probability of the current state, given all previous evidence $(P(X_k|E_{1:t}))$ (aka the smoothing problem)?
2. What is the likelihood for the evidence sequence $(P(E_{1:t}))$? (Useful for comparing models)
3. What is the probability of future states, given all evidence up to the present $P(X_{t+k+1}|E_{1:t})$ (aka the prediction problem)?
# Summary
Hidden Markov Models are a powerful extension of Markov Chains that allow us to model systems where the state of the system is not directly observable.