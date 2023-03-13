Classical proofs:

Today, we're going to think of proof as an interactive process where there is the prover. But maybe more importantly for
our study, there is a verifier.So there is an explicit reference to whoever it is that's reading the proof and verifying
it is correct.And we think about this as follows. There's a claim, which is an input to both prover and the
verifier.Both of the prover and the verifier are actually algorithms. And the prover sends a string, which we will refer
to in this slide as a proof. The verifier reads this. So if you would like to think about that geometric proof,verifier
is the teacher reading your proof and at the end accepting is it correct or reject. Accepting the claim as being proved
or not.In fact in computer science, we often talk about efficiently verifiable proofs or NP proofs.And those are proofs
where the string that the prover sends to the verifier is short. And the verifier, in addition, doesn't have all the
time in the world to read it, he has polynomial time. Now to be more explicit, what does it mean by short?What do we
mean by polynomial? What we mean is that the string that the prover sends to the verifier is of size polynomial in the
length of the claim. So we think about the claim as string x, binary string.The message here is string, binary string w,
the length of w is polynomial in the length of x.So if it takes 100 bits to describe the claim, w's lengths would be
polynomial in 100.And the verifiers time is also polynomial in the length of x. So it could be linear, just the length
of x, quadratic length of x squared or the length of x, even to 100, as long as it's a polynomial function.Again, the
verify is an algorithm. Takes as input both x, the claim, and w, the proof string,does some processing. And at the end
decides what to accept or reject. We often say either accept or one.And when we say reject, it's either zero or reject.
I'll use those interchangeably.

Examples:

What are some examples?
And these are going to be important examples for the duration of the class today.

* One example might be of an NP proof in a claim is that the prover is trying to convince the verifier that a
  particular number n is a product of two large primes. This is an interesting claim because the verifying polynomial
  time, we don't know the procedure for it to be able to convince himself that n isa product of two large primes. So
  we need the help of a prover. Perhaps an all powerful prover. Certainly more powerful than polynomial time.Again,
  for this portion of the class, I don't pay any attention to how much time it took the prover to come up with the
  proof. All the attention is going to be devoted to how much time it takes to verify a proof once it's sent.Later, we
  will dedicate our attention to the kind of claims that can be proved by a polynomial time prover who knows maybe some
  extra information, which enables it to convince the verifier of the correctness of the claim. So for now, let's go
  back to n is a product of two large prime. What's the proof?Since the proven time might take a long time, we don't
  care about that. We just take attention to how much timeit takes to verify the prover just factors in, let's say the
  two prime divisors are p and q,sends it over to the verifier. What does the verify have to do? Is to multiply p times
  q and see that it gets n back.Multiplication is an easy operation, polynomial time. And he has to check that p and q
  each of both primes.And that's also an easy operation we know how to do in polynomial time. And if that's the case, he
  accepts. Otherwise, he rejects.So after this interaction, what does the verify really know? He knows the claim is true
  and isa product of two large primes. He knows something extra. He knows the primes themselves is actually more than
  was necessary in order to convince yourself that n is a product of two large primes or is it?Is there some other way
  to do that? We will see in a couple of slides that there is.But let's look at a few more examples.
* Second example. Now the prover is trying to convince the verifier that a number y is what we call a quadratic
  residue mod, a modulus n.So the input to do is to prove and verify is a pair y and n.And the claim is y is a
  quadratic residue mode n. What does it mean to be a quadratic residue?It means that if you look at the equation y
  is equal to x squared mod n, it's solvable.That is, there exists an x and it's an x that's essentially between one
  and n.And furthermore, it's what we call relatively prime to n. So there is no divisors in common between n and x.
  That's a solution to this equation. So there is an x such that y is equal to x squared mod n.And what would be the
  proof of that? Well, maybe the verifier can do it himself. It turns out that this is very hard problem.So it's hard,
  for example, to find the square root of y mod n because if it was an easy in polynomial time,the verifier would need
  the prover. How hard is it? It's as hard as factoring n, a well-known hard problem for classical computers. But the
  prover as we said, he's all powerful. Or she in this case.So she finds out an x, sends it over to the verifier. The
  verifier squares mode n, compares to see if is equal to y. And if so, it accepts. Else, it rejects. Again, it's an
  empty proof. There's a short string x that will convince the verifier to accept when the claim is correct. What
  happens after this interaction? The verifier is convinced that indeed there exists an x such a y is equal to x squared
  mode n. But he also knows x. He knows the square root of y.
* Last example before we start defining this more generally. Here, the claim doesn't talk about numbers.It talks
  about graphs. There are two graphs. Turns out if you look more carefully in these two graphs, they are actually
  isomorphic to each other.In plain English, that means they are the same graph, but drawn a little differently.And
  formally, it means that there's a mapping from the vertices of the graph of the left to the vertices of the graph
  on the right so that if you take this mapping which we call the isomorphism pi from numbers one up to 10 on the
  left the numbers one upto 10 on the right, vertices are from the left to the right, it will be the case that
  essentially the one on the left, if you map it to-- with the isomorphism to a vertex on the right,let's think of
  it as one, similarly, the two on the left to the two on the right,if there is an edge between the one and two on
  the left, there's also going to be an edge between the vertices that these two are mapped to on the right. And that's
  true for every pair of vertices. That means that these two graphs are isomorphic to each other.And that pi is an
  isomorphism. So how hard it is to describe how long is pi?Is it polynomial size and the size of the graph? Yeah.
  Essentially, the signs for every vertex a name on the edge of the graph. And that's just essentially, if there are n
  vertices,it's length n. And how much time does it take the verifier to check it? He has to go for every pair of
  vertices on the left, check if there is an edge between them on the left is also an edge between where they were
  mapped on the right. And if there's no edge between them on the left,there should be no edge between them on the
  right. After the interaction, the verifier will believe that two graphs are isomorphic, if you got a good isomorphism,
  but they also knows n isomorphous.

Efficiently Verifiable Proofs(NP-Languages)
So all of these examples are examples of NP proofs.Now of course, we are not interested in a particular number n or
a particular number of y, or particular pairs of graphs.We we're interested in the problem more generally. And we
call this a language, that is all the n's which are product of two primes. That's the language of composite
numbers, which are product of two primes or all the y's in n pairs,such that y is a quadratic residue mod n. In
other words, we're interested in languages. Formally, a language is just a set of binary strings x that satisfies
some property. And an NP language is defined to be,and this goes back to cooking. And the completeness is defined to
be those sets of strings L is an NP language if there is some verifier V who runs in polynomial time, polynomial in
the length of the x, such that both, two conditions hold. And that is completeness and soundness.What does it mean
that completeness holds? It means that when x is in the language, if you're talking about a claim or in the example,
it's the or composite numbers, when the language is a language of composite numbers, which are product of two primes
and were given such an n, then there has to be a poly log proof of witness w,the proof of consent to the verifier, such
that the verifier examining x and w will accept.But completeness is not enough. We also need soundness. And that is to
make absolutely sure that when x is not in the language, for this example,n is not a product of two primes, then there
is no witness that will convince the verifier to accept.In other words, for all strings w that the prover may send to
the verifier,the verifier will reject. So we usually talk about completeness allows honest provers to convince the
verifier. Soundness ensures that regardless of what a cheating prover is trying to do, he will not be able to convince
you the correctness of an incorrect claim.

1982-1985: Is there any other way?

But our question in this course is not about NP or NP completeness. But rather we're asking is there some other way
to prove these type of theorems? Can a prover, for example, convince a verifier that y is a quadratic residue of n
without sending a square root. So this is the question that motivatedSilvio Micali, Charlie Rackoff and myself to
study zero-knowledge proofs in the early 80s.And this is a process that took about three years. And the answer is yes.

Zero Knowledge Proofs: Yes

And the main idea, even without getting into the mathematics, is the way that the prover will convince the 
verifier that the
claim is true without giving away the NP proof,in the example of the square-- the y is a quadratic residue of n without
giving you the square root,is to prove instead that I could prove it, if I felt like it. So I'm not going to prove it to
you.But I will prove that I could prove it. And somehow being able to prove that I could will imply that at the end, the
verifier will be convinced and yet he will not know a square root, he will not know the factors of n, he will not 
know an
isomorphism.In fact, he will get zero-knowledge in addition to the fact that he claim is true.Of course, we will need to
define what it means to be zero-knowledge precisely. 

Zero Knowledge Interactive Proofs

So before we define it, I want to give you an idea of how possible
you can prove something is a square root or that two graphs are isomorphic and so forth without actually giving that as
isomorphism or giving you the square root.

Two New Ingredients

