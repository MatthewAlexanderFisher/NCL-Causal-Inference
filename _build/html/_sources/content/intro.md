# Causal Inference

These notes are an exposition of Causal inference. In particular, we focus on the two main approaches:

1. Pearl's Structural Equation Framework
2. Rubin Causal Models (Potential Outcomes Framework)

## Background on Causal Inference

### What is Causality?

There are two broad philosophical approaches.

1. *Counterfactual Definition:* Causation as counterfactual statements ``If $X$ had not occurred, $Y$ would not have occurred.
    - Originates with Hume (1748). Fully synthesised by David Lewis (1973).
    - Conditional Causal effect
    - Potential Outcome Framework
    - Structural Equation Framework
2. *Interventionist Definition:* An event $X$ causes another event $Y$ if an intervention that changes $X$ also changes $Y$.
    - Originates with James Woodward (2003) and Judea Pearl (2000).
    - Conditional Causal Effect
    - Structural Equation Framework

### Population Level vs. Individual Level Causality

1. *Population Level Causality:* General trends and average effects across a group or population.
    - Uses statistical methods to infer causal relationships from group data.
    - Often used in epidemiology and social sciences.
    - Challenges include heterogeneity of treatment effects.
2. *Individual-Level Causation:* Concerns specific causal relationships for individuals.
    - Involves deterministic or probabilistic predictions about individual outcomes.
    - Relevant in clinical decision-making and personalised medicine.
    - Challenges include data limitations and complexity of individual variability.

Causal Inference *usually* deals with population level causation.

### Towards a Definition of counterfactual Causal Inference

Let's start with a bad definition of Counterfactual Causality

```{prf:definition}
:label: bad-causal-def

 An event $A$ is said to *cause* event $B$ if and only if $\text{Pr}(B|A)$ is *large* and $\text{Pr}(B|A^c)$ is *small*.

```

For example, if I push an object, it moves; if I don't push the object, it remains stationary.

This simple example makes this approach seem plausible.

- Counterexample:  When ice cream sales are high, drowning incidents are also high. Conversely, when ice cream sales are low, drowning incidents are low.

By our bad definition, ice cream sales cause drowning. We are confusing correlation (or dependence) with causality.

```{prf:definition}
:label: better-causal-def

An event $A$ is said to cause event $B$ if, after controlling for a set of confounders $\underline{X}$, $\text{Pr}(B|A, \underline{X})$ differs significantly $\text{Pr}(B|A^c, \underline{X})$.

```

- Counter Example Revisited: When ice cream sales are high (event $A$), drowning incidents (event $B$) are also high. Conversely, when ice cream sales are low, drowning incidents are low.

- Identifying Confounders: In the counter example, we can identify $\underline{X}$ as the temperature.

A true cause is temperature. High temperatures lead to more swimming activities, thereby increasing the probability of drowning incidents.

