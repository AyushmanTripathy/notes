# Software Testing

from: [nptel](onlinecourses.nptel.ac.in/noc24_cs91)

## Introduction

### Facts about Testing

- cannot be used to prove software is correct
- Needs human intervention, cannot be completely automated
- cannot be replaced by software reviews and audits

### Testing based on process maturity

based on different levels of thinking

0. testing and debugging is same
1. used to show correctness (good software or bad test)
2. show software doesn't work
3. there is risk, want to reduce the risk
4. way to increase quality

this course is for level 3 and 4 thinking

## Terminologies

IEEE maintaines standard glossary of software terms

### Terms

- `Validation` done at the end of development, to ensure compliance
- `Verification` done while the development

- `Test case` inputs and expected outputs

<br>

- `Fault` static defect
- `Error` internal incorrect state due to fault 
- `Faliure` external incorrect behaviour due to fault

a fault will not always give an error, error will not always give failure.

### Types of testing

depending on the phase of software development

- `Unit Testing` Done by developer during coder
- `Integration Testing` component tested together
- `System Testing` full system and platform where it will run
- `Acceptance Testing` Done by end customer

`Beta Testing` beta version of software is tested by users.  
Additional types of testing

- `Functional Testing` ensures that it meets its functionality
- `Stress Testing` evaluate how system behaves under peak inputs
- `Performance Testing` ensure speed and response time of system
- `Usability Testing` evaluate user interface, aesthetics
- `Regression Testing` done after modification, modification is working and does not damage others

broad methods

- `Black-box Testing` tests functionality without looking at internal design (ex: all)
- `White-box Testing` tests internal structure of design (ex: during development, Unit, Integration and System)

Test design is the most critical job, because Pareto principle

### Testibility 

`Observability` ease to observe behaviour of program  
`Controllability` ease to provide needed inputs  
together they mean Testibility.

#### RIPR Model

conditions required for failure to be observed

- `Reachability` reaching the fault
- `Infection` reaching the error
- `Propagation` reaching the failure
- `Revealability` failure is observed

### Model Based Testing

working with models of software artifact and deriving test cases.  
models can be

1. formal, mathmatical notations
1. modelling languages (UML, SysMl, Simulink)

## Miscs

- `Pareto Principle` 80% of consequences come from 20% of causes