And I'm going to start just letting you know that this is no longer going to
be a prover sending a string w to a verifier.We're going to need to change the proof model. We're going to need two new
ingredients. One of them is going to be interaction.Rather than the verifier just passively reading the proof, he's
going to have to be engaged in a non-trivial interaction with the prover. So like you see in this picture, there will be
messages going back and forth, prover sending a message to the verifier.Verifier answers back, back and forth, back and
forth. Might be three steps, might be two steps,it might be length of x steps. But it will be polynomial number of
steps, you'll be more than a single message from prover to verifier. Later on in this class, we will see that there is a
way to remove much of this interaction.There will still be, in a sense, at least a single message from prover to the
verifier and some preliminary stage. But for now, we have interaction.Interaction is not enough. We also have 
randomness.
What do we mean by that? We mean that the verifier is not just going to be a deterministic algorithm, evaluating what he
received from the prover. He is actually going to be allowed to toss coins as a primitive operation. And his 
questions to
the prover will depend on the result of tossing these coins. Another way to say that is that his questions are
somewhat unpredictable because if they were all predictable, the prover could have anticipated them and just sent 
him the
one string W in advance. But since they are unpredictable,after the prover sends a message, the verifier may ask
depending on its coin tosses, many different options.And the prover is supposed to be able to respond to all of them.
What is inherent in the fact that the verifier tosses randomness is that we're also going to be willing to accept a 
small
probability of error.What does that mean? We will get to the formal definition in a few minutes. Informally what that
will mean is that we whereas in geometry class, when you gave the teacher a proof, they checked it.And it was 
supposed to
be 100% correct. We are going to have as a formal part of the model,allow a small probability of error. But it's going
to be quantified. And you're going to have to be able to show that your error is smaller than one over-- I don't know,
Avogadro's number or a negligible error. We'll get to that in a minute.For now, the proof model is changing.

Interactive Proof Model

Its
interactive. It's probabilistic, meaning the verifier can toss coins.That means that there a lot of possible
interactions that will come up between prover and verifier. So there are a lot of possible executions.It's still going
to be the case, they both get input, which is the claim. And at the end of this question answer period,the verifier will
take the history of the interaction, the coin tosses that he's made, run an algorithm and decide whether to accept or
reject.

How to prove colors are different to a blind verifier?

Let's look at the first example.The first example is not going to even be mathematical. But it will be something
from the physical world.The claim here will be that this particular page right in front of us has two colors rather
than a single monochromatic color. And the scenario that I would like you to keep in mind is let's say the prover can
tell colors apart,but the verifier is colorblind. And the prover is trying to convince the verifier that this particular
page has two colors.He's not going to enable him to see colors for the future. So in some sense, all he's going to
convince him is that this page is two colors and nothing else. So in that sense, it will not be transferring to him
anything beyond the claim. How? So here's the first step.The first step is the verifier uses his coin, flips the coin.
And with the following idea.If the coin lands on heads, he takes the page and flips it over. And if it lands on 
tails, it
doesn't change the page at all.Let's assume that he tossed the coin and indeed it was heads. So he flipped the pages so
that what earlier was purple in the top now it's on the bottom. And now he does this in the privacy of his own home,not
showing the prover of the results of his coin. But what he does is he sends the coin the page over to the prover.The
prover now looks at this page. He knew what the page looked like before and he's now sees what the page looks like
now.Since the prover can distinguish colors, he can tell whether the coin landed on heads or tails,right? And indeed,
that's exactly what he says. He sets out, he checks whether the page was flipped or not, he writes the value of the new
coin, coin prime, to be head if it's flipped, tails otherwise,then he sends back coin prime. He says, listen, I think
you tossed coin prime.The verifier-- the rule right now is that the verifier, if indeed the coin that the verifier 
tossed
is equal to the coin prime that prover thinks he tossed, he says, well, hmm,it looks like the prover could tell whether
the page was flipped or not.But he couldn't tell if he was only a monochromatic. So there must be two colors on this
page. I accept the claim's true.Of course, if the coin that he sent over is different than what if flipped, he says,
well, he couldn't even tell that he flipped it.There's certainly not two colors there. I reject. Let's try to analyze
this for a minute. Clearly, if there are two colors and the prover follows this procedure, then the verifier will always
accept because the coin prime will always equal the coin.If there is a single color, the prover cannot tell whether he
flipped or not.He could still try to guess he's a cheating proof, whether the coin landed on heads or tails. And he has
a 50/50 chance of guessing correctly.So the probability that he sends the correct coin is a half at most. And if the
verifier accepts in this case,the probability of the verify accepts incorrectly because perhaps the prover was lucky,
but there's a single color on this page is 1/2.So if there are two colors, he will always accept. If there's a single
color, the probability accepts is less than half.There's a gap between them, but you might not like these odds. Say
what, I'm going to accept incorrect statements, claims,with probability 1/2? No worries. You can repeat this process
again and again. Each time, the verifier tosses a new coin,decides whether to flip or not, sends the result, and so
forth. And now, what is the chance that the prover, in case there is only a single color, so it's not correct claim, is
able to provide the verify each timew ith a correct coin he tossed? It's 1/2 the first time. It's 1/4 to be able to do
this twice in a row.It's 1/8 to do this three times in a row. And it's 1/2 to the k if you repeat this k times.So the
probability that the verifier accept after k iterations of this is very, very small.So what has happened here? I was
able to convince a colorblind verifier of whether a page has two colors or not so that he always will accept when 
they're
two pages.And he will accept that there's two pages incorrectly with extremely small probability.Let's see this again.
This idea, a little bit different of using interaction and randomness to be able to convince someone of this time, a
mathematical statement without transferring sort of the obvious NP proof over. 

Interactive Proof for QR

So the next example is the example 
that we
started with.And that is the input to the prover and verifier are the pair n and y such that there exist an x such that
y is equal to x squared mod n. Or is it the proof is trying to convince the verifier that indeed this pair n,y is a
member of this language,the QR language, the quadratic residues language, those y's such that y equals the x squared mod
n for some x.How would you convince the verify of this case without giving him a square root? Here it goes.The prover as
a first step chooses a random value one r between one and n. In fact, to be absolutely correct,this r is supposed to be
between r and n and have the greatest common divisor with n,which is one, meaning there's no common divisors between r
and n. For those who don't want to really dwell into this, let'sjust think of it as a random number between one and n.
And then what he sends to the verifier is r squared.Doesn't send r, he sends r squared. And let's call it s, sends s.
And he says to him, listen, if I gave you both square root of s and a square root of s times y where y is the input, 
then
you would be convinced that the claim is true because if s has a square root, and s times y has a square root, then also
y itself has a square root mod n.But if I did that, that's like sending you a square root of s would be r. Square root
of s times y would be r times x, then you would know a square root of y. You would know x, just take r times x divide by
r. And the whole point here is I don't want to give you both.So what I'm going to do is I'm only going to give you
either square root of s or square root of s times y.But I want to convince you that I could have given you both the
square roots. And the way I convinced you is I tell you, you get to choose--you can choose to get a square root of s or
square root of s times y, your choice. And I will be able to answer either question.But I'm only going to answer one.
Now if the verifier is smart, the way to choose which he wants is going to be to flip a coin.Not to decide this
deterministically, but flip a coin. So then with 50/50 chance, he will,in case the prover is cheating, ask for an
equation that the prover cannot solve.Why? Because if the prover is cheating, he cannot solve both finding a square root
of s and a square root of s times y because in that case is not cheating.So the fact that he can do both means he's not
cheating. I will flip a coin as a verifier to choose a challenge.Hey, give me square root of s or hey, give me a square
root of s times y. He's supposed to do that.So my coin turned out heads or one, the prover is supposed to give back the
square root of s,which is r. And if the coin was tails, he's supposed to give the square root of s times y, which is r
times the square root of y or r times x, that's the square root of y.The verifier checks that he got the right answer.
So he will accept only if indeed when he takes what he got backand squares it, he will get back an answer for what he
asked for. So if it was heads, he asked for square root of s.In that case, it's s times y to the zero, just s. And if he
asked for tails, he wants the square root of s times y. 

Analysis 

Let's analyze this. Again, if the claim is true and the
prover acts according to the protocol, the verifier will always accept because the proof can always give the square root
of s and the square root of s times y.Again, prover's all powerful. He knows the square root of y. He can because he's
all powerful.In fact, that's the only thing he needs to know. But what happens when the claim is false? And this is
always the thing that's harder to show.If the claim is false, then no matter what the prover does,the probability that
he will be able to solve both equations, he can't solve both equations.He can solve one of them. So what's the
probability I asked him to solve the equation that he knows how to solve. It's at most 1/2.Again, maybe a half is not
enough for you. Repeat this 100 times and the probability that the verifier can 100 times be so unlucky as to choose
exactly the equation the prover can solve and not the other one which he cannot solve in the case where the claim is
false, is going to be vanishing within a number of trials.1/2 if you try once, 1/4 if you try twice, 1/8 if you try a
third time, and 1/2 to 100 if you go 100 times.And if you want it to go k times, it's 1/2 to do the k. 

