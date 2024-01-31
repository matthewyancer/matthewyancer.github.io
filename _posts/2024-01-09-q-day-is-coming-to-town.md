## Q-Day is Coming to Town

It was December 24, 2023. The stockings were hung with care. All of the presents were wrapped and under the tree. The children had finally settled down for the night. The house was quiet. Time for a bit of relaxing in front of my TV [fireplace](https://www.youtube.com/watch?v=UraL4IEcu-o) (thank you, [George Ford](https://www.fireplaceforyourhome.com/)).

"I wonder what's new in the world?", I muttered to myself while opening up [Slashdot](https://slashdot.org), news for nerds. Scroll, scroll, scroll. Amongst the postings about ChatGPT, the Free Software Foundation, gaming, Doctor Who, Linux, AI, [Aquaman flopping at the boxoffice](https://www.youtube.com/watch?v=7hC3uyQdQKM), I stumble upon a quantum computing post with a rather alarming first line:

> A Canadian cybersecurity firm [has warned that as soon as 2025](https://it.slashdot.org/story/23/12/23/1954219/the-race-to-shield-secrets-from-quantum-computers), quantum computers could make current encryption methods useless.

And [to further complicate matters](https://www.reuters.com/investigates/special-report/us-china-tech-quantum/)...

> QD5’s executive vice president, Tilo Kunz, told officials from the Defense Information Systems Agency that possibly as soon as 2025, the world would arrive at what has been dubbed “Q-day,” the day when quantum computers make current encryption methods useless. Machines vastly more powerful than today’s fastest supercomputers would be capable of cracking the codes that protect virtually all modern communication, he told the agency, which is tasked with safeguarding the U.S. military’s communications.
>
> In the meantime, Kunz told the panel, a global effort to plunder data is underway so that intercepted messages can be decoded after Q-day in what he described as “harvest now, decrypt later” attacks, according to a recording of the session the agency later made public.

![Meme: Blinking White Guy](/assets/images/blinking-white-guy.jpg)

Well, that's not what I want to see on my quiet Christmas Eve.

But there's some good news. While the above article describes efforts underway to develop post-quantum cryptography, there are solutions available today. The types of encryption vulnerable to attack by quantum computers are those based on large prime numbers, such as asymmetric public-key cryptography. There are other types of cryptography available now that are quantum-resistant and can be deployed using existing standards on today's non-quantum computers. This [post](https://www.archonsecure.com/blog/quantum-resistant-cryptography) describes the use of IKEv1 (not the newer IKEv2, which is quantum vulnerable) combined with pre-shared keys and the use of AES-256 symmetric encryption algorithm to achieve this quantum-resistant purpose.

There is disagreement on how quickly Q-Day will arrive, with some saying years and others saying decades, but it is an inevitability. If it does end up being closer to the multiple decades mark, this is still a concern for military data, state secrets, and healthcare data. It sounds like slapping on https and calling it good enough is no longer good enough.

Happy Holidays
