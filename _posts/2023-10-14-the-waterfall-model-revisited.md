## The Waterfall Model, Revisited

In 1970, Dr. Winston W. Royce wrote a paper entitled *Managing the Development of Large Software Systems*. This is where the famous and much maligned [Waterfall Model](https://www.techtarget.com/searchsoftwarequality/definition/waterfall-model) for software development was pulled from and would go on to be a dominant software development methodology for over 30 years. Here's an image of the model, pulled straight from Royce's paper, that you may have seen many times before:

![Diagram: Waterfall Model](/assets/images/waterfall.png)  
(Image from [here](https://web.archive.org/web/20170219154153/https://www.cs.umd.edu/class/spring2003/cmsc838p/Process/waterfall.pdf), figure 2 on page 2)

You may be amazed, however, to learn that Royce gave this as an example **of what not to do**! He describes the approach as "risky and invites failure". The rest of the paper describes a five-step process for transforming this "simpler" method into something that could produce desired results in a large software development project. Royce reinforces again at the end of the paper that (with added emphasis):

> The simpler method **has never worked on large software development efforts** and the costs to recover far exceeded those required to finance the five-step process listed.

What did Royce see as the risks with this "simpler" approach? It was only once the project had reached the testing phase, after much of the project was supposed to be "complete" that major learnings were discovered about the product itself. Things like performance and storage requirements. And if these didn't meet constraints, major requirements or design changes would be necessary. To put it in Royce's words (with added emphasis):

> In effect, the development process has returned to the origin and one can expect up to a **100-percent overrun in schedule and/or costs**.

*It never ceases to amaze me that people don't read instructions.*
 
So, what is Royce's recommended five-step process, you might ask? Below is a diagram from the same paper (I have removed the side-by-side inclusion of the "simpler" method from the diagram for clarity purposes):

![Diagram: Royce Five-Step Process](/assets/images/royce-five-step-process.png)  
(Image from [here](https://web.archive.org/web/20170219154153/https://www.cs.umd.edu/class/spring2003/cmsc838p/Process/waterfall.pdf), figure 10 on page 11)

Let's step through what is going on here.

1. **Program Design Comes First**: An architectural design step is added between the Software Requirements and Analysis steps. The purpose of this step is to work through [non-functional requirements](https://en.wikipedia.org/wiki/Non-functional_requirement#:~:text=6%5D%5B7%5D-,Examples,-%5Bedit%5D) such as performance and storage so that impacts from these areas can be considered at the beginning of the project and factored into downstream activities rather than showing up as surprises at the end of the project.

2. **Document the Design**: Clarification is given on when and what should be documented throughout the project. Detailing the types of documentation at each phase and when documents should be revisited and revised throughout the process.

3. **Do it Twice**: If the system is [being built for the first time (greenfield), as opposed to extending an existing system (brownfield)](https://naturaily.com/blog/greenfield-vs-brownfield-projects-in-it-differences-pros-cons-and-how-to-lead), then Royce recommends building the system twice. The first time as a smaller pilot or prototype, and then applying the lessons learned to the second production version of the system. The pilot would focus on "trouble spots" in the design, evaluating solutions and alternatives once again to ensure risk is eliminated earlier in the project rather than as a surprise at the end.

4. **Plan, Control, and Montior Testing**: Royce identifies a number of practices to include within the testing phase, including code reviews, testing of every logic path, and product assurance techniques.

5. **Involve the Customer**: There are a lot of steps between specifying requirements and making a system operational. If the customer is only involved at the beginning and end, there is a risk that the project can go off course. Royce identifies 3 points where the customer should be involved: after preliminary program design, during the main program design, and after testing prior to operations.

What do you think? Does this seem like a reasonable approach for developing software?
