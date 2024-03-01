# Graphical Models

## Directed Acyclic Graphs (DAG)

```{prf:definition}
:label: dag

A *Directed Acyclic Graph (DAG)* is a finite directed graph with no directed cycles. We denote the graph as $G = (V, E)$, where $V$ are the nodes (or vertices) and $E$ are the directed edges.

```

### DAG Example

```{tikz}
:xscale: 50

\usetikzlibrary{arrows.meta, positioning, shapes, backgrounds}

\definecolor{darkred}{RGB}{160,0,0}
\definecolor{darkblue}{RGB}{7, 90, 224}
\definecolor{nicegreen}{RGB}{43, 194, 88}
\definecolor{niceorange}{RGB}{255, 221, 0}

\definecolor{mediumgray}{RGB}{120,120,120}

\tikzset{arrow/.style={
    -{Latex[length=3mm, width=2mm]}, % Arrow tip configuration
    line width=0.4mm, % Arrow line width
    draw=mediumgray, % Use the medium gray color for the arrow
}}

\begin{tikzpicture}[node distance=0.7cm and 1.5cm, 
                    mynode/.style={circle, draw=none, minimum size=1cm,outer sep=1pt, font=\sffamily}]
    \node[mynode,shape=circle, fill=darkblue!40!white] (A) at (0,0) {A};
    \node[mynode,shape=circle, fill=darkblue!40!white] (B) at (2,0) {B};
    \node[mynode,shape=circle, fill=darkblue!40!white] (C) at (4,0) {C};
    \node[mynode,shape=circle, fill=darkblue!40!white] (D) at (2,-2) {D};

    \draw[arrow] (A) -- (B);
    \draw[arrow] (B) -- (C);
    \draw[arrow] (A) -- (D);
    \draw[arrow] (D) -- (C);
\end{tikzpicture}

```

It consists of finitely many nodes and edges, with each edge directed from one node to another, such that there is no way to start at any node $v$ and follow a consistently-directed sequence of edges that eventually loops back to $v$ again.

## Bayesian Network

```{prf:definition}
:label: bayesian-network

A *Bayesian network* is a DAG with dependence semantics.

- Each *node* represents a *random variable*.
- Each *edge* encodes *probabilistic dependencies* between each random variable.

If a random variable $Y$ is connected to $X$ by a directed edge ($Y\rightarrow X$), then $X$ is *conditionally dependent* on $Y$. That is,

$$ \text{Pr}(X \in S \,|\, Y\in A) \neq \text{Pr}(X\in S) $$

```

Bayesian networks are helpful as both a cognitive and computation tool.

### Parents and Descendants

- *Parents:* The *parents* $\text{Pa}(X)$ of a node $X$ in a Bayesian network are the nodes that have a direct edge leading to the node. They represent the direct influencers of the node.
- *Descendants:* The *descendants* $\text{De}(X)$ of a node $X$ are all nodes that can be reached by following directed edges starting from the node. They represent all nodes directly or indirectly influenced by the node.

`<a id="tikz:pd_ex1"></a>`

```{tikz}
:xscale: 50

\usetikzlibrary{arrows.meta, positioning, shapes, backgrounds}


\definecolor{darkred}{RGB}{160,0,0}
\definecolor{darkblue}{RGB}{7, 90, 224}
\definecolor{nicegreen}{RGB}{43, 194, 88}
\definecolor{niceorange}{RGB}{255, 221, 0}

\definecolor{InvisibleRed}{rgb}{0.97, 0.92, 0.92}
\definecolor{InvisibleGreen}{rgb}{0.92, 0.97, 0.92}
\definecolor{InvisibleBlue}{rgb}{0.92, 0.92, 0.97}

\definecolor{MediumRed}{rgb}{0.925, 0.345, 0.345}
\definecolor{MediumGreen}{rgb}{0.37, 0.7, 0.66}
\definecolor{MediumBlue}{rgb}{0.015, 0.315, 0.45}

\definecolor{mediumgray}{RGB}{120,120,120}

\tikzset{arrow/.style={
    -{Latex[length=3mm, width=2mm]}, % Arrow tip configuration
    line width=0.4mm, % Arrow line width
    draw=mediumgray, % Use the medium gray color for the arrow
}}



\begin{tikzpicture}[node distance=0.7cm and 1.5cm, 
                    mynode/.style={circle, draw=none, minimum size=1cm,outer sep=1pt, font=\sffamily}]

    % Nodes
    \node[mynode, shape=circle, fill=MediumRed!40!white] (A) {A};
    \node[mynode, below right=of A, shape=circle,draw=darkblue!70!white,
    line width = 0.7mm, fill=darkblue!40!white] (D) {D};
    \node[mynode, above right=of D, shape=circle, fill=MediumRed!40!white] (B) {B};
    \node[mynode, below left=of D, shape=circle, fill=MediumRed!40!white] (C) {C};
    \node[mynode, below right=of D, shape=circle, fill=darkblue!40!white] (E) {E};

    % Edges
    \draw[arrow] (A) -- (D);
    \draw[arrow] (B) -- (D);
    \draw[arrow] (C) -- (D);
    \draw[arrow] (D) -- (E);
\end{tikzpicture}

```