What Made it possible?

So what happened
here?I can convince the verifier to accept when the claim is true.It's very, very unlikely I will convince the verifier
to accept when the claim is false.And I never, if you think about it, transferred the square root of x because every
time.I just give him a random r, which is a square root of s, or a random r times the original x or the square root of
y.Random times of the square root of y is random when you reduce it to mod m. So it gives, essentially, I'm sending
him random numbers which are independent of each other, even if I repeat this 100 times because each time I start
againw ith a verify-- with a prover choosing a new r. So what made this possible?Here's one intuition. There's lots of
possible execution. So there's lots of possible interactions or proofs.And the prover essentially chooses one of those
many possibilities in the first step.When he sends r squared, he's, sort of, choosing one of these many possibilities at
random. And each and every proof of these many random proofs is made of exactly two parts. One part is when I asked to
see the square root of s and one part is when I asked to seethe square root of s times y. Seeing either square root of s
or the square root of s times y gives nothing. If the verifier could have seen both, it would imply 100% correctness.And
the verifier chose at random which of these halves he wants to see, the square root of sor the square root of s times y.
The ability of the prover in principle to provide either part or convinces the verifier that the prover could have
answered both and therefore the correct-- the claim is correct.

Definitions : of Zero Knowledge Interactive Proofs

Let's define this precisely. All right. So we have p and
v, there an interactive prooff  or a language, for a set of statements. If, again, v is polynomial time, but this time
probabilistic polynomial time, and there's completeness and soundness. If the claim is true or x is a member of the
language,the verifier will always accept. And soundness now has been modified.If x is not true, the claim is incorrect
or x is not a member of the language, then for all cheating prover strategy,no matter how hard they worked, the verifier
will not accept with negligible probability, like the one 1/2 to the 100 or 1/2 to the k, 1/2 to the length of x.Let's
introduce a little bit of notation. So this is a-- sorry, this is a cheating prover.Every cheater proof of strategy will
only help the prover to convince the verifier with negligible probability. So a bit of notation. We use the following
notation.We talk about the probability that pv, so open paren, pv,closed paren on x except in the case of x equal to L,
x is an L, completeness is probability one.In the soundness case, we say that for all cheating provers P star, the
probability that P star interactin gwith V on input x, the probability that accepts is negligible. What's a negligible
function of length of x?That's a function that grows slowly than any one over polynomial.So wanting to do the length of
x is an exponentially small function. So it's smaller than one over polynomial for any polynomial. 

Interactive Proofs: Notation

Interestingly, if you
step back and you think to yourself,is this reasonable to call this an interactive proof? I claim that this is
ultimately what a proof is.It should convince the verifier of correct theorems. And it should not convince them of
incorrect theorems.If you only are managing to convince him with a probability that is so small that in one in the
lifetime of the universe, it's not going to happen, it's good enough for me. And that is ultimately what a proof should
be.It should convince you of correct theorems and not convince you of incorrect theorems. And an event that will take
time in one in Avogadro's number, one in the lifetime of the universe of convincing of an incorrect theorem
essentially never happens. 

Interactive Proofs for a Language ℒ: Notation

All right. By the way, interestingly, is that when you have an exercise, a homework,and 
you're
coming up with an interactive proof, sometimes, it's going to take a lot of work to get you to have verify,always accept
correct theorems and not accept correct theorems with negligible incorrect--and accept incorrect theorems with
negligible probability. You don't have to work that hard.You just have to show the completeness holds with probability c
and soundness does not hold, at most holds with probability s for c and s which are a polynomial apart.So this will be
equivalent to achieving probability one for c, and negligible for s.This can be shown in some standard technique of
using repetitions.So we define what an interactive preferred language is.

The class of Interactive Proofs (IP)

We also can talk about the class of all
languages that have interactive proofs. And in the same way that we talked about NPas being all those languages for
which there is an NP poof, we will talk about IP as all those languages for which there is an interactive proof. Again,
the proven runtime might be very slow. But the verifier has to be polynomial time,probabilistic polynomial time. 

What is zero-knowledge?

All
right.We have defined what an interactive proof is. But what about zero-knowledge?How do we define zero-knowledge? What
is even the intuition of what should be zero-knowledge? So here is the intuition.I want a zero-knowledge interactive
proof to be the kind of proof such that whenever the statement is true, then the verifier goes through a
proof,interactive proof of the prover. And at the end, he's convinced with high probability that the claim is true. But
in addition to that, he has a history of interaction,he has the coins that he's tossed. Maybe you've given him so much
during this interactive proof that now he can compute a lot more than he could compute before. So for the example of the
n, proving that n is a product of two primes, perhaps after the interactive proof, he can factor a number or compute a
square root or find an isomorphism.We will say that the interaction was zero-knowledge if what the verifier can compute
after the interaction is essentially the same of what he could have computed before, namely the interaction has not
increased the computational power or allowed the verifier to compute more than he could have computed before.
Furthermore,
we want this to be true, not just for the honest verifier who follows the protocol, but for any verifier, even in a
devious malicious, adversarial verifier. This slide is an intuition. 

How do we mathematically capture this? The Verifier’s View

Let's try.
Again, we're going to do this slowly.So first of all, I want to say that this verifier has some sort of view. And I want
to--so he's learned that after the interaction that the theorem is true with high probability. But he's also gotten a
view.And that's the transcript of the answers and questions plus the coins he tossed. We will define this formal
variable,which is view sub v of PV on x. And that is a random variable.What I mean by that is that there's a lot of
possible values that this variable can get.And this is a probability, if they're distributed over the coins that v and p
both tossed. Remember, let's say in the example of showing that y is a quadratic residue, the prover tossed coins
selected r. The verifier tossed coins to select whether he wants to see the square root of r squared or the square root
of r squared times y.So those are all possible executions, these are all possible assignment that this variable can
get.OK. So this is a verifier's view. 

The Simulation Paradigm

I will say that this view gives the verifier nothing new if the following is true.
And this is called the simulation paradigm. This is-- the simulation paradigm is started with the concept of
zero-knowledge. It's used all over cryptography today. What is the simulation paradigm idea?We say that the real view,
so if we look at this blurb or this great blurb that I call real view, which is essentially, this is a probability
distribution, the points in this space are all the possible histories of interactions between prover and verifier plus
the verifier's coin.I say that this view gives the verifier nothing new if he could have actually simulated it on his
own,sitting with his laptop or his computer at home, not talking to any prover, he could have come up with a simulated
view. So this is again a probability distribution. You can essentially sample these simulated views himself.And what has
to be true about the simulated view in terms of relation to the real view is that if there's someone else out there, 
like
let's call him the polynomial time distinguisher, and he's pressing a button say he's giving me give me a sample in the
distribution that you have. I'm trying to determine whether I'm talking to the real view or I'm talking to the simulated
view.I'm just going to keep pressing the button getting views. And at the end, I should tell whether all the views I
got were from the real view or all the views I got from the simulated view. If a distinguisher can't tell this apart,
can't tell better than essentially 50/50, I say that these two views are computationally indistinguishable. He just, 
upon a
time distinguished, cannot tell them apart.Let's chew in this a little bit further.What does it mean that two
distributions-- two probability distributions are computationally indistinguishable? In our case here, the two
distributions are the real views and the simulated views.But it doesn't have to be applicable to this particular
setting.

Computational Indistinguishability

We can talk about computational indistinguishability as a notion more generally, where, again, there are two
distributions. In our case there were views, but there could be just two k-bit strings.And the game is that there's a
distinguisher on the other side of the wall and he can press a but to nand get samples always from either-- all the
samples from distribution d1, all the samples from the distribution d2.And his wish is to distinguish which is the case.
We say that these two distributions are computationally indistinguishable if for whatever strategy this polynomial
time distinguisher employs, so for all distinguishing algorithms, even after receiving a polynomial number of 
samples from
d, the distributions of either one or two, the probability that he can guess what is whether this was distribution 
one or
the distribution two is less than 1/2 plus negligible. Negligible and what?There's some sort of security parameter,
which I call k here, which might be the size of the strings of the samples,the size of the sample string.

Zero Knowledge: Definition

