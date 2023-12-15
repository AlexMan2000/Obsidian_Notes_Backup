# Basic Setup of Linear Programs

## General Form LPs
> [!def]
> ![](Linear_Programs.assets/image-20231213224732929.png)




## Standard Form LPs - Conic Form
> [!def]
> ![](Linear_Programs.assets/image-20231129122742640.png)![](Linear_Programs.assets/image-20231213224640502.png)




## Converting LP to Stand Form
> [!important] Method
> ![](Linear_Programs.assets/image-20231213231145503.png)![](Linear_Programs.assets/image-20231213231150959.png)
![](Linear_Programs.assets/image-20231213231130399.png)![](Linear_Programs.assets/image-20231213231408682.png)

> [!example]
> ![](Linear_Programs.assets/image-20231129122836866.png)![](Linear_Programs.assets/image-20231129122631591.png)![](Linear_Programs.assets/image-20231129122638713.png)

### Any Linear Program is Convex Problem
> [!property]
> ![](Linear_Programs.assets/image-20231129122926905.png)



## Dual of Standard Form Linear Program
> [!important]
> ![](Linear_Programs.assets/image-20231129123000901.png)![](Linear_Programs.assets/image-20231129123009603.png)![](Linear_Programs.assets/image-20231129123017555.png)








# Solving Linear Programs - Simplex Method Idea
> [!motiv] Motivation
> ![](Linear_Programs.assets/image-20231129123051076.png)![](Linear_Programs.assets/image-20231129123311347.png)
> What simplex method is saying is that for **bounded** linear programs there is at least one optimal solution that is extreme point. 
> 
> It is not saying that all the optimal points are extreme points, for example if the contour line of our objective function is parallel to the boundary of the polyhedra, under which case all the points(definitely including vertices) will be the optimal points.
> 
> But we will later show that for a bounded linear program, **all the optimal points must be on the boundary of the feasible set.**



## Extreme Point, Vertex
> [!def]
> ![](Linear_Programs.assets/image-20231129123455006.png)

> [!important] Counter-Definition
> This definition seems weird, since it defines something by saying ... doesn't exist. So it's better to work with its counter definition, which goes like:
> 
> **If for any $\vec{y},\vec{z}\in K\backslash\{\vec{x}\}$ and $\theta\in \{0,1\}$ we have $\vec{x}=\theta\vec{y}+(1-\theta)\vec{z}$, then $\vec{x}$ is not a vertex of $K$**.

> [!example]
> ![](Linear_Programs.assets/image-20231129180548947.png)


## Polyhedra
> [!thm]
> P has an extreme point, if and only if P contains no line. 
> 
> If it contains no line, then it is bounded.
> 
> Bounded polyhedra is a polygon.
> 
> **In all, bounded polyhedra <=> Contains no line <=> Has a vertex <=> Is a polygon.**




## Geometric Interpretation of LP
> [!important]
> ![](Linear_Programs.assets/image-20231213225921701.png)![](Linear_Programs.assets/image-20231213225928120.png)



## Main Theorem of Linear Programming
> [!thm]
> ![](Linear_Programs.assets/image-20231213230052752.png)
> Here we assume that the feasible set contains no line and thus has an extreme point.
> 
> Since LP's feasible set is always a polyhedra, the above condition ensures that our feasible set contains a vertex. 
> 
> In this section, we want to prove that for a polygon(bounded polyhedra), at least one optimal point is the vertex of the feasible set $\Omega$.


> [!proof] Prook Sketch
> A few assumption of LP:
> 1. The feasible set $\Omega$ contains no line.
> 2. The feasible set $\Omega$ contains a vertex.
> 
> Suppose that the optimization problem has an optimal objective $p*$, then we pick its optimal set $Q$, which contains all the optimal points. 
>   
> Now, since $\Omega$ is a bounded polyhedra, or equivalently, contains no line, and that $Q\subseteq \Omega$, we know that $Q$ contains no line. Since every point in $Q$ must satisfy the feasible constraint, $Q$ is itself a bounded polyhedra and contains a vertex.  
> 
> Now we want to prove that if $\vec{v}$ is a vertex of $Q$, then $\vec{v}$ is a vertex of $\Omega$, this immediately implies that there exists an optimal point that's a vertex of $\Omega$. 
> 
> For the sake of contradiction, suppose $\vec{v}$ is not a vertex of $\Omega$, then by the counter definition of a vertex(which happens to be surprisingly straight forward), we know that $\exists\vec{y},\vec{z}\in \Omega\backslash\{x\},s.t. \vec{x}=\theta \vec{y}+(1-\theta)\vec{z}$, for $\theta\in (0,1)$. 
> 
> Now since $\vec{x}\in Q$, we know by definition that $\vec{c}^{\top}\vec{x}=p^*$. But since $\vec{c}^{\top}\vec{y}\geq p^*$ and $\vec{c}^{\top}\vec{z}\geq p^*$, we know that in order for the equality to hold, we have to ensure that $\vec{c}^{\top}\vec{y}=\vec{c}^{\top}\vec{z}= p^*$.
> 
> Thus $\vec{y},\vec{z}\in Q$, but this would imply that $\vec{x}$ is not a vertex of $Q$ by definition. Thus we derive a contradiction.

> [!proof] Formal Proof
> To formalize the proof, we have the following derivations:
> ![](Linear_Programs.assets/image-20231213230655926.png)

> [!important] Idea behind the theorem
> ![](Linear_Programs.assets/image-20231213230716233.png)


## Bounded Feasible Set => All Optimals on the boundary
> [!important] EECS127 Fa22 HW10 P2
> ==Important==: Next we want to prove that for a bounded LP program, the optimal point must appear on the boundary, not the interior of the feasible set. That is, all the optimal points must 
> ![](Linear_Programs.assets/image-20231214210428675.png)![](Linear_Programs.assets/image-20231214210435819.png)![](Linear_Programs.assets/image-20231214210444046.png)










# Extreme Points, Vertices, BFS
## Extreme Points
> [!def]
> ![](Linear_Programs.assets/image-20231214091704691.png)![](Linear_Programs.assets/image-20231214091735938.png)



## Vertex
> [!def]
> ![](Linear_Programs.assets/image-20231214091809399.png)![](Linear_Programs.assets/image-20231214091930754.png)








# Chapter Exercises

