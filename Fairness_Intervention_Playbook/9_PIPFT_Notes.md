### Translating Fairness Definitions to Mathematical Constraints

Different fairness definitions require different mathematical formulations. For example, demographic parity can be expressed as equality 
constraints on prediction rates across groups, while equalized odds requires conditional constraints that consider both predictions and ground truth labels.  

Zafar et al. (2017) pioneered this approach by showing how fairness constraints could be incorporated into logistic regression through convex relaxations. 
For demographic parity, they formulated a constraint that equalizes the mean prediction across protected groups:  

<img width="779" height="88" alt="image" src="https://github.com/user-attachments/assets/dd8de286-2c74-4e0c-a136-7ddb56bd59a0" />  

Where h(X) is the model's prediction, Z is the protected attribute, and ε is a small tolerance. This constraint ensures that the 
average prediction for different groups differs by no more than ε, directly enforcing the demographic parity criterion during training.  

### Constrained Optimization Approaches  

Constrained Optimization Approaches
Once fairness definitions are translated into mathematical constraints, you must integrate these constraints into the learning process through constrained optimization techniques. 
This integration is essential for in-processing because it determines how the algorithm will navigate the trade-off between its original objective and the fairness constraints.  

Standard machine learning models typically minimize an unconstrained loss function: min₍θ₎ L(θ)  

Where L(θ) represents the loss function (e.g., cross-entropy loss) and θ represents the model parameters. To incorporate fairness, this problem is reformulated with constraints:  

<img width="1035" height="106" alt="image" src="https://github.com/user-attachments/assets/00a6f30f-be93-4fea-a6c9-379e40d4c2f3" />  

Where Cᵢ(θ) represents fairness constraint functions and εᵢ represents tolerance levels for each constraint.  

### Lagrangian Methods and Duality  

<img width="551" height="135" alt="image" src="https://github.com/user-attachments/assets/478ab662-9314-4362-b781-f8f2d556228a" />  