So back to
zero-knowledge.Here is a definition. An interactive protocol p and v is zero-knowledge for language L if there exists a
simulator in algorithm Sim, such that for every x in L, so I'm only requiring it when the theorem is correct, only 
when x
is in L. And why?Because you do get something, you get that x is an L. But that's a detail aside. So I require that the
following two probability distribution are polynomial time indistinguishable. The first is the real view that the
verifier gets during an interaction. The second is an output of the simulator. The simulator here is taking x as an
input, just the x.Here it doesn't have any square root of y or any secrets, just the input, they're both p and vc.You'll
notice here that there's another input to the simulator, which is this one to the power of lambda.This is essentially a
technicality. It's because we want to make sure that we allow the simulator to run enough time, polynomial time.And
sometimes when x really small, that doesn't give him enough time. But really for all practical purposes,if we're
thinking about large x's, forget about this one. So both of them, the simulator runs in polynomial time.To be
zero-knowledge means that these two distributions should be computationally indistinguishable.And that will make a
protocol PV,a zero note interactive proof, if it's complete, if it's sound, so it satisfies completeness and
soundness and zero-knowledge according to this definition. Almost.Two caveats. We're going to let this Sim guy, this
probabilistic polymial time run in expected polynomial time.What that means is that it might-- that the simulator might
expect the polynomial time essentially means that if you take the expectation of how much time the simulator runs over
all possible randomness of the simulator, it's going to be a polynomial time.What essentially that means is that there
might be some very, very unlucky coins for the simulator, which will take a long time to run. But typically, he's going
to run in polynomial time.This is something that you guys should know. And that is the definition of expected polynomial
time.One more caveat. In this definition, I never said anything about the verifier.I just said that a particular pair of
p and v is zero-knowledge if the following conditions hold. But we want this to hold really, the zero-knowledge
property,for every verifier, even a cheating verifier. 

What if V is NOT HONEST

So the real final definition has to take into account the
possibility that the verifier might be a liar and might be trying to get knowledge when he shouldn't. So he's not
honest.So we finally get the definition that a protocol is zero-knowledge for language L if for every v start
working with p there exist a polynomial time simulator such that the view and the simulation are computationally
indistinguishable. And I'm using this squiggly equality to mean computationally indistinguishable. So these might be
different probability distribution, but the distinguiser cannot tell them apart.All right. So let's rest a second. So
p,v is zero-knowledge if for every v star, there was--no matter what v star does-- actually we could have simulated this
in our own.What does this capture the intuition that what the verifier can learn during the interaction doesn't add any
computational power?Remember our original intuition was that what you can compute before and what you can compute after
is the same.The reason is because we say the following. Listen, maybe there is a v star, a really devious one,who can
get something out of the prover. Being zero knowldedge says, no.If such a v star exists, then we could have computed
this before because the simulator could use that vstar to come up with a simulated distribution, which is more than what
the view is. But the zero-knowledge requirement says that that's not possible, that for every star there will be a
simulator that can achieve the same distribution essentially,computationally equivalent, to what can happen in the real
view. And therefore, the real view did not add any computational power.

Flavors of Zero Knowledge

All right.By the way, this is what's called a
computationally indistinguishable zero-knowledge. Sometimes people use the notation CZK for computational.But there are
other flavors of zero-knowledge. You can also ask for perfect zero-knowledge definition,so where the real distribution
and the simulated distribution are identical, or maybe statistically close.

Special Case: Perfect Zero Knowledge

So a perfect zero-knowledge is a special case
where if you look at the view of the verifier, then we can actually simulate it perfectly. So the simulated view and the
real view are the same. And that means that they're indistinguishable for any algorithm. So this would mean that 
when you
can prove perfect zero-knowledge, it's an unconditional result because usually when we only prove computationally
zero-knowledge, we make some assumption that there are some computations which are hard.Whereas with perfect, it's just
perfect zero-knowledge. There is no difference between what we can learn during the view, during the real 
interaction and
what we can learn from a simulation. 

Working through a Simulation for QR Protocol\
Recall the Simulation Paradigm


Let's work through a simulation now that we have a definition.We call the protocol
for quadratic residues. So the prover send r squared.He asked for either seeing r or r times square root of y. He got
back an answer.He checked it. So what's the view here? The view is s. That's the first message, b, second message.And z,
third message. And what are the coin tosses? Our B. So it's anyway included it's SBZ.How do we simulate that? Well,
we're going to simulate this a little bit in a different order.After all, the simulator, we can't just choose an r and
send himself a message. I mean, he could.But then if you toss a coin, you only know how to return r. You don't know how
to return r times square root of y.So how are we going to get a simulation? 

(Honest Verifier) Perfect Zero Knowledge

The idea is as follows.And we're going to
show a simulator just for an honest verifier. And in fact, the simulation is going to be a perfect zero-knowledge
simulation.What the simulator is going to do is rather than really go in the order that the real interaction is, it a
first going to choose the question of the verifier. And he's going to do that just the way an honest verifier would do.
It picks a random bit, b.Then it's going to actually pick the third answer, which is it's going to pick a random z.
Notice that z actually is just a random number except in this case, it's r. In this case, it's r times x. So the only
thing that remains isto make sure that I can figure out for which s would have been z the right answer?And note that
this equation s equal to z squared over y to the b mod n satisfies exactly what should be. Why is that? Let's look at
this. Let's plug in b equal to zero, in which case,s is equal to z squared. That's exactly what it should be. In the
case that b is equal to zero,z is the square root of s. What about when y is-- when b is equal to one?Then, I'm letting
us to be z squared over y. Is that correct? Let's think about it.If you look at z here, it's supposed to be in the case
of B equal to one, r times x. And what's the relation of r times x to s?The relation is that if I square this, I should
get s times y.And that's exactly the case here. If I square z, I get s times y.So lo and behold, I was able to come out
with a triplet which is identically distributed as what the view of the verifier, the honest verifier is during an
interaction. Obviously, this doesn't convince me of anything.It's not that I actually got an r squared and then I asked
a random b and got the response.I did this in my basement in a simulation. But the view is identical.Now what about when
the verifier is not honest?

Perfect Zero Knowledge: for all V*

So what about the case, the general case,where the verifier might not be tossing a coin and
sending over? That's a little bit of a problem. What if this adversarial verifier was the kind that when he saw some s,
he did some very complicated function or computational s and depending on the result of his computation, would ask a
particular b? Then he might have gotten something interesting depending on his computation. Well, I will show you that
even if he was an adversarial, very complex computation, I could still get the same view that he did using a
simulator.How is that? Again, I will pick a random b. Even though he doesn't like things that random.But wait, I'm not
done yet. I pick a random b, then I pick a random z. And now is when I do something different.I say to myself, all
right, I will for a minute,suppose that indeed b would have been what he will ask me the bad guy, the adversarial guy.
And I will compute s accordingly. And now it will actually send s to this bad guy.What does it mean send? Remember, the
simulator should work correctly for every v star, for every bad guy v star.The simulator has access to v star. The
intuition is that no matter how powerful the verifier is, he's polynomial time. And I have to come up with opponent time
simulator. So he, polynomial time program can have access to any other polynomial time program, including this verifier.
So what I do is know is I run this verifier,the bad verifier, on the input ny and first message s and see what he asks
for.If I was lucky, he's going to ask exactly the bit that I prepared for. And I know how to answer.But he might not do
that, in which case, I can't really output SBZ because I justdon't know the answer, the correct answers. What do I do
then? I start again. I go to step one.I again pick a random bit. I again pick a random z. I then compute s and now I ask
v star on this new n,y, and s.Why am I hoping that this time it's going to be better? I don't know if this time is going
to be better.But I do know that whatever it is that v star is doing, is this is a fixed behavior.But my v was chosen at
random. What's the probability that a random bit will equal a fixed behavior?50/50. And that means that within two
trials, I will be lucky enough to hit on the question the v star would have asked. I suggest that you think about this
more deeply and prove to yourself in the expected number of repetitions is two before I can output a triplet SBZ. And
this is why we require the simulator to be expected polynomial time. So within expected two trials, I will be able to
output something that is exactly the same distribution as would have happened in the real interaction. 

Prover seems to have proved more

