
# Electrical Circuit Analysis Introduction
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059197671.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059198617.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059191750.png)



# Basic Circuit Quantities
> **Current** is the flow of charges (e.g. electrons) in the circuit
> **Voltage **is the potential energy (per charge) between two points in the circuit. This potential energy is what causes charge to flow (ie. causes current). 
> **Resistance** is the material's tendency to resist the flow of current.  
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059209763.png)
> We use these quantities in a Circuit Diagram, a visual representation of how a collection of circuit elements are connected. Each circuit element has some voltage across it and some current through it. 
> Why is voltage “across” a circuit element? 
> Voltage, or electric potential, is only defined relative to another point. A simple analogy is elevation: A mountain’s summit could be 9,000 ft above sea level, but 21,000 ft above the bottom of the ocean. In both cases, the elevation is only meaningful relative to another point. 
> For convenience, we frequently define sea level as a reference point with “0 ft of elevation” – then we can state elevation as a single number which is implicitly referenced to sea level (ex. the mountain is 9,000 ft tall). 
> **Similarly, in circuits, we will frequently define a reference point, called ground, against which other voltages can be measured.  



# Basic Circuit Elements
## Wire
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059201190.png)



## Resistor
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059209120.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059209688.png)



## Open Circuit
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059207833.png)



## Voltage Source
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059205481.png)


## Current Source
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059208110.png)



# Rules for Circuit Analysis
## Kirchhoff's Current Law(KCL)
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059205732.png)

**Example**![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059219049.png)
**KCL Within Elements**![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059219124.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059219617.png)

## Kirchhoff's Voltage Law(KVL)
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059218164.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059214072.png)

**Example**![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059221435.png)


## Ohm's Law and Resistors
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059222916.png)



## Voltage Reference - Potentials
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059221250.png)






# Circuit Analysis Algorithm
## Guide to Finding Nodes
### Algorithm
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059222433.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059232459.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059239651.png)



### Redraw the Circuit
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059233321.png)

**Original**![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059231091.png)
**Alternative 1**![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059234497.png)
**Alternative 2**![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059234484.png)

## Circuit Diagram
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059249450.png)
> **Node: **Any point on the circuit where two or more elements intersects.
> **Branch:** Any circuit element apart from wires and open circuits.




## Node Voltage Analysis(NVA) Algorithm
> ![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059248490.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059256100.png)![image.png](1_Circuit_Analysis_Node_Voltage.assets/20230302_1059252855.png)



# Resources
[Note11](typed_notes_pdf/Note11.pdf)
[Written_Notes11](typed_notes_pdf/Written_Notes11.pdf)
