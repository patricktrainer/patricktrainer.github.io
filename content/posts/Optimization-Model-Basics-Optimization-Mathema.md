---
date: '2023-02-16'
draft: false
title: Optimization-Model-Basics-Optimization-Mathema
---

# Optimization-Model-Basics-Optimization-Mathema

An Unconstrained optimization problem is an optimization problem where the objective function can be of any kind (linear or nonlinear) and there are no constraints.
A linear program is an optimization problem with an objective function that is linear in the variables, and all constraints are also linear.
A quadratic program is an optimization problem with an objective function that is quadratic in the variables (i.e. it may contain squares and cross products of the decision variables), and all constraints are linear.
A nonlinear program is an optimization problem with an objective function that is an arbitrary nonlinear function of the decision variables, and the constraints can be linear or nonlinear.
An optimization model's variables can be accessed through its [Variables](https://www.extremeoptimization.com/Documentation/Reference/Extreme.Mathematics.Optimization.OptimizationModel.Variables.aspx) property.
For example, both linear and quadratic programs use variables of type [LinearProgramVariable](https://www.extremeoptimization.com/Documentation/Reference/Extreme.Mathematics.Optimization.LinearProgramVariable.aspx), which inherits from [DecisionVariable](https://www.extremeoptimization.com/Documentation/Reference/Extreme.Mathematics.Optimization.DecisionVariable.aspx) and has an extra [Cost](https://www.extremeoptimization.com/Documentation/Reference/Extreme.Mathematics.Optimization.LinearProgramVariable.Cost.aspx) property that represents the coefficient of the variable in the linear portion of the objective function.
An optimization model's constraints can be accessed through its [Constraints](https://www.extremeoptimization.com/Documentation/Reference/Extreme.Mathematics.Optimization.OptimizationModel.Constraints.aspx) property.