All right.I want
to say that actually, if you think about this a little bit deeper, you realize that not only the prover convinced the
verifier that y has a square root, he actually proved that he knows how to--what that square root is. Because if he can
answer what the square root of s is and what the square root of s times y is,he could actually answer the square root of
y. He never does. He always gives you only the square root of s, which is just random, or the square root of s times the
square root of y, which again the square root of s masks the square root of y. But if he could do both, he does actually
know how to do a square root of y.So what's hiding in here is some definition of what it means for a machine to prove to
you they know something.Let's try to define that formally. We will say that a proof system is a proof of knowledge.So
it's not just a proof that something is true or false, but it's a proof of knowledge for language if the following is
true.So let's think for a second. How would you define that a machine knows something?Maybe the first definition would
come to mind is that it has some register and that square root is written in there.Or whatever it knows is written in
there. But it's not always the case. The way that we want to define that you know something or the algorithm knows
something, is that if I can run that algorithm on multiple inputs,I could eventually compute that thing that the
algorithm knows.So since the prover is an interactive algorithm, running it multiple time means that it can send me
messages,I could ask it a question, and send messages to ask questions. So I can run executions with the prover multiple
times if at the end, I can extract w, that is the definition to mean that the prover renewed w.And that's how we define
proof of knowledge. We say there exists a knowledge extractor algorithm,this extractor, that can run a protocol with a
prover, such at an expected polynomial time, this extractor running a prover the rotation is E sup p. So he has 
access to
the prover almost as an Oracle on x, will output the witness, w.Now I want to make one thing clear is that when I say
that the extractor runs p multiple times, I can actually make it run so that he always,in every execution, he asked me
the first same message. So it's like saying I can rewind him to run--to get started from the same starting point on the
same randomness. This is called the rewinding technique,which is something that happens all the time when we talk about
zero-knowledge. That is usually the technique to prove that something is zero-knowledge. And that is zero-knowledge 
proof
of knowledge.If we can rewind someone multiple times and eventually extract something from them,it will mean that they
knew it to begin with.So here are some technicality which I'm not going to cover but it is the more precise 
definition of
proof of knowledge that takes into account what's the probability that the prover managed to convince the verifier to
accept? Essentially, if the probability is greater than alpha, we have always in this lecture said that in the case x is
in the language, then the probability is always one. But sometimes, you will have example swhen the probability is not
one, it might be just greater than 2/3. Then we will just require the extracted to run in expected time one over alpha,
which one in 2/3 or one in polynomial, which will be polynomial still.

The Rewinding Method

An example of extraction. I said that the examples
of quadratic residues, the prover actually knows the square root x of r mod n. To technically show that he knows,we have
to satisfy the definition. So here it goes. Here's the extractor. The extractor starts running with the prover.The first
message of the prover is r squared mode n for some n. What does the extract to do?First step, it receives s and it asks
the heads for zero and gets back an r. So it stores r. And now he rewinds to the first step again.This time though, when
he gets s, he asks for tails or b equal to one, to zero.And he gets back rx mode n. Now he has run two executions, 
first
time asking for heads,second time asking for tails. He got two answers, rx and r can divide and extract the square root
of y mode n. So there's definitely an extractor. So by the definition, we have just shown here in this slide the prover
knows the square root of y. 

ZK Proof for Graph Isomorphism

ZK Interactive Proof for Graph Isomorphism

And let's try it for graphs.So graph isomorphism, which we discussed before. What would be
the interactive proof,the zero-knowledge interactive proof for graph isomorphism? Let's go through that. It's going to
be surprisingly similar to the square root example, even though we're talking about graphs. When I say similar, I don't
mean that it's the same message is going back and forth. But the idea is quite similar. What is the idea?So now we're
talking there's graphs G0, G1, the prover is this all powerful guy. He knows actually in this example, an
isomorphism.He wants to convince the verifier that isomorphism exists without giving the isomorphism. How does he do
it?Here is what he does. He says to the verifier, listen. I'm going to forget about the proof for a minute.Let's just
see what the interaction is. He says to the verifier, I'm going to produce a random graph H, like a third graph, so that
I can give you an isomorphism either from G0 to H or I can give you an item of wisdom from G1 to H. These are two 
different
isomorphism. But the conclusion is if indeed I could do both,then there is actually direct isomorphism from G0 to G1. So
you see that very quickly here on the left on the side,if H is gamma zero of G, an isomorphism from G0 and H is also an
isomorphism from G1, gamma one,then you could go directly from G0 to G1 by taking gamma one inverse of gamma zero,
composition of these two isomorphisms. Now the point is, again, he's not going to do both.He's only going to give him
either isomorphism for G0 or G1. But he lets the verify choose which it is.And the fact that he will be able to do both
should convince the verifier that there is an isomorphism from G0 to G1 with high probability.

Input: (G0,G1)

If we break it down into
the interaction, the prover sends the verifier the new graph H, the verifier tosses a coin, asks either for isomorphism
from G0, isomorphism from G1, or isomorphism from G1.The prover is supposed to supply what he was asked for and the
verifier can check that he got the right thing.And only then accept, otherwise reject. If the statement that G0 was
isomorphic to G1 is true,the prover will be able to answer and the verifier should always accept. If the statement was
false, the probability the verifier will catch a mistake, that is, will ask to see isomorphism from G0 and the prover
won't be able to supply it because there's either just an isomorphism G0 or from G1 or maybe from none,the probability
the verifier will catch a mistake is great or equal than a half.And if we do this 100 times, the probability will be--
of catching a mistake it will be very close to one.One minus one into 100 or if you repeat k times one minus one in two
to the k.I leave it as an exercise to you that it's perfect zero-knowledge. It's going to be essentially trivial if you
understood the quadratic residue example to come up with the perfect zero-knowledge proof here.I encourage you to do
that.

ZKPOK that Prover knows an isomorphism from G1 to G2

It's also not just a zero-knowledge proof,but it's a zero-knowledge proof of knowing an isomorphism. So it's a
proof of knowledge.Again, to show that, you have to show an extractor. Let's show an extractor.So the extractor
algorithm is allowed to run the prover. Let's do it.The prover sends you a graph H. What do you do? First, you set the
coins to heads and you get back and answer, which is an isomorphism from G0 to H. Second, you rewind. You start again
with the same H, but this time, you ask for tales. And it will give you an isomorphism from G1 to H. And now you can
combine the isomorphism and from G0 to H with isomorphism from G1 to H to get a direct isomorphism from G0 to G1.The 
end.
We are able to extract the isomorphism. And therefore, we know that this was a proof of knowledge of an isomorphism.
Great.

The first application: Identity Theft

Why did I talk about proofs of knowledge?Because it gives us immediate corollary in our application. And that is
the first application that Fiat-Shamir proposed a few months after we wrote the paper about zero-knowledge for
identity theft. And they're saying, look, Alice wants to prove over the internet that she is Alice to Bob.Bob could be
Amazon, say. Over the net means something could be listening.But even more interestingly, suppose nobody was listening,
but Amazon had to store all those passwords in order to recognize Alice when she comes in. What if somebody breaks into
Amazon? You don't want those passwords in the clear.You don't even want those passwords encrypted because maybe the
encryption that Amazon does,one can do a birthday attack or a lot of other attacks that you can on a password file. 
Is it
possible that Alice can convince Bob she's Alice in a different mechanism without Bob actually being able to turn around
and convince someone else that they are Alice without a break in attack?And the answer is yes, zero-knowledge proofs
gives you the mechanism. 

Zero Knowledge: Preventing Identity Theft

Now we think about the password of Alice as knowing the proof of a hard theorem. So you can
think of Alice as someone who takes an x, squares it, calls that y. And says, hey, I know a square root of y mod n.
That's
a hard theorem. But whoever knows it, that's Alice. How does she convince Amazon, a mainframe, an ATM, someone who just
wants to know that Alice is the right person, but shouldn't really know Alice's proof for the hard theorem.
Zero-knowledge proof. So they would go through a few steps of interaction at the end of which it says, hmm, she knows a
square root. She just given me a zero-knowledge proof of knowledge. And that identifies her. So somehow it's possible to
verify that Alice knows the proof without knowing the proof yourself. 

Examples

It's not the only example of an application.But in
order to get many more applications, including applications in the realm of blockchains,we need to do one more thing,
and that is a big thing.We've seen the example that two graphs are isomorphic. We've seen the example that y is a
quadratic residue mod n.But there are lots of other languages. So let's ask a really big question.Do all NP languages
have a zero-knowledge interactive proof. Whoa, that would be amazing.But how are we going to do that? Are we going to go
for every single NP language and show that they have zero-knowledge proof?No.

Yes: All of NP is in Zero Knowledge