In [Figure 2](#tikz:pd_ex1), nodes $A$, $B$ and $C$ are parents of node $D$ and node $E$ is a descendant of node $D$.

### Conditional independence in Bayesian Networks

A node in a Bayesian netowrk is *conditionally independent* of its non-descendants given its parents nodes.

`<a id="tikz:cond_independence"></a>`

```{tikz}
:xscale: 50

\usetikzlibrary{arrows.meta, positioning, shapes, backgrounds}

\definecolor{darkred}{RGB}{160,0,0}
\definecolor{darkblue}{RGB}{7, 90, 224}
\definecolor{nicegreen}{RGB}{43, 194, 88}
\definecolor{niceorange}{RGB}{255, 221, 0}

\definecolor{InvisibleRed}{rgb}{0.97, 0.92, 0.92}
\definecolor{InvisibleGreen}{rgb}{0.92, 0.97, 0.92}
\definecolor{InvisibleBlue}{rgb}{0.92, 0.92, 0.97}

\definecolor{MediumRed}{rgb}{0.925, 0.345, 0.345}
\definecolor{MediumGreen}{rgb}{0.37, 0.7, 0.66}
\definecolor{MediumBlue}{rgb}{0.015, 0.315, 0.45}

\definecolor{mediumgray}{RGB}{120,120,120}

\tikzset{arrow/.style={
    -{Latex[length=3mm, width=2mm]}, % Arrow tip configuration
    line width=0.4mm, % Arrow line width
    draw=mediumgray, % Use the medium gray color for the arrow
}}


\begin{tikzpicture}[node distance=0.7cm and 1.5cm, 
                    mynode/.style={circle, draw=none, minimum size=1cm,outer sep=1pt, font=\sffamily}]

    % Nodes
    \node[mynode, shape=circle, fill=niceorange!40!white] (A) {A};
    \node[mynode, below right=of A, shape=circle, fill=MediumRed!40!white] (D) {D};
    \node[mynode, above right=of D, shape=circle, fill=niceorange!40!white] (B) {B};
    \node[mynode, below left=of D, shape=circle, fill=niceorange!40!white] (C) {C};
    \node[mynode, below right=of D, shape=circle,draw=darkblue!70!white,
    line width = 0.7mm, fill=darkblue!40!white] (E) {E};

    % Edges
    \draw[arrow] (A) -- (D);
    \draw[arrow] (B) -- (D);
    \draw[arrow] (C) -- (D);
    \draw[arrow] (D) -- (E);
\end{tikzpicture}
```

In [Figure 3](#tikz:cond_independence), we have $\text{Pr}(E|A,B,C,D) = \text{Pr}(E|D)$.

### Graph Compatibility

In applications of Bayesian networks, we are often interested in whether the dependency relations implied by a DAG $G$ are *compatible* with a distribution.

```{prf:definition}
:label: graph-compatibility

A distribution $P$ is *compatible* with a DAG $G$ if it satisfies the conditional independencies implied by $G$. That is, suppose $\underline{X}\sim P$, then

$$\text{Pr}(\underline{X}) = \prod_{i=1}^{n} \text{Pr}(X_i | \text{Pa}(X_i))$$

```

We can roughly categorise the different modes of application of *Graph Compatibility* as follows:

1. *Finding a Graph Compatible with a Given Distribution:*
   - *Starting point:* This mode assumes the distribution $P$ is known.
   - *Objective:* We seek to construct a Bayesian network $G$ that is compatible with $P$.
   - *Approach:*
   - *Application:* This is particularly useful in theoretical or simulation studies where the distribution is specified in advance, and the researcher aims to visualise or understand the underlying dependency structure through a graph.
   - *Example:* A researcher in epidemiology is studying the relationship between lifestyle factors (diet and exercise), genetic predispositions, and the risk of developing type 2 diabetes. The researcher has theoretical knowledge and prior research findings that suggest certain conditional independencies among these variables.
2. *Using Data to Validate a Posited Statistical Model and Graph:*
   - *Starting point:* This mode assumes the graph $G$ is known and posits a statistical model $P_\theta$ using $G$. The statistical model is then fit to data.
   - *Objective:* We seek to check whether the dependencies implied by the graph $G$ are consistent with the data.
   - *Approach:* We can use $G$ to check which variables should be dependent or independent of each other. Then, statistical tests or measures of association in the data can validate our assumptions.
   - *Example:*
3. *Exploring Conditional Independencies Given a Graph:*
   - *Starting Point:* This mode assumes the graph $G$ is known.
   - *Objective:* We seek to investigate specific conditional independencies within this graph. For instance, given a set of variables $X$ and $Y$ and a conditioning set $Z$, we may want to determine if $X$ and $Y$ are conditionally independent given $Z$.
   - *Approach:*
   - *Application:*
   - *Example:*

#### Chains, Forks and Colliders

```{tikz}
:xscale: 100

\usetikzlibrary{arrows.meta, positioning, shapes, backgrounds}

\definecolor{darkred}{RGB}{160,0,0}
\definecolor{darkblue}{RGB}{7, 90, 224}
\definecolor{nicegreen}{RGB}{43, 194, 88}
\definecolor{niceorange}{RGB}{255, 221, 0}

\definecolor{InvisibleRed}{rgb}{0.97, 0.92, 0.92}
\definecolor{InvisibleGreen}{rgb}{0.92, 0.97, 0.92}
\definecolor{InvisibleBlue}{rgb}{0.92, 0.92, 0.97}

\definecolor{MediumRed}{rgb}{0.925, 0.345, 0.345}
\definecolor{MediumGreen}{rgb}{0.37, 0.7, 0.66}
\definecolor{MediumBlue}{rgb}{0.015, 0.315, 0.45}

\definecolor{mediumgray}{RGB}{120,120,120}

\tikzset{arrow/.style={
    -{Latex[length=3mm, width=2mm]}, % Arrow tip configuration
    line width=0.5mm, % Arrow line width
    draw=mediumgray, % Use the medium gray color for the arrow
}}

\begin{tikzpicture}[node distance=1.2cm and 1.5cm, 
                   mynode/.style={circle, draw=none, minimum size=1.2cm,outer sep=1pt, font=\sffamily}]

    % First figure
    \node[mynode, fill=MediumRed!40!white] (A1) {X};
    \node[mynode, right=of A1, shape=circle,draw=darkblue!70!white,
    line width = 0.7mm, fill=darkblue!40!white] (B1) {Y};
    \node[mynode, right=of B1, fill=nicegreen!40!white] (C1) {Z};
    \draw[arrow] (A1) -- (B1);
    \draw[arrow] (B1) -- (C1);


    % Second figure, positioned right of the first figure
    \node[mynode, right=1cm of C1, fill=nicegreen!40!white] (A2) {X};
    \node[mynode, below right=of A2, draw=darkblue!70!white, line width = 0.7mm, fill=darkblue!40!white] (B2) {Y};
    \node[mynode, above right=of B2, fill=nicegreen!40!white] (C2) {Z};
    \draw[arrow] (B2) -- (A2);
    \draw[arrow] (B2) -- (C2);

    % Third figure, positioned right of the second figure
    \node[mynode, right=1cm of C2, fill=MediumRed!40!white] (A3) {X};
    \node[mynode, below right=of A3, draw=darkblue!70!white, line width = 0.7mm, fill=darkblue!40!white] (B3) {Y};
    \node[mynode, above right=of B3, fill=MediumRed!40!white] (C3) {Z};
    \draw[arrow] (A3) -- (B3);
    \draw[arrow] (C3) -- (B3);

\end{tikzpicture}
```

- *Chain:*  Conditioning on $Y$ ensures $X$ and $Z$ are independent.
- *Fork:* Conditioning on $Y$ ensures $X$ and $Z$ are independent.
- *Collider:* Conditioning on $Y$ creates a dependency between $X$ and $Z$.

#### $d$-separation

$d$-separation provides a formal criterion for determining whether a set of variables is conditionally independent of another set of variables, given a third set of variables, within a Bayesian network. The criteria is purely graphical and makes no reference to the actual distribution of the variables.

Before we give the definition, we discuss its key component, open and blocked paths.

```{prf:definition} Open and Blocked Paths
Let $G =(V,E)$ be a Bayesian network. Let $X, Y\in V$ be nodes in the graph. A *path* (a sequence of edges) from $X$ to $Y$ is *open* if:
- 


```

```{prf:definition} $d$-separation
Let $G = (V,E)$ be a Bayesian network. For any disjoint subsets of variables $A,B,C\subseteq V$, $A$ and $B$ are $d$-separated by $C$ if and only if all paths from $A$ to $B$ are *blocked* by $C$.

```

### Inference in a Bayesian Network

### Graphical Model Examples

#### IID Bayesian Inference

Suppose we have $n$ independent observations $X_i | \theta \sim \text{Distribution}(\theta)$. We can represent this as the following Bayesian Network:

```{tikz}
:xscale: 50

\usetikzlibrary{arrows.meta, positioning, shapes, backgrounds}

\definecolor{darkred}{RGB}{160,0,0}
\definecolor{darkblue}{RGB}{7, 90, 224}
\definecolor{nicegreen}{RGB}{43, 194, 88}
\definecolor{niceorange}{RGB}{255, 221, 0}

\definecolor{InvisibleRed}{rgb}{0.97, 0.92, 0.92}
\definecolor{InvisibleGreen}{rgb}{0.92, 0.97, 0.92}
\definecolor{InvisibleBlue}{rgb}{0.92, 0.92, 0.97}

\definecolor{MediumRed}{rgb}{0.925, 0.345, 0.345}
\definecolor{MediumGreen}{rgb}{0.37, 0.7, 0.66}
\definecolor{MediumBlue}{rgb}{0.015, 0.315, 0.45}

\definecolor{mediumgray}{RGB}{120,120,120}

\tikzset{arrow/.style={
    -{Latex[length=3mm, width=2mm]}, % Arrow tip configuration
    line width=0.4mm, % Arrow line width
    draw=mediumgray, % Use the medium gray color for the arrow
}}

\begin{tikzpicture}[node distance=1cm and 1cm, 
                    mynode/.style={circle, draw=none, minimum size=1cm, outer sep=1pt, font=\sffamily}]

% Parameter node
\node[mynode, shape=circle, fill=darkblue!40!white] (theta) {$\theta$};

% Data nodes
\node[mynode, below left= 1cm and 2cm of theta, shape=circle, fill=darkblue!40!white] (X1) {$X_1$};
\node[mynode, right=of X1, shape=circle, fill=darkblue!40!white] (X2) {$X_2$};
\node[right=of X2] (dots) {\color{mediumgray}$\cdots$}; % "..." element
\node[mynode, right=of dots, shape=circle, fill=darkblue!40!white] (Xn) {$X_n$};

% Edges
    \draw[arrow] (theta) -- (X1);
    \draw[arrow] (theta) -- (X2);
    \draw[arrow] (theta) -- (Xn);
\end{tikzpicture}
```

#### Markov Model

Suppose we have $n$ independent observations $X_{i+1} | \theta, X_{i} \sim \text{Distribution}(\theta, X_i)$. We can represent this as the following Bayesian Network:

```{tikz}
:xscale: 50

\usetikzlibrary{arrows.meta, positioning, shapes, backgrounds}

\definecolor{darkred}{RGB}{160,0,0}
\definecolor{darkblue}{RGB}{7, 90, 224}
\definecolor{nicegreen}{RGB}{43, 194, 88}
\definecolor{niceorange}{RGB}{255, 221, 0}

\definecolor{InvisibleRed}{rgb}{0.97, 0.92, 0.92}
\definecolor{InvisibleGreen}{rgb}{0.92, 0.97, 0.92}
\definecolor{InvisibleBlue}{rgb}{0.92, 0.92, 0.97}

\definecolor{MediumRed}{rgb}{0.925, 0.345, 0.345}
\definecolor{MediumGreen}{rgb}{0.37, 0.7, 0.66}
\definecolor{MediumBlue}{rgb}{0.015, 0.315, 0.45}

\definecolor{mediumgray}{RGB}{120,120,120}

\tikzset{arrow/.style={
    -{Latex[length=3mm, width=2mm]}, % Arrow tip configuration
    line width=0.4mm, % Arrow line width
    draw=mediumgray, % Use the medium gray color for the arrow
}}


\begin{tikzpicture}[node distance=1cm and 1cm, 
                    mynode/.style={circle, draw=none, minimum size=1cm, outer sep=1pt, font=\sffamily}]

% Parameter node
\node[mynode, shape=circle, fill=darkblue!40!white] (theta) {$\theta$};

% Data nodes
\node[mynode, below left= 1cm and 2cm of theta, shape=circle, fill=darkblue!40!white] (X1) {$X_1$};
\node[mynode, right=of X1, shape=circle, fill=darkblue!40!white] (X2) {$X_2$};
\node[right=of X2] (dots) {\color{mediumgray}$\cdots$}; % "..." element
\node[mynode, right=of dots, shape=circle, fill=darkblue!40!white] (Xn) {$X_n$};

% Edges
    \draw[arrow] (theta) -- (X1);
    \draw[arrow] (theta) -- (X2);
    \draw[arrow] (theta) -- (Xn);
    \draw[arrow] (X1) -- (X2);
    \draw[arrow] (X2) -- (dots);
    \draw[arrow] (dots) -- (Xn);
\end{tikzpicture}
```
