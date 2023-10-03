## The Pizza Ordering Interface

If I were to call up any pizza place in town, I guarantee you, this is the conversation flow I would get:

Them: *"Hi, Pizza Brand Pizza. This is Julie speaking. How can I help you?"*  
Me: *"Yes, I'd like to order delivery."*  
Them: *"Delivery? Sure. Can I get your phone number?"*  
Me: *"867-5309."*  
Them: *"Ok, I have you at 123 Fancy Pants Lane. Is this correct?"*  
Me: *"Yes."*  
Them: *"Ok, what can I get you?"*  
Me: *"I'd like a large pizza with mushrooms, green peppers, and onions."*  
Them: *"Ok, large pizza with mushrooms, green peppers, and onions. Anything else?"*  
Me: *"Yes, I'd like a large cheese pizza."*  
Them: *"Ok, large cheese pizza. Anything else?"*  
Me: *"That's it."*  
Them: *"Ok, you're total is $41.34. Will that be cash or card?"*  
Me: *"Card."*  
Them: *"Ok, I'm ready for the digits when you are."*  
Me: *"Ok. 1234 5678 9012 3456."*  
Them: *"Ok, expiration date?"*  
Me: *"10/25."*  
Them: *"Security code?"*  
Me: *"987."*  
Them: *"Ok, you're all set. A driver will be out in about 45 minutes."*  
Me: *"Ok, thanks."*  
Them: *"You're welcome."*  

In fact, I expect that if I were to call up any pizza place in the whole country, I would get the same flow. This would probably be true in the whole world; perhaps just swap out English for some other language.

How can this be? How can all pizza restaurants follow the same script? Was there a Zoom call that representatives from all pizza establishments joined where everyone agreed that this would be the only way to order pizza? A "continental congress of pizza," if you will?

It turns out there is a well-defined *pizza ordering interface* that is implemented by all pizza restaurants because all pizza restaurants need the same things.

Pizza restaurants need a phone number that customers can call, and they need to publish this phone number where customers can see it, or there will not be orders coming in.

There is a set of data points that all pizza restaurants need from customers:

- Contact Info
- Order Info
- Payment Info

And customers like to know:

- The total cost for their order
- How long will they have to wait until they get that ["lovely cheese pizza, just for me"](https://www.youtube.com/watch?v=RISQc8mptK4)

Information needs to be exchanged in a certain order. Imagine if the customer asked for their total at the beginning of the call: "But sir, you haven't ordered anything yet!" And I don't think the customer would be happy if the restaurant asked for the credit card first: "How much are you charging on my card?!" Or if they established your address at the very end of the call: "Oh, I'm sorry, you appear to be outside our delivery radius; we'll have to cancel your order." What if they took down your phone number at the end of the call? Re-establishing call interruptions would be difficult: "Uh yeah, I was the guy that was ordering a pepperoni pizza..."

There needs to be a way to handle and prevent issues. The person taking your order needs to confirm your order to prevent mistakes. If the kitchen has a question about your order or if the delivery driver can't find your address, they need a phone number to call. And if there are weird, exceptional situations, there needs to be a manager that can address the issues.

When designing communications between two modules in any system, the same areas need to be established:
- Why are the parties communicating?
- What data will need to be exchanged?
- In what order does the communication need to take place?
- How will communication errors or interruptions be handled?

For further reading on interfaces, including more on the pizza interface, I recommend the now out-of-print [Pragmatic Programmer's Interface Oriented Design by Ken Pugh](https://www.amazon.com/Interface-Oriented-Design-Pragmatic-Programmers/dp/0976694050/).

There is also some good information on interface-based programming over on Stack Overflow [here](https://stackoverflow.com/questions/1848442/what-exactly-is-interface-based-programming) and [here](https://stackoverflow.com/questions/1413543/what-does-it-mean-to-program-to-an-interface).