So in 1986, Goldreich, Micali,
Widgersonshowed that if one way functions exist, then every language in NP has a zero-knowledge interactive proof. Let's
dwell on the statement. There's a condition here. When we showed that graph isomorphism has perfect zero-knowledge or
quadratic residues of perfect zero-knowledge, there was no condition. Here the condition is that one way functions
exist.This is essentially the simplest condition or the simplest assumption that we use in cryptography.It will be
covered in the supplementary material. But for now, let's just assume that factoring is hard or discrete logs are 
hard or
bilinear maps or hard.That will be an instantiation of one-way function. And then they showed that for every language in
NP,there is a zero-knowledge interactive proof, a computational zero-knowledge interactive proof. It won't be a perfect
one, but it will be using the general definition of computational. There were two main ideas in the proof.The first key
idea it is to show that an NP, an example of an NP complete problem that has a zero-knowledge interactive proof. That
will be sufficient to establish that every language in an NP has a computational zero-knowledge interactive proof. 
Why is
that?Due to NP completeness irreducibility, if a language is an NP complete, then every string x can be reduced, let's
say if we're talking about the three coloring NP complete language, every instance x will be reduced to a graph G sub x,
such that if x is in the language,then the graph is three-colorable. And if x is not in the language, then the graph is
not three-colorable.That means that if I had a way now to have a zero-knowledge interactive proof of whether the graph G
sub x is three-colorable, it will also imply that I have zero-knowledge of interactive proof of x being in the language,
for every language, which is an NP. So what they showed in their paper is a zero-knowledge interactive proof for a
particular NP complete problem, the three coloring problem.And I'll show you in a minute how to do that. But they needed
one ingredient, and that is where the one-way functions come in. They needed, essentially, to use the one-way 
function to
get a primitive, cryptographic primitive, called a commitment scheme.And that is the second idea. So when we functions
imply actually a big commitment scheme.What's a commitment scheme? Essentially a commitment scheme or commitment
protocol is a pair of protocols, a commit protocol and decommit.A commit protocol takes as input an m. Usually, I want
to think of m as a bit, it's either zero or one.And essentially, metaphorically, puts m in an envelope, seals it so it's
an opaque envelope.There's a sender and a receiver. The sender commits, the receiver gets the envelope, can't tell
whether there's a zero or one being committed to it. Then there's a decommit protocol, where the receiver can actually
open the envelope and show--the sender opens the envelope and shows the receiver that what was in there was either zero
or one. The properties of these two protocol is that they satisfy hiding and binding. Hiding means that while it's
committed, you can't tell whether it's zero or one better than 50/50.And binding means that when you open the envelope,
you can't have committed to zero and open to one.Whatever it is you committed to, you are actually bound to it to reveal
it.

Properties of a Bit Commitment Protocol

We can go in a little bit more detail here talking about exact definition for hiding and that is that really the view
of the receiver when you commit to a bit B or a bit B prime is incomputationally indistinguishable. And binding is that
you are not able to decommit to two different values, B and B prime. What is an example of how did that get a big
commitment scheme? The simplest example is using encryption. You can think of commit as the sender essentially
encrypting the bit. If you want to commit to a bit B, you encrypt a bit B.And you can think of decommitting then as
giving the receiver either the decryption key or the randomness you used in order to encrypt the bit B. It's very
important that it will be a randomized scheme for hiding to hold because I really want to be able to hide very strongly
so you cannot tell apart whether what you've committed to is zero or one. And for that, you need a probabilistic
encryption scheme.

Theorem : is G3-COLORABLE

So let's go to the main act. And that is how do you show that a graph is three-colorable without
giving the coloring in fact in computational zero-knowledge? Having access to this commitment and decommitment
primitives.Here is the idea. So the prover, again, he knows all. He doesn't only have the graph, like the verifier and
the prover both have the graph. He actually has a coloring. So let's say he has a coloring of the vertices to red, blue,
and green. Or we can call these colors the zero color, the one color,and the two color. The first step what the prover
does, it's very different by the way, than the protocol swe've seen before. What he does now he picks a random
permutation, which is a step that's unclear why but we'll explain it in a minute. Rather than using the original
coloring, he takes actually a permutation of those three colors.So there are six permutations of that, like red could be
now blue, blue could be green, green could be red, or any of the other five possibilities.So you pick a random
permutation of those colors. And now you go to all the vertices of the graph and you recolor them, take the old
coloring and recolor it according to the random permutation that you chose.Now the graph is three colored. If the prover
is claiming a correct proof,there is a three-coloring and you just colored it again with a permutation of this
coloring.And now what the prover does is he commits to each of these colors by running a commit protocol.In other words,
he sends to the verifier a commitment to, for every vertex, it will be either a commitment to red, to blue, or to green.
The commitment means it's hidden. The verifier gets this, but he can't tell what the heck are the colors. What the
verifier now does is the following.He thinks to himself, well, either this is a proper coloring or it isn't. If it
isn't, it means that there's at least one edge in this graph that if you look at the two endpoints, they're going to have
the same color or maybe some other color altogether. But to be proper three coloring means that you only use red, green,
and blue.And for every edge, the two endpoints are different colors. So what the verifier says, I have no idea which one
of these edges is wrong. Maybe they're all correct. But I'm trying to catch the mistake.So what I'm going to do is I'm
going to select a random edge among all the edges. And I'll send it to the prover.And I'll say, you see this edge? I
want you to commit the colors at the endpoints of the two endpoints of this edge.And that's exactly what the prover is
supposed to do. He's supposed to, sort of, open the envelopes that have to do with vertex a and vertex b.And now there
is the edge a,b has been decommitted in some sense.The colors of endpoints. And the verifier, of course, if the
colors are not two different colors, he rejects immediately. Otherwise, it goes back to step one and repeats it 
again.And
after k iterations, maybe k's 100, if he never rejected, he never found an edge that has anything but two different
colors,he will accept. Let's analyze this.I will analyze it in the next slide. But I want you to think for a second
about this zero-knowledge aspect.What has the verifier found? One iteration they found the colors of a single edge.But
what about the second iteration? And someone asked me in class, maybe he can build up after 100 iterations or more,a
partial coloring or maybe the entire coloring, no. And that is why. Why?Because in step one, remember, I picked a random
permutation of the base coloring. Why did I do that?I did it so that even though I'm repeating this again and again and
again, each time selecting maybe different edges,the verifier is selecting different edges, the colors mean different
things. Whereas before blue meant blue, now when I pick a random permutation of the colors, blue might mean something
completely different. In fact, you can prove that these coloring sare uncorrelated between repetitions. OK. So we 
need to
prove that this is zero-knowledge.We need to prove completeness, soundness, and zero-knowledge in this.

Completeness and Soundness

Completeness,
what does that mean?If the graph is three-colorable, the prover, an honest prover can always convince the verifier to
accept.Yes, because you can always color it properly. And no matter what edge is being requested, you can always give
the proper color.What about soundness? If the graph is not three-colorable, now think about it.No matter what the prover
P star does, there is one edge there that's not properly colored.What's the probability that when the verifier chose
that random edge, he will actually hit on the wrong--on the edge that is not properly colored, pretty small. Maybe
everything is well colored except for one edge.What's the chance you get that edge? Well, the chance is one in the
number of edges.So the probability that after one trial, one iteration of this, the probability that the verifier will
accept when the graph is not three-colorable is pretty good. It's one minus one in E. That's not good enough.We want the
probability that he accepts to be small in this case. So repeat again. But how many repetitions?Twice won't be enough
because one minus one in E times one minus one in E, it's a little smaller than one minus one in E, but not much. But if
I repeat this the number of edges, number of times,then it will disappear exponentially. We will have one in natural log
to one in little Eto the number of edges. And that is an exponentially small probability. And we get this gap between
completeness and soundness.You will always accept, the verifier will always accept when the graph is three-colorable.
And you will accept with exponentially small probability when the graph is not three-colorable. Now zero-knowledge, as I
said, it's easy to see informally.It's messy to prove it formally. So how do we see it?At least let's give you-- I give
you some inkling of the proof. And let's do it for the honest verifier.

Honest Verifier Computational ZK

So the honest verifier competition zero-knowledge
works like this. This is the simulation. The simulation, again, works in a different order.Rather than first taking a
coloring and committing, how can he do that?The simulator doesn't know coloring. There's no way you can do that. Can't
even get off the ground. So what the simulator does is it chooses at random in advance the challenge of the honest
verifier, which is just a random edge. Then it chooses a bunch of colors,really don't matter, he can color the whole
graph in the same color, except for that edge that in the lucky execution, the verifier will ask him.That's the a,b
edge. And it colors it in two different colors, two different random colors. And what is the simulated view it
outputs?It commits to the transcript, which is a bunch of commitments. The commitments are not supposed to give
anything to a computationally bounded distinguisher because they're just commitments there or if you think about how we
implement the commitments,a bunch of encryptions. So we can't see anything. Then you give an edge the honest verifier
put the random edge.And then you have a decommitment transcript to those colors. And the decommitment transcript will
give two different colors to a and b because my commitment made it so that I essentially--the only colors that were
different were on that edge a and b.This is exactly a transcript. But is it?Not really. If you think about what
has been committed to is not a legal coloring. So this transcript is very different than what happens in the real
interaction. But it is computationally indistinguishable. And that depends on the hiding property of the commitment
protocol.

Computational ZK: Simulation for any Verifier V*

So what does the simulation look like?The simulation, which doesn't talk about honest verifies,but for every
verify, that's harder. It's here on the slide and I will leave it for the TAto discuss in the supplementary lecture.

Now, we have as many CZK examples as NP-languages

The
upshot of this. Now that we know that all of NP can be done in interactive--has an interactive zero-knowledge proof, it
means that we have many--many-- many examples which are interesting for us as many as there are NP languages.Obviously,
we can use this protocol also for the statements we already know perfect zero-knowledge for, but we can get a stronger
guarantee with perfect zero-knowledge. But the more interesting case is when we don't a perfect zero-knowledge protocol
and we have to go through this three coloring protocol. So an example.Any satisfiable boolean formula to prove that it
has a satisfying assignment can be done in zero-knowledge without actually giving the assignment. Given an encrypted
input E of x and a program, program, PROG,I can prove to you in zero-knowledge that if you ran this program on an x that
you only see the encryption of, you will get y.In fact, I can give you an encrypted input, an encrypted program, and
prove to you that if you ran that program on the input,you would get back y.

Protocol design applications

And that is without revealing the input or
the program.Why is that important? Here are applications. The first major application that they already noticed in the
original paper is a protocol design application. Essentially, this is a tool to enforce owners behavior in cryptographic
protocols without revealing any knowledge or information.The idea is the following. Suppose you take a protocol and
you've proved that if all players follow honestly the protocol steps, it's a safe, secure protocol. Now you run it 
in the
wild. The players may not follow the protocol.But you want to make sure that you can still use your security proof. What
do you do?You tell the players, OK, I want you along with every message you send to give me a zero-knowledge proof,a
zero-knowledge interactive proof possibly that the next message that you're sending that is the message you're 
sending is
what you should have sent if you were honest. In other words, it's what the protocol rules would tell you to send on the
history of communication so far and your internal randomness, r, and maybe some other internal inputs. How do you prove
that in zero-knowledge?Essentially, you commit to the internal randomness, you commit your internal secrets once and for
all when the protocol starts. And then every time you send a message, you attach a zero-knowledge proof that on these
committed randomness, on these committed private inputs, this is the right message to be sent.Why can this be done?
Because that is an NP statement. So if you think about the language,there exists some randomness such that the next
message is what is equal to the protocol on the history of communication in rand in fact r has been committed to, that's
an NP statement.Again, it's a mouthful. I advise you to mill over this. But it is an amazingly powerful
tool.

Uses for Zero Knowledge Proofs 90-onwards

Zero-knowledge has been used for many things. In the 80s, it was mostly, the two applications I already mentioned,
which is identity-- preventing identity theft and a tool for protocol transformation from honest to dishonest
players.But since then, it's been used in the context of computation delegation, if you want to delegate computation to
the cloud, but only give the cloud encrypted data. It's even been discussed as a tool for nuclear disarmament.That's a
very interesting application of the concept of zero-knowledge that actually nuclear physicists have been, at least about
10 years ago, there was a lot of work in this field.People have suggested to use it in the context of forensics to
prove, for example, that your DNA is not the DNA on the crime scene without revealing your DNA. But in the context of
this class and the huge boom that has happened to zero-knowledge, it's mostly started with a paper by BenSasson,
Chiesa,and others on how to do Bitcoin in a private and anonymous manner.So adding zk proofs in the context of
cryptocurrency. More recently, there's some work by Bamberger and Rebecca Wexler, and Ron Canetti, and Evan 
Zimmerman and
myself that shows zero-knowledge might be a very important tool in the context of the legal domain where there's many
verification dilemmas in the law that necessitate right now revealing a lot of information that you might not want to
reveal and zero-knowledge can be used instead. 

Complexity Theory: Randomized Analogue to NP

The last thing I want to say is that zero-knowledge has been not only
useful for cryptographic-type applications, but it's actually been, sort of, revolutionary in the context of complexity
theory.And in fact, it's not so much zero-knowledge, but really the concept of interactive proofs. So I'm going to spend
the last five minutes talking about that before we end the class today. So when we talk about what's efficiently
solvable, what's an efficient algorithm, we usually talk about P, polynomial time, things that run in polynomial 
time, or
things that run in polynomial time plus coins. When we talk about what's efficiently verifiable,we used to talk 
about NP.
But in this lecture, I suggested a new form of proof and interactive where essentially you take NP and you add
interaction and randomness on the part of the verifier.Notice that our verifier was pretty simple in the perfect
zero-knowledge examples. He was just choosing a coin and sending it over. And also in the NP three coloring
zero-knowledge proof,the verified shows a random edge. Is there something more sophisticated the verifier can do?Here is
an example. I'll show you an example of an interactive proof for a statement, which is not an NP statement, where the
verifier is doing something a little bit more than just tossing coins.And this will answer two questions at the same
time. One is can you interactively convince a verifier in polynomial time of statements that we don't know how to
convince using a classical, old NLP proof,just sending a witness? And the answer is going to be yes. And second of all,
is there something else that a verifier can do except for tossing coins. And the answer for the next minute will be
maybe.

Claim: G0 is Not Isomorphic to G1

Let me show you an example. Suppose I wanted to prove as a prover to the verifier that actually these two graphs,
which are different from the other graphs are not isomorphic to each other.Is this any different than the previous
painting, picture? Yes. I've added an edge here on the left graph, which is zero between seven and four and on the right
between four and ten. What adding this edges has done is we've maintained the number of vertices and edges. But it's no
longer true that these two graphs are important to each other.How do I prove that to the verifier? Think about it for a
minute.I can't give an isomorphism because they're not isomorphous. I guess one thing to do is to go through all
possible isomorphisms and to show one by one that neither all of them-- neither one of them works or none of them
work.But there are a lot of isomorphism. So that is going to take a long time. There's an exponential number of
isomorphism.And in fact, But I want to convince an efficient verifier. So even though I don't have a short
proof to send over like an NP type proof, I will show you how to convince an efficient verifier interactively that two
graphs are not isomorphic to each other so that completenes sand soundness hold, and also zero-knowledge actually. 

Graph Non-Isomorphism in IP

Here's
the idea.Let me fill everything in and then go through it.Step one, the verifier flip-- so the input is two graphs G0
and G1. And the claim is that they are not isomorphic to each other.There is no isomorphism that maps the vertices of G0
to G1. Step one, the verifier flips a coin zero, one.And he does that in order to select either G0 or G1. And he also
picks a random isomorphism, a permutation of the n vertices. And then he applies his isomorphism to either--to the G sub
of the coin. So let's say if the coin was 0, he applies at the G0. If the coin was one, he applies it G1.That gives him
a graph H, which he sends over to the prover. Now this graph is an isomorphic copy of G sub C. Notice that if the two
graphs were isomorphic, so it was an incorrect claim, this graph actually H is isomorphic to G0, but it also is
isomorphic to G1. How does a prover know which is the case?If the two graphs are not isomorphic to each other, and he's
an all powerful person, remember that's how we were thinking about the prover,he just examines whether h is isomorphic
to zero or G1 and he tells back to the verifier which is the case.If the verifier knows whether he took an isomorphism
of G0 or G1, if b is equal to his coin,he's happy. If b is not equal to his coin, he immediately rejects. He says, hey,
this guy couldn't tell whether it was an isomorphism of G0 or G1. He must be a liar. These two graphs must be isomorphic
to each other.I reject. However, as usual, he could have been lucky. He could have guessed the right coin.Even though h
is isomorphic to only-- to both G0 or G1, he could have guessed that the coin flip was zero. And convinced the verifier,
or at least not convince the verifier or left the verifier ambivalent.So the probability that he succeeds to do that is
going to be at most a half.We do this as usual, k times the probability that you will always get the result of the coin
of the verifier is a half the first time, a quartertwice in a row, and eight three times in a row and one into two to k,
k times in a row.So when the two graphs are isomorphic, you'll catch them. When they are not isomorphic, he can always
convince you,so completeness and soundness hold. But does zero-knowledge hold for this protocol?Let's think about it.
Even intuitively, before we try to do a simulation and fail, it doesn't.Why is that? Because the honest verifier, yes.
The honest verifier, no problem. But if the verifier was not honest,maybe he didn't just take a random H, apply it to
the G sub c, and send over H. If he was honestlydid that, all he finds back is the result of his coin which he knows if
it's what the coin was.But maybe he's a cheater. If he's a cheater, he might be sending Hs here that he just wants to--
he's finding out whether this graphH is as isomorphic to G0 or G1. So when this honest verifier is workingwith an honest
prover who's giving him, essentially he's telling him whether this new H isisomorphic to G0 or G1, this is knowledge
that I don't know how to simulate. And in fact, this is an example of a protocol,which is an interactive proof. It's a
nontrivial interactive proof. Like it convinces the verifier.We don't know how to convince the verifier of
non-isomorphism with an NP proof, but it's not zero-knowledge.We will need to modify it to be zero-knowledge.How do we
modify it to be zero-knowledge? The verifier essentially before the prover answerswill have to prove to the prover. So
now it's, sort of, a switcheroo.He's going to send them H and then he will prove to him that actually he knowsthat he
really did these steps. He really applied this isomorphism to G sub C.And it's beyond scope here, but there is a way for
the verifierto do that. What's interesting about this protocol is that it was very important for this protocolto work
that the verifier here did more than just flip a coin.He actually picked-- a flipped a coin to pick this random
numberand he didn't reveal to the proof or the result of his coin tosses. It's actually kind of interestingthat the
prover is the one who gives back b. But the verifier flips them coins in secrecyand then sends over H. If you think
about it, this actually is very similar to the example of the colorblindin the beginning of the lecture. The issue is
that it brings up a general question.And that is a question that came up around the same time that zero-knowledge paper
came.There was a proposal something called an Arthur-Merlin game by Babai and Moran, which is an interaction between a
proverand verifier, he called it Merlin and Arthur. The difference was that Arthur wasn't a probabilistic polynomial
time algorithm that tossedcoin and did computation. He was just a coin tosser. He threw coins, get back, threw coins got
back.This was the case actually in the perfect zero-knowledge proofs that we've seen also in the three coloring case.But
it was not the case for this last example that I showed you.And the question was asked, is it really the case that maybe
you can prove more theoremslike non-isomorphism if you let the verifier Arthur hide his coins?Or in other words, is IP,
interactive proofs, more powerful than Arthur-Merlin, what they calledArthur-Merlin games? Is the privacy coin necessary
in order for the--we were to convince statements which are not in NP?The answer was no. Actually, you can take any
interactive proof like the one we just showed for graph and isomorphismand turn it automatically to a system where the
author or the verifier only tosses coins.It turns out that this transformation is such that it makes it so that even if
Merlinwas efficient to begin with, he will become inefficient. But again, this is a complexity course.There are lots of
other questions people asked and that was how exactly powerfulare interactive groups? So you can do graph and
isomorphism. Can you do more than that? The answer is that you can do actually a lot more than that.But before I show
you that, I want to say that protocol is where Arthur or the verifier,is only a coin tosser, a very interesting protocol
in practice because it has been suggested by Fiat and Shamirin a paper on-- suggesting something called a Fiat-Shamir
paradigm or at least since then, we call itthe Fiat-Shamir paradigm is that when you have a protocol where the approver
is sending messages,but the verifier always doing the sending coins, you could possibly get rid of interaction.Now
getting rid of interaction is a big one. If we can transform all this to like the prover just sending a string, that
would be amazing.How could you get rid of interaction. The suggestion of Fiat-Shamir was this.They said, let's assume
for a minute that we had access to some H, big H whichwe think of as a cryptographic hash function. Again this is for
the supplementary material. For the purposes of my lecture, let's justthink of H as a random oracle. What does that
mean? H, basically, I can apply it to a string and get random coins.Something that really looks unpredictable. Then if
such an H existed, what the prover can do is say,well, there's some interactive proof. And let's say we prove
completeness and soundness about it, what I can do instead of really interacting, sendingA1, getting back coin, sending
A2, and so forth, what I'll do is I will send you a string, which is my first message A1and instead of waiting for your
message with coins, I will, by myself, apply big H, this hashfunction to my own message. And since I'm told this H
really just takesthe message and outputs something that looks random, I will now view this as your question, your coin
questionand answer that. And this transcript rather than A1 coins A2,its A1, the result of applying the hash function to
A1, A2 should be just as good.And the verifier can run his decision procedure on this history rather than on a true
interactionand then decide it to accept or reject, it should be satisfied completeness and soundnessin the same way as a
real interaction did. A lot of people use this Fiat-Shamir in practice, this paradigm.It's heuristic. Why do I say it's
heuristic? Because we don't really have such cryptographic hashfunctions that take a string and give me something at
random. That is an idealization. It's called a random oracle model.But it is used in practice all the time. What you can
say that if h is behaving like a random oracle,then completeness and soundness twofold. Warning, this does not mean that
all interactive zero-knowledgeproofs can be made non-interactive. Even though IP is equal to AM, it's not truethat all
interactive proof protocols where the verifier hides his coin can beturned into zero-knowledge interactive proofs where
Arthur doesn't hide his coins.But it can benefit many protocols. And just one other thing is noticethat what I did here
in this slide, I looked at a case where the first message is from Marylyn,the second message is coins. But in some of
the protocols we've seen, the first message is actually from the verifier.Then how do you make that non-interactive.
Well usually what happens is--and that is going to be used in the course extensively, is that we will post the first
message coins as, sort of, a publicly chosen randomness for allto see. And then apply the Fiat-Shamir heuristics to get
non-interactive proofs.The notion of interactive proofs has been really a catalyst for complexity theory.Because it was
the first time that we really decoupled correctness from the knowledge of the proof.And it enabled people to ask a lot
of new questions about the nature of the proof. These questions have been asked and some of thembeen answered for the
last 30 plus years. And it's leading up to actually current research on provablyoutsourcing computation and some
research in quantum computation, some highlights.Well, classically, before interactive proofs, the notion of efficient
verificationwas NP, that is that there exists a solution. So I just send you the solution. And you as a verifier check
it.We didn't know how to verify whether Co-NP statements werecorrect, like to do graphs are not isomorphic to each
other, Co-NP are the complement to NP languages.To count how many solutions are there to a statement. So for example, if
you have a Boolean formula, how many--and you want to find out does there exist a solution, that's an NP statement.
There's no solutions, that's a co-NP statement.There are exactly 37 correct solution,that's what's called a sharpie
statement. We don't know how to convince the verifier of that efficiently using an NP proof.Or even a more complex
statement where you have an alternation of quantifiers like for all x, there exist a y such that for all x2 the exist a
z,and so forth. We have no idea how to convince a polynomial of time prover of such statements.However, if we use
interactive proofs, it turns out we can. So just by adding interaction and randomness,it has been shown in an amazing
paper by Fortnow, Karlof, Babai, Lund Nissanand then by Shamir, that you can convince a polynomial timeprobabilistic
verifier with a very powerful prover, by a polynomial number of messagesthat even statements in P space can be proved
using an interactive proof.Not only that, but people have thought they said, well interaction helps, coins help, maybe
there'sother ways to define probabilistic proof system. And in fact, in a joint paper with Benor, Killian, Widgerson,we
came with one such statement. And we said, one prover, we we're able to do p space, what if we add another one.So to
begin with, you say why would one-- two be better than one? I mean, they're all powerful, what does that add?The idea
was that we will let these two provers, this one will interact with the verifier. And this one will interact with the
verifier,but they won't see each other's messages. And we likened it as if there was an interrogation of these two
provers like interrogatingsomeone in the crime. What's the crime? There's a claim. If the claim is true, there is no
crime.If the claim is false and he's trying to convince you that it's true, there is a crime. There's a bug in the
proof, you're trying to find it.And we were able to show indeed that if you use this kind of proof system, you can
getunconditional zero-knowledge. So perfect zero-knowledge for all of NP.But more interestingly, it turned out that in
some incredible sequence of events,it was shown that two provers can actually convince you of even more statements than
P is based.The kind of intuition is the power of two provers which are in different interrogationrooms is that you can
catch inconsistency. So they have to be consistent for you to accepttheir proof of a claim. And catching inconsistency
is an incredibly powerful device.And in fact, it's been shown you can even convince a polynomial time verifier of
non-deterministic exponential time statements.This has led to incredible theorem called the PCP theoremsaying that even
if you stuck back to NP statements, back to the usual good old NP statements where you haveshort witnesses for, there is
a way to verify them being correct with very high probabilityby only reading a constant number of bits of the proof. So
this is like going somewhere completely different. But it is a result of interactive proofsbecause we are allowing the
verifier to make an error. We are allowing him to toss coins and what has been shownis that by coming up with a very
different mechanism for writingproofs down, you could write them in such a way that you could only need to read a few
random locations in orderto find an error. It's another way to think of a two-prover proof system. As I said, it had an
impact on quantum computing.And one of the beautiful results there is the result of some people from Berkeley, Umesh
Vaziraniand others. And that is how do we know that a quantum computer is actuallyusing quantum power if we only have
classical powers? And what they showed is a way to take,essentially, a claimed efficient quantum computation, two
copiesof it, likening the two provers, make them sit in separate rooms, but be entangled and showhow you could convince
a classical verifier of the correctness of the computation by choosing coinsand by using entanglement. And then this
leads up to something very, very recent showing that actually, if you have two provers, sonot necessarily efficient
quantum computers, but two quantum computers who might be taking a long time,they can convince a classical verifier of
languages,which are all they recursively enumerable languages. So this is, kind of, an amazing statement and it's an
amazing theorem.There's a lot of buzz around it today. All right. Thank you.
