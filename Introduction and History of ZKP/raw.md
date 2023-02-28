
SHAFI GOLDWASSER: Hi, everyone. I'm giving the first lecture in the course on zero-knowledge proofs. And my lecture will be an introduction
0:06
to zero-knowledge interactive proof. And I'm very happy to be co-lecturing with Don
0:12
Boneh, Dawn Song, Justin Thaler, and Yupeng Zhang. So we're talking about proofs. Let's start with classical proofs.
0:19
So when we think of a classical proof, we think about these various esteemed provers, Gauss, Euclid, Emmy Noether, Alan Turing,
0:27
and our own, Steve Cook. And we think about theorems, the kind of theorems that you learn perhaps in geometry in class
0:33
where there's a bunch of axioms, there's a claim that you're trying to prove or theorem, you make a sequence of derivations from the axioms
0:40
and then eventually you declare the theorem as proved. It could be the prime number theorem,
0:46
the Pythagorean theorem, and so forth. But today, we're going to think of proof
0:51
as an interactive process where there is the prover. But maybe more importantly for our study, there is a verifier.
0:58
So there is an explicit reference to whoever it is that's reading the proof and verifying it is correct.
1:04
And we think about this as follows. There's a claim, which is an input to both prover and the verifier.
1:09
Both of the prover and the verifier are actually algorithms. And the prover sends a string, which we will refer to
1:16
in this slide as a proof. The verifier reads this. So if you would like to think about that geometric proof,
1:22
verifier is the teacher reading your proof and at the end accepting is it correct or reject. Accepting the claim as being proved or not.
1:31
In fact in computer science, we often talk about efficiently verifiable proofs or NP proofs.
1:38
And those are proofs where the string that the prover sends
1:43
to the verifier is short. And the verifier, in addition, doesn't have all the time
1:50
in the world to read it, he has polynomial time. Now to be more explicit, what does it mean by short?
1:55
What do we mean by polynomial? What we mean is that the string that the prover sends
2:03
to the verifier is of size polynomial in the length of the claim. So we think about the claim as string x, binary string.
2:10
The message here is string, binary string w, the length of w is polynomial in the length of x.
2:17
So if it takes 100 bits to describe the claim, w's lengths would be polynomial in 100.
2:23
And the verifiers time is also polynomial in the length of x. So it could be linear, just the length
2:30
of x, quadratic length of x squared or the length of x, even to 100, as long as it's a polynomial function.
2:36
Again, the verify is an algorithm. Takes as input both x, the claim, and w, the proof string,
2:43
does some processing. And at the end decides what to accept or reject. We often say either accept or one.
2:49
And when we say reject, it's either zero or reject. I'll use those interchangeably.
2:54
What are some examples? And these are going to be important examples for the duration of the class today.
2:59
One example might be of an NP proof in a claim is that the prover is trying
3:05
to convince the verifier that a particular number n is a product of two large primes. This is an interesting claim because the verifying
3:13
polynomial time, we don't know the procedure for it to be able to convince himself that n is
3:18
a product of two large primes. So we need the help of a prover. Perhaps an all powerful prover. Certainly more powerful than polynomial time.
3:25
Again, for this portion of the class, I don't pay any attention to how much time it took the prover
3:31
to come up with the proof. All the attention is going to be devoted to how much time it takes to verify a proof once it's sent.
3:38
Later, we will dedicate our attention to the kind of claims that can be proved by a polynomial time
3:46
prover who knows maybe some extra information, which enables it to convince the verifier of the correctness
3:52
of the claim. So for now, let's go back to n is a product of two large prime. What's the proof?
3:57
Since the proven time might take a long time, we don't care about that. We just take attention to how much time
4:04
it takes to verify the prover just factors in, let's say the two prime divisors are p and q,
4:09
sends it over to the verifier. What does the verify have to do? Is to multiply p times q and see that it gets n back.
4:16
Multiplication is an easy operation, polynomial time. And he has to check that p and q each of both primes.
4:22
And that's also an easy operation we know how to do in polynomial time. And if that's the case, he accepts. Otherwise, he rejects.
4:29
So after this interaction, what does the verify really know? He knows the claim is true and is
4:34
a product of two large primes. He knows something extra. He knows the primes themselves is actually more
4:40
than was necessary in order to convince yourself that n is a product of two large primes or is it?
4:46
Is there some other way to do that? We will see in a couple of slides that there is.
4:51
But let's look at a few more examples. Second example. Now the prover is trying to convince the verifier
4:58
that a number y is what we call a quadratic residue mod, a modulus n.
5:04
So the input to do is to prove and verify is a pair y and n.
5:10
And the claim is y is a quadratic residue mode n. What does it mean to be a quadratic residue?
5:15
It means that if you look at the equation y is equal to x squared mod n, it's solvable.
5:22
That is, there exists an x and it's an x that's essentially between one and n.
5:28
And furthermore, it's what we call relatively prime to n. So there is no divisors in common between n and x.
5:36
That's a solution to this equation. So there is an x such that y is equal to x squared mod n.
5:44
And what would be the proof of that? Well, maybe the verifier can do it himself. It turns out that this is very hard problem.
5:50
So it's hard, for example, to find the square root of y mod n because if it was an easy in polynomial time,
5:57
the verifier would need the prover. How hard is it? It's as hard as factoring n, a well-known hard problem
6:05
for classical computers. But the prover as we said, he's all powerful. Or she in this case.
6:10
So she finds out an x, sends it over to the verifier. The verifier squares mode n, compares
6:17
to see if is equal to y. And if so, it accepts. Else, it rejects. Again, it's an empty proof. There's a short string x that will convince the verifier
6:25
to accept when the claim is correct. What happens after this interaction? The verifier is convinced that indeed there
6:32
exists an x such a y is equal to x squared mode n. But he also knows x. He knows the square root of y.
6:38
Last example before we start defining this more generally. Here, the claim doesn't talk about numbers.
6:44
It talks about graphs. There are two graphs. Turns out if you look more carefully in these two graphs, they are actually isomorphic to each other.
6:52
In plain English, that means they are the same graph, but drawn a little differently.
6:58
And formally, it means that there's a mapping from the vertices of the graph of the left to the vertices of the graph on the right
7:04
so that if you take this mapping which we call the isomorphism pi from numbers one up to 10 on the left the numbers one up
7:14
to 10 on the right, vertices are from the left to the right, it will be the case that essentially the one
7:22
on the left, if you map it to-- with the isomorphism to a vertex on the right,
7:29
let's think of it as one, similarly, the two on the left to the two on the right,
7:34
if there is an edge between the one and two on the left, there's also going to be an edge between the vertices
7:41
that these two are mapped to on the right. And that's true for every pair of vertices. That means that these two graphs are isomorphic to each other.
7:50
And that pi is an isomorphism. So how hard it is to describe how long is pi?
7:57
Is it polynomial size and the size of the graph? Yeah. Essentially, the signs for every vertex
8:02
a name on the edge of the graph. And that's just essentially, if there are n vertices,
8:08
it's length n. And how much time does it take the verifier to check it? He has to go for every pair of vertices on the left, check
8:14
if there is an edge between them on the left is also an edge between where they were mapped on the right. And if there's no edge between them on the left,
8:21
there should be no edge between them on the right. After the interaction, the verifier
8:26
will believe that two graphs are isomorphic, if you got a good isomorphism, but they also knows n isomorphous.
8:32
So all of these examples are examples of NP proofs.
8:39
Now of course, we are not interested in a particular number n or a particular number of y, or particular pairs of graphs.
8:44
We we're interested in the problem more generally. And we call this a language, that is all the n's
8:51
which are product of two primes. That's the language of composite numbers, which are product of two primes or all the y's in n pairs,
9:01
such that y is a quadratic residue mod n. In other words, we're interested in languages. Formally, a language is just a set of binary strings
9:08
x that satisfies some property. And an NP language is defined to be,
9:15
and this goes back to cooking. And the completeness is defined to be those sets of strings
9:22
L is an NP language if there is some verifier v who runs in polynomial time, polynomial in the length
9:30
of the x, such that both, two conditions hold. And that is completeness and soundness.
9:37
What does it mean that completeness holds? It means that when x is in the language, if you're talking about a claim or in the example,
9:43
it's the or opposite numbers, when the language is a language of opposite numbers, which are product of two primes
9:50
and were given such an n, then there has to be a poly log proof of witness w,
9:56
the proof of consent to the verifier, such that the verifier examining x and w will accept.
10:03
But completeness is not enough. We also need soundness. And that is to make absolutely sure that when x is not in the language, for this example,
10:10
n is not a product of two primes, then there is no witness that will convince the verifier to accept.
10:15
In other words, for all strings w that the prover may send to the verifier,
10:20
the verifier will reject. So we usually talk about completeness
10:26
allows honest provers to convince the verifier. Soundness ensures that regardless of what a cheating
10:33
prover is trying to do, he will not be able to convince you the correctness of an incorrect claim.
10:40
But our question in this course is not about NP or NP completeness. But rather we're asking is there some other way
10:47
to prove these type of theorems? Can a prover, for example, convince a verifier
10:52
that y is a quadratic residue of n without sending a square root. So this is the question that motivated
10:58
Silvio Micali, Charlie Rackoff and myself to study zonal truths in the early 80s.
11:04
And this is a process that took about three years. And the answer is yes.
11:11
And the main idea, even without getting into the mathematics, is the way that the prover will convince the verifier
11:17
that the claim is true without giving away the NP proof,
11:22
in the example of the square-- the y is a quadratic residue of n without giving you the square root,
11:28
is to prove instead that I could prove it, if I felt like it. So I'm not going to prove it to you.
11:34
But I will prove that I could prove it. And somehow being able to prove that I could
11:41
will imply that at the end, the verifier will be convinced
11:47
and yet he will not know a square root, he will not know the factors of n, he will not know an isomorphism.
11:53
In fact, he will get zero-knowledge in addition to the fact that he claim is true.
11:59
Of course, we will need to define what it means to be zero-knowledge precisely. So before we define it, I want to give you
12:07
an idea of how possible you can prove something is a square root or that two graphs are isomorphic
12:13
and so forth without actually giving that as isomorphism or giving you the square root. And I'm going to start just letting
12:20
you know that this is no longer going to be a prover sending a string w to a verifier.
12:26
We're going to need to change the proof model. We're going to need two new ingredients. One of them is going to be interaction.
12:32
Rather than the verifier just passively reading the proof, he's going to have to be engaged in a non-trivial interaction
12:38
with the prover. So like you see in this picture, there will be messages going back and forth, prover sending a message to the verifier.
12:45
Verifier answers back, back and forth, back and forth. Might be three steps, might be two steps,
12:50
it might be length of x steps. But it will be polynomial number of steps, you'll be more than a single message from prover
12:57
to verifier. Later on in this class, we will see that there is a way to remove much of this interaction.
13:06
There will still be, in a sense, at least a single message from prover to the verifier
13:12
and some preliminary stage. But for now, we have interaction.
13:18
Interaction is not enough. We also have randomness. What do we mean by that? We mean that the verifier is not just
13:23
going to be a deterministic algorithm, evaluating what he received from the prover. He is actually going to be allowed to toss coins
13:31
as a primitive operation. And his questions to the prover will
13:36
depend on the result of tossing these coins. Another way to say that is that his questions are somewhat
13:42
unpredictable because if they were all predictable, the prover could have anticipated them and just
13:47
sent him the one string W in advance. But since they are unpredictable,
13:54
after the prover sends a message, the verifier may ask depending on its coin tosses, many different options.
14:00
And the prover is supposed to be able to respond to all of them. What is inherent in the fact that the verifier tosses
14:08
randomness is that we're also going to be willing to accept a small probability of error.
14:14
What does that mean? We will get to the formal definition in a few minutes. Informally what that will mean is
14:21
that we whereas in geometry class, when you gave the teacher a proof, they checked it.
14:28
And it was supposed to be 100% correct. We are going to have as a formal part of the model,
14:37
allow a small probability of error. But it's going to be quantified. And you're going to have to be able to show that your error is
14:45
smaller than one over-- I don't know, Avogadro's number or a negligible error. We'll get to that in a minute.
14:51
For now, the proof model is changing. Its interactive. It's probabilistic, meaning the verifier can toss coins.
15:00
That means that there a lot of possible interactions that will come up between prover and verifier. So there are a lot of possible executions.
15:07
It's still going to be the case, they both get input, which is the claim. And at the end of this question answer period,
15:15
the verifier will take the history of the interaction, the coin tosses that he's made, run an algorithm
15:21
and decide whether to accept or reject. Let's look at the first example.
15:26
The first example is not going to even be mathematical. But it will be something from the physical world.
15:34
The claim here will be that this particular page right in front of us has two colors rather than
15:40
a single monochromatic color. And the scenario that I would like you to keep in mind is let's say the prover can tell colors apart,
15:47
but the verifier is colorblind. And the prover is trying to convince the verifier that this particular page has two colors.
15:54
He's not going to enable him to see colors for the future. So in some sense, all he's going to convince
16:01
him is that this page is two colors and nothing else. So in that sense, it will not be transferring to him anything
16:08
beyond the claim. How? So here's the first step.
16:13
The first step is the verifier uses his coin, flips the coin. And with the following idea.
16:20
If the coin lands on heads, he takes the page
16:25
and flips it over. And if it lands on tails, it doesn't change the page at all.
16:31
Let's assume that he tossed the coin and indeed it was heads. So he flipped the pages so that what
16:38
earlier was purple in the top now it's on the bottom. And now he does this in the privacy of his own home,
16:44
not showing the prover of the results of his coin. But what he does is he sends the coin the page over to the prover.
16:51
The prover now looks at this page. He knew what the page looked like before and he's now sees what the page looks like now.
16:56
Since the prover can distinguish colors, he can tell whether the coin landed on heads or tails,
17:02
right? And indeed, that's exactly what he says. He sets out, he checks whether the page was flipped or not, he
17:10
writes the value of the new coin, coin prime, to be head if it's flipped, tails otherwise,
17:17
then he sends back coin prime. He says, listen, I think you tossed coin prime.
17:22
The verifier-- the rule right now is that the verifier, if indeed the coin that the verifier
17:28
tossed is equal to the coin prime that prover thinks he tossed, he says, well, hmm,
17:35
it looks like the prover could tell whether the page was flipped or not.
17:41
But he couldn't tell if he was only a monochromatic. So there must be two colors on this page. I accept the claim's true.
17:48
Of course, if the coin that he sent over is different than what if flipped, he says, well, he couldn't even tell that he flipped it.
17:53
There's certainly not two colors there. I reject. Let's try to analyze this for a minute. Clearly, if there are two colors and the prover
18:01
follows this procedure, then the verifier will always accept because the coin prime will always equal the coin.
18:07
If there is a single color, the prover cannot tell whether he flipped or not.
18:12
He could still try to guess he's a cheating proof, whether the coin landed on heads or tails. And he has a 50/50 chance of guessing correctly.
18:20
So the probability that he sends the correct coin is a half at most. And if the verifier accepts in this case,
18:27
the probability of the verify accepts incorrectly because perhaps the prover was lucky, but there's a single color on this page is 1/2.
18:36
So if there are two colors, he will always accept. If there's a single color, the probability accepts is less than half.
18:42
There's a gap between them, but you might not like these odds. Say what, I'm going to accept incorrect statements, claims,
18:49
with probability 1/2? No worries. You can repeat this process again and again. Each time, the verifier tosses a new coin,
18:56
decides whether to flip or not, sends the result, and so forth. And now, what is the chance that the prover, in case there
19:03
is only a single color, so it's not correct claim, is able to provide the verify each time
19:10
with a correct coin he tossed? It's 1/2 the first time. It's 1/4 to be able to do this twice in a row.
19:17
It's 1/8 to do this three times in a row. And it's 1/2 to the k if you repeat this k times.
19:23
So the probability that the verifier accept after k iterations of this is very, very small.
19:29
So what has happened here? I was able to convince a colorblind verifier
19:35
of whether a page has two colors or not so that he always will accept when they're two pages.
19:40
And he will accept that there's two pages incorrectly with extremely small probability.
19:49
Let's see this again. This idea, a little bit different of using interaction
19:55
and randomness to be able to convince someone of this time, a mathematical statement
20:01
without transferring sort of the obvious NP proof over. So the next example is the example that we started with.
20:09
And that is the input to the prover and verifier are the pair n and y such that there exist an x such that y
20:17
is equal to x squared mod n. Or is it the proof is trying to convince the verifier that indeed this pair n,y is a member of this language,
20:25
the QR language, the quadratic residues language, those y's such that y equals the x squared mod n for some x.
20:32
How would you convince the verify of this case without giving him a square root? Here it goes.
20:38
The prover as a first step chooses a random value one r between one and n. In fact, to be absolutely correct,
20:45
this r is supposed to be between r and n and have the greatest common divisor with n,
20:52
which is one, meaning there's no common divisors between r and n. For those who don't want to really dwell into this, let's
20:58
just think of it as a random number between one and n. And then what he sends to the verifier is r squared.
21:06
Doesn't send r, he sends r squared. And let's call it s, sends s. And he says to him, listen, if I gave you both square root of s
21:15
and a square root of s times y where y is the input, then you would be convinced that the claim is true
21:21
because if s has a square root, and s times y has a square root, then also y itself has a square root mod n.
21:28
But if I did that, that's like sending you a square root of s would be r. Square root of s times y would be r times x, then you
21:35
would know a square root of y. You would know x, just take r times x divide by r. And the whole point here is I don't want to give you both.
21:44
So what I'm going to do is I'm only going to give you either square root of s or square root of s times y.
21:49
But I want to convince you that I could have given you both the square roots. And the way I convinced you is I tell you, you get to choose--
21:58
you can choose to get a square root of s or square root of s times y, your choice. And I will be able to answer either question.
22:04
But I'm only going to answer one. Now if the verifier is smart, the way to choose which he wants is going to be to flip a coin.
22:14
Not to decide this deterministically, but flip a coin. So then with 50/50 chance, he will,
22:20
in case the prover is cheating, ask for an equation that the prover cannot solve.
22:26
Why? Because if the prover is cheating, he cannot solve both finding a square root of s and a square root of s times y because in that case is not cheating.
22:34
So the fact that he can do both means he's not cheating. I will flip a coin as a verifier to choose a challenge.
22:43
Hey, give me square root of s or hey, give me a square root of s times y. He's supposed to do that.
22:48
So my coin turned out heads or one, the prover is supposed to give back the square root of s,
22:54
which is r. And if the coin was tails, he's supposed to give the square root of s times y, which
23:01
is r times the square root of y or r times x, that's the square root of y.
23:06
The verifier checks that he got the right answer. So he will accept only if indeed when he takes what he got back
23:12
and squares it, he will get back an answer for what he asked for. So if it was heads, he asked for square root of s.
23:20
In that case, it's s times y to the zero, just s. And if he asked for tails, he wants the square root
23:25
of s times y. Let's analyze this. Again, if the claim is true and the prover
23:32
acts according to the protocol, the verifier will always accept because the proof can always give the square root of s and the square root of s times y.
23:39
Again, prover's all powerful. He knows the square root of y. He can because he's all powerful.
23:45
In fact, that's the only thing he needs to know. But what happens when the claim is false? And this is always the thing that's harder to show.
23:53
If the claim is false, then no matter what the prover does,
23:58
the probability that he will be able to solve both equations, he can't solve both equations.
24:04
He can solve one of them. So what's the probability I asked him to solve the equation that he knows how to solve. It's at most 1/2.
24:09
Again, maybe a half is not enough for you. Repeat this 100 times and the probability that the verifier
24:18
can 100 times be so unlucky as to choose exactly the equation
24:23
the prover can solve and not the other one which he cannot solve in the case where the claim is false, is going to be vanishing within a number of trials.
24:31
1/2 if you try once, 1/4 if you try twice, 1/8 if you try a third time, and 1/2 to 100 if you go 100 times.
24:40
And if you want it to go k times, it's 1/2 to do the k. So what happened here?
24:47
I can convince the verifier to accept when the claim is true.
24:53
It's very, very unlikely I will convince the verifier to accept when the claim is false.
24:58
And I never, if you think about it, transferred the square root of x because every time
25:03
I just give him a random r, which is a square root of s, or a random r times the original x or the square root of y.
25:13
Random times of the square root of y is random when you reduce it to mod m. So it gives, essentially, I'm sending him
25:20
random numbers which are independent of each other, even if I repeat this 100 times because each time I start again
25:26
with a verify-- with a prover choosing a new r. So what made this possible?
25:31
Here's one intuition. There's lots of possible execution. So there's lots of possible interactions or proofs.
25:38
And the prover essentially chooses one of those many possibilities in the first step.
25:45
When he sends r squared, he's, sort of, choosing one of these many possibilities at random. And each and every proof of these many random proofs
25:55
is made of exactly two parts. One part is when I asked to see the square root of s and one part is when I asked to see
26:01
the square root of s times y. Seeing either square root of s or the square root of s times y
26:07
gives nothing. If the verifier could have seen both, it would imply 100% correctness.
26:13
And the verifier chose at random which of these halves he wants to see, the square root of s
26:18
or the square root of s times y. The ability of the prover in principle to provide either part or convinces the verifier
26:26
that the prover could have answered both and therefore the correct-- the claim is correct.
26:32
Let's define this precisely. All right. So we have p and v, there an interactive proof
26:41
for a language, for a set of statements. If, again, v is polynomial time, but this time probabilistic
26:47
polynomial time, and there's completeness and soundness. If the claim is true or x is a member of the language,
26:54
the verifier will always accept. And soundness now has been modified.
26:59
If x is not true, the claim is incorrect or x is not a member of the language, then for all cheating prover strategy,
27:06
no matter how hard they worked, the verifier will not accept with negligible probability, like the one 1/2
27:13
to the 100 or 1/2 to the k, 1/2 to the length of x.
27:19
Let's introduce a little bit of notation. So this is a-- sorry, this is a cheating prover.
27:25
Every cheater proof of strategy will only help the prover to convince the verifier
27:31
with negligible probability. So a bit of notation. We use the following notation.
27:37
We talk about the probability that pv, so open paren, pv,
27:42
closed paren on x except in the case of x equal to L, x is an L, completeness is probability one.
27:50
In the soundness case, we say that for all cheating provers P star, the probability that P star interacting
27:58
with V on input x, the probability that accepts is negligible. What's a negligible function of length of x?
28:05
That's a function that grows slowly than any one over polynomial.
28:12
So wanting to do the length of x is an exponentially small
28:17
function. So it's smaller than one over polynomial for any polynomial. Interestingly, if you step back and you think to yourself,
28:27
is this reasonable to call this an interactive proof? I claim that this is ultimately what a proof is.
28:32
It should convince the verifier of correct theorems. And it should not convince them of incorrect theorems.
28:39
If you only are managing to convince him with a probability that is so small that in one
28:45
in the lifetime of the universe, it's not going to happen, it's good enough for me. And that is ultimately what a proof should be.
28:52
It should convince you of correct theorems and not convince you of incorrect theorems. And an event that will take time in one
28:59
in Avogadro's number, one in the lifetime of the universe of convincing of an incorrect theorem essentially
29:05
never happens. All right. By the way, interestingly, is that when you have an exercise, a homework,
29:11
and you're coming up with an interactive proof, sometimes, it's going to take a lot of work to get you to have verify,
29:20
always accept correct theorems and not accept correct theorems with negligible incorrect--
29:27
and accept incorrect theorems with negligible probability. You don't have to work that hard.
29:33
You just have to show the completeness holds with probability c and soundness does not hold, at most holds
29:40
with probability s for c and s which are a polynomial apart.
29:46
So this will be equivalent to achieving probability one for c, and negligible for s.
29:51
This can be shown in some standard technique of using repetitions.
29:57
So we define what an interactive preferred language is.
30:03
We also can talk about the class of all languages that have interactive proofs. And in the same way that we talked about NP
30:10
as being all those languages for which there is an NP poof, we will talk about IP as all those languages
30:17
for which there is an interactive proof. Again, the proven runtime might be very slow. But the verifier has to be polynomial time,
30:25
probabilistic polynomial time. All right.
30:30
We have defined what an interactive proof is. But what about zero-knowledge?
30:36
How do we define zero-knowledge? What is even the intuition of what should be zero-knowledge? So here is the intuition.
30:43
I want a zero-knowledge interactive proof to be the kind of proof such that whenever the statement is
30:49
true, then the verifier goes through a proof,
30:54
interactive proof of the prover. And at the end, he's convinced with high probability that the claim is true. But in addition to that, he has a history of interaction,
31:02
he has the coins that he's tossed. Maybe you've given him so much during this interactive proof
31:07
that now he can compute a lot more than he could compute before. So for the example of the n, proving
31:14
that n is a product of two primes, perhaps after the interactive proof, he can factor a number or compute a square root or find an isomorphism.
31:21
We will say that the interaction was zero-knowledge if what the verifier can compute after the interaction is
31:29
essentially the same of what he could have computed before, namely the interaction has not increased
31:35
the computational power or allowed the verifier to compute more than he could have computed before.
31:42
Furthermore, we want this to be true, not just for the honest verifier who follows the protocol, but for any verifier, even in a devious malicious, adversarial
31:53
verifier. This slide is an intuition. How do we mathematically capture this?
31:59
Let's try. Again, we're going to do this slowly.
32:05
So first of all, I want to say that this verifier has some sort of view. And I want to--
32:11
so he's learned that after the interaction that the theorem is true with high probability. But he's also gotten a view.
32:17
And that's the transcript of the answers and questions plus the coins he tossed. We will define this formal variable,
32:24
which is view sub v of PV on x. And that is a random variable.
32:30
What I mean by that is that there's a lot of possible values that this variable can get.
32:36
And this is a probability, if they're distributed over the coins that v and p both tossed. Remember, let's say in the example of showing
32:45
that y is a quadratic residue, the prover tossed coins selected r. The verifier tossed coins to select
32:51
whether he wants to see the square root of r squared or the square root of r squared times y.
32:56
So those are all possible executions, these are all possible assignment that this variable can get.
33:02
OK. So this is a verifier's view. I will say that this view gives the verifier nothing new
33:12
if the following is true. And this is called the simulation paradigm. This is-- the simulation paradigm
33:18
is started with the concept of zero-knowledge. It's used all over cryptography today. What is the simulation paradigm idea?
33:26
We say that the real view, so if we look at this blurb or this great blurb
33:31
that I call real view, which is essentially, this is a probability distribution, the points
33:38
in this space are all the possible histories of interactions between prover and verifier plus the verifier's coin.
33:44
I say that this view gives the verifier nothing new if he could have actually simulated it on his own,
33:55
sitting with his laptop or his computer at home, not talking to any prover, he could have come up
34:03
with a simulated view. So this is again a probability distribution. You can essentially sample these simulated views himself.
34:12
And what has to be true about the simulated view in terms of relation to the real view is that if there's someone
34:17
else out there, like let's call him the polynomial time distinguisher, and he's pressing a button say he's giving me give me a sample in the distribution
34:26
that you have. I'm trying to determine whether I'm talking to the real view or I'm talking to the simulated view.
34:32
I'm just going to keep pressing the button getting views. And at the end, I should tell whether all the views I got
34:38
were from the real view or all the views I got from the simulated view. If a distinguisher can't tell this apart,
34:45
can't tell better than essentially 50/50, I say that these two views are computationally
34:52
indistinguishable. He just, upon a time distinguished, cannot tell them apart.
34:59
Let's chew in this a little bit further.
35:05
What does it mean that two distributions-- two probability distributions are computationally
35:10
indistinguishable? In our case here, the two distributions are the real views and the simulated views.
35:16
But it doesn't have to be applicable to this particular setting.
35:22
We can talk about computational indistinguishability as a notion more generally, where, again, there
35:28
are two distributions. In our case there were views, but there could be just two k-bit strings.
35:34
And the game is that there's a distinguisher on the other side of the wall and he can press a button
35:40
and get samples always from either-- all the samples from distribution d1, all the samples from the distribution d2.
35:46
And his wish is to distinguish which is the case. We say that these two distributions
35:51
are computationally indistinguishable if for whatever strategy this polynomial time
35:57
distinguisher employs, so for all distinguishing algorithms, even after receiving a polynomial number of samples
36:04
from d, the distributions of either one or two, the probability that he can guess what is whether this
36:12
was distribution one or the distribution two is less than 1/2 plus negligible. Negligible and what?
36:17
There's some sort of security parameter, which I call k here, which might be the size of the strings of the samples,
36:23
the size of the sample string. So back to zero-knowledge.
36:29
Here is a definition. An interactive protocol p and v is zero-knowledge for language
36:34
L if there exists a simulator in algorithm Sim, such that for every x in L, so I'm only
36:41
requiring it when the theorem is correct, only when x is in L. And why?
36:46
Because you do get something, you get that x is an L. But that's a detail aside. So I require that the following two probability
36:54
distribution are polynomial time indistinguishable. The first is the real view that the verifier
36:59
gets during an interaction. The second is an output of the simulator. The simulator here is taking x as an input, just the x.
37:06
Here it doesn't have any square root of y or any secrets, just the input, they're both p and vc.
37:12
You'll notice here that there's another input to the simulator, which is this one to the power of lambda.
37:17
This is essentially a technicality. It's because we want to make sure that we allow the simulator to run enough time, polynomial time.
37:23
And sometimes when x really small, that doesn't give him enough time. But really for all practical purposes,
37:30
if we're thinking about large x's, forget about this one. So both of them, the simulator runs in polynomial time.
37:37
To be zero-knowledge means that these two distributions should be computationally indistinguishable.
37:42
And that will make a protocol PV,
37:47
a zero note interactive proof, if it's complete, if it's sound, so it satisfies completeness and soundness
37:54
and zero-knowledge according to this definition. Almost.
37:59
Two caveats. We're going to let this Sim guy, this probabilistic polymial time run in expected polynomial time.
38:06
What that means is that it might-- that the simulator might expect the polynomial time essentially means that if you take the expectation of how much time
38:15
the simulator runs over all possible randomness of the simulator, it's going to be a polynomial time.
38:21
What essentially that means is that there might be some very, very unlucky coins for the simulator, which
38:28
will take a long time to run. But typically, he's going to run in polynomial time.
38:36
This is something that you guys should know. And that is the definition of expected polynomial time.
38:42
One more caveat. In this definition, I never said anything about the verifier.
38:47
I just said that a particular pair of p and v is zero-knowledge if the following conditions hold. But we want this to hold really, the zero-knowledge property,
38:54
for every verifier, even a cheating verifier. So the real final definition has to take into account
39:03
the possibility that the verifier might be a liar and might be trying to get knowledge when he shouldn't. So he's not honest.
39:09
So we finally get the definition that a protocol is zero-knowledge for language L if for every v start working
39:16
with p there exist a polynomial time simulator such
39:22
that the view and the simulation are computationally indistinguishable. And I'm using this squiggly equality
39:28
to mean computationally indistinguishable. So these might be different probability distribution, but the distinguiser cannot tell them apart.
39:36
All right. So let's rest a second. So p,v is zero-knowledge if for every v star, there was--
39:42
no matter what v star does-- actually we could have simulated this in our own.
39:48
What does this capture the intuition that what the verifier can learn during the interaction doesn't add any computational power?
39:54
Remember our original intuition was that what you can compute before and what you can compute after is the same.
40:01
The reason is because we say the following. Listen, maybe there is a v star, a really devious one,
40:07
who can get something out of the prover. Being zero knowldedge says, no.
40:12
If such a v star exists, then we could have computed this before because the simulator could use that v
40:17
star to come up with a simulated distribution, which
40:23
is more than what the view is. But the zero-knowledge requirement says that that's not possible, that for every star
40:30
there will be a simulator that can achieve the same distribution essentially,
40:37
computationally equivalent, to what can happen in the real view. And therefore, the real view did not
40:43
add any computational power. All right.
40:49
By the way, this is what's called a computationally indistinguishable zero-knowledge. Sometimes people use the notation CZK for computational.
40:57
But there are other flavors of zero-knowledge. You can also ask for perfect zero-knowledge definition,
41:03
so where the real distribution and the simulated distribution are identical, or maybe statistically close.
41:10
So a perfect zero-knowledge is a special case where if you look at the view of the verifier, then
41:17
we can actually simulate it perfectly. So the simulated view and the real view are the same. And that means that they're indistinguishable
41:24
for any algorithm. So this would mean that when you can prove perfect zero-knowledge, it's an unconditional result
41:29
because usually when we only prove computationally zero-knowledge, we make some assumption that there are some computations which are hard.
41:36
Whereas with perfect, it's just perfect zero-knowledge. There is no difference between what we can learn during the view, during the real interaction
41:44
and what we can learn from a simulation. Let's work through a simulation now that we have a definition.
41:53
We call the protocol for quadratic residues. So the prover send r squared.
41:58
He asked for either seeing r or r times square root of y. He got back an answer.
42:03
He checked it. So what's the view here? The view is s. That's the first message, b, second message.
42:09
And z, third message. And what are the coin tosses? Our B. So it's anyway included it's SBZ.
42:14
How do we simulate that? Well, we're going to simulate this a little bit in a different order.
42:20
After all, the simulator, we can't just choose an r and send himself a message. I mean, he could.
42:26
But then if you toss a coin, you only know how to return r. You don't know how to return r times square root of y.
42:34
So how are we going to get a simulation? The idea is as follows.
42:39
And we're going to show a simulator just for an honest verifier. And in fact, the simulation is going to be a perfect zero-knowledge simulation.
42:47
What the simulator is going to do is rather than really go in the order that the real interaction is, it a first going to choose
42:54
the question of the verifier. And he's going to do that just the way an honest verifier would do. It picks a random bit, b.
43:00
Then it's going to actually pick the third answer, which is it's going to pick a random z. Notice that z actually is just a random number
43:09
except in this case, it's r. In this case, it's r times x. So the only thing that remains is
43:14
to make sure that I can figure out for which s would have been z the right answer?
43:22
And note that this equation s equal to z squared over y to the b mod n satisfies exactly what
43:30
should be. Why is that? Let's look at this. Let's plug in b equal to zero, in which case,
43:37
s is equal to z squared. That's exactly what it should be. In the case that b is equal to zero,
43:42
z is the square root of s. What about when y is-- when b is equal to one?
43:49
Then, I'm letting us to be z squared over y. Is that correct? Let's think about it.
43:55
If you look at z here, it's supposed to be in the case of B equal to one, r times x. And what's the relation of r times x to s?
44:02
The relation is that if I square this, I should get s times y.
44:08
And that's exactly the case here. If I square z, I get s times y.
44:16
So lo and behold, I was able to come out with a triplet which is identically distributed as what
44:25
the view of the verifier, the honest verifier is during an interaction. Obviously, this doesn't convince me of anything.
44:32
It's not that I actually got an r squared and then I asked a random b and got the response.
44:37
I did this in my basement in a simulation. But the view is identical.
44:45
Now what about when the verifier is not honest? So what about the case, the general case,
44:52
where the verifier might not be tossing a coin and sending over? That's a little bit of a problem. What if this adversarial verifier was the kind
45:02
that when he saw some s, he did some very complicated function or computational s and depending on the result
45:09
of his computation, would ask a particular b? Then he might have gotten something interesting
45:14
depending on his computation. Well, I will show you that even if he was an adversarial, very
45:20
complex computation, I could still get the same view that he did using a simulator.
45:28
How is that? Again, I will pick a random b. Even though he doesn't like things that random.
45:34
But wait, I'm not done yet. I pick a random b, then I pick a random z. And now is when I do something different.
45:41
I say to myself, all right, I will for a minute,
45:46
suppose that indeed b would have been what he will ask me
45:53
the bad guy, the adversarial guy. And I will compute s accordingly. And now it will actually send s to this bad guy.
46:03
What does it mean send? Remember, the simulator should work correctly for every v star, for every bad guy v star.
46:09
The simulator has access to v star. The intuition is that no matter how powerful the verifier
46:15
is, he's polynomial time. And I have to come up with opponent time simulator. So he, polynomial time program can have access
46:23
to any other polynomial time program, including this verifier. So what I do is know is I run this verifier,
46:29
the bad verifier, on the input ny and first message s and see what he asks for.
46:36
If I was lucky, he's going to ask exactly the bit that I prepared for. And I know how to answer.
46:41
But he might not do that, in which case, I can't really output SBZ because I just
46:48
don't know the answer, the correct answers. What do I do then? I start again. I go to step one.
46:55
I again pick a random bit. I again pick a random z. I then compute s and now I ask v star on this new n,y, and s.
47:03
Why am I hoping that this time it's going to be better? I don't know if this time is going to be better.
47:08
But I do know that whatever it is that v star is doing, is this is a fixed behavior.
47:15
But my v was chosen at random. What's the probability that a random bit will equal a fixed behavior?
47:22
50/50. And that means that within two trials, I will be lucky enough to hit on the question
47:29
the v star would have asked. I suggest that you think about this more deeply and prove to yourself in the expected number of repetitions
47:36
is two before I can output a triplet SBZ. And this is why we require the simulator
47:43
to be expected polynomial time. So within expected two trials, I will be able to output something that is exactly
47:50
the same distribution as would have happened in the real interaction. All right.
47:56
I want to say that actually, if you think about this a little bit deeper, you realize that not only the prover
48:03
convinced the verifier that y has a square root, he actually proved that he knows how to--
48:09
what that square root is. Because if he can answer what the square root of s is and what the square root of s times y is,
48:16
he could actually answer the square root of y. He never does. He always gives you only the square root
48:21
of s, which is just random, or the square root of s times the square root of y, which
48:26
again the square root of s masks the square root of y. But if he could do both, he does actually know how to do a square root of y.
48:34
So what's hiding in here is some definition of what it means for a machine to prove to you they know something.
48:40
Let's try to define that formally. We will say that a proof system is a proof of knowledge.
48:46
So it's not just a proof that something is true or false, but it's a proof of knowledge for language if the following is true.
48:52
So let's think for a second. How would you define that a machine knows something?
48:57
Maybe the first definition would come to mind is that it has some register and that square root is written in there.
49:04
Or whatever it knows is written in there. But it's not always the case. The way that we want to define that you
49:10
know something or the algorithm knows something, is that if I can run that algorithm on multiple inputs,
49:16
I could eventually compute that thing that the algorithm knows.
49:21
So since the prover is an interactive algorithm, running it multiple time means that it can send me messages,
49:28
I could ask it a question, and send messages to ask questions. So I can run executions with the prover multiple times if at the end, I can
49:35
extract w, that is the definition to mean that the prover renewed w.
49:44
And that's how we define proof of knowledge. We say there exists a knowledge extractor algorithm,
49:50
this extractor, that can run a protocol with a prover, such at an expected polynomial time, this extractor running
49:59
a prover the rotation is E sup p. So he has access to the prover almost as an Oracle on x, will output the witness, w.
50:09
Now I want to make one thing clear is that when I say that the extractor runs
50:17
p multiple times, I can actually make it run so that he always,
50:23
in every execution, he asked me the first same message. So it's like saying I can rewind him to run--
50:29
to get started from the same starting point on the same randomness. This is called the rewinding technique,
50:36
which is something that happens all the time when we talk about zero-knowledge. That is usually the technique to prove that something
50:43
is zero-knowledge. And that is zero-knowledge proof of knowledge.
50:48
If we can rewind someone multiple times and eventually extract something from them,
50:55
it will mean that they knew it to begin with.
51:00
So here are some technicality which I'm not going to cover but it is the more precise definition
51:06
of proof of knowledge that takes into account what's the probability that the prover managed to convince
51:13
the verifier to accept? Essentially, if the probability is greater than alpha, we have always in this lecture said that in the case
51:20
x is in the language, then the probability is always one. But sometimes, you will have examples
51:26
when the probability is not one, it might be just greater than 2/3. Then we will just require the extracted
51:31
to run in expected time one over alpha, which one in 2/3 or one
51:36
in polynomial, which will be polynomial still.
51:43
An example of extraction. I said that the examples of quadratic residues, the prover
51:49
actually knows the square root x of r mod n. To technically show that he knows,
51:56
we have to satisfy the definition. So here it goes. Here's the extractor. The extractor starts running with the prover.
52:04
The first message of the prover is r squared mode n for some n. What does the extract to do?
52:09
First step, it receives s and it asks the heads for zero
52:17
and gets back an r. So it stores r. And now he rewinds to the first step again.
52:23
This time though, when he gets s, he asks for tails or b equal to one, to zero.
52:31
And he gets back rx mode n. Now he has run two executions, first time asking for heads,
52:38
second time asking for tails. He got two answers, rx and r can divide and extract
52:43
the square root of y mode n. So there's definitely an extractor. So by the definition, we have just
52:49
shown here in this slide the prover knows the square root of y. And let's try it for graphs.
52:55
So graph isomorphism, which we discussed before. What would be the interactive proof,
53:00
the zero-knowledge interactive proof for graph isomorphism? Let's go through that. It's going to be surprisingly similar to the square root
53:08
example, even though we're talking about graphs. When I say similar, I don't mean that it's the same message
53:13
is going back and forth. But the idea is quite similar. What is the idea?
53:19
So now we're talking there's paragraphs G0, G1, the prover is this all powerful guy. He knows actually in this example, an isomorphism.
53:27
He wants to convince the verifier that isomorphism exists without giving the isomorphism. How does he do it?
53:34
Here is what he does. He says to the verifier, listen. I'm going to forget about the proof for a minute.
53:41
Let's just see what the interaction is. He says to the verifier, I'm going to produce a random graph
53:47
H, like a third graph, so that I can give you
53:53
an amorphous either from G0 to H or I can give you an item of wisdom from G1 to H. These
54:01
are two different isomorphism. But the conclusion is if indeed I could do both,
54:06
then there is actually direct isomorphism from G0 to G1. So you see that very quickly here on the left on the side,
54:14
if H is gamma zero of G, an isomorphism from G0 and H is also an isomorphism from G1, gamma one,
54:25
then you could go directly from G0 to G1 by taking gamma one inverse of gamma zero, composition
54:32
of these two isomorphisms. Now the point is, again, he's not going to do both.
54:38
He's only going to give him either isomorphism for G0 or G1. But he lets the verify choose which it is.
54:44
And the fact that he will be able to do both should convince the verifier that there is an isomorphism from G0 to G1 with high probability.
54:53
If we break it down into the interaction, the prover sends the verifier the new graph H, the verifier tosses a coin, asks either
55:02
for isomorphism from G0, isomorphism from G1, or isomorphism from G1.
55:07
The prover is supposed to supply what he was asked for and the verifier can check that he got the right thing.
55:13
And only then accept, otherwise reject. If the statement that G0 was isomorphic to G1 is true,
55:21
the prover will be able to answer and the verifier should always accept. If the statement was false, the probability
55:28
the verifier will catch a mistake, that is, will ask to see isomorphism from G0
55:34
and the prover won't be able to supply it because there's either just an isomorphism G0 or from G1 or maybe from none,
55:41
the probability the verifier will catch a mistake is great or equal than a half.
55:46
And if we do this 100 times, the probability will be-- of catching a mistake it will be very close to one.
55:53
One minus one into 100 or if you repeat k times one minus one in two to the k.
56:00
I leave it as an exercise to you that it's perfect zero-knowledge. It's going to be essentially trivial if you understood
56:08
the quadratic residue example to come up with the perfect zero-knowledge proof here.
56:14
I encourage you to do that. It's also not just a zero-knowledge proof,
56:19
but it's a zero-knowledge proof of knowing an isomorphism. So it's a proof of knowledge.
56:25
Again, to show that, you have to show an extractor. Let's show an extractor.
56:31
So the extractor algorithm is allowed to run the prover. Let's do it.
56:36
The prover sends you a graph H. What do you do? First, you set the coins to heads and you get back and answer, which is an isomorphism from G0
56:45
to H. Second, you rewind. You start again with the same H, but this time, you
56:51
ask for tales. And it will give you an isomorphism from G1 to H. And now you can combine the isomorphism and from G0 to H
57:00
with isomorphism from G1 to H to get a direct isomorphism from G0 to G1.
57:06
The end. We are able to extract the isomorphism. And therefore, we know that this was a proof
57:13
of knowledge of an isomorphism. Great. Why did I talk about proofs of knowledge?
57:20
Because it gives us immediate corollary in our application. And that is the first application
57:26
that Fiat-Shamir proposed a few months after we wrote the paper about zero-knowledge for identity
57:32
theft. And they're saying, look, Alice wants to prove over the internet that she is Alice to Bob.
57:39
Bob could be Amazon, say. Over the net means something could be listening.
57:44
But even more interestingly, suppose nobody was listening, but Amazon had to store all those passwords in order
57:50
to recognize Alice when she comes in. What if somebody breaks into Amazon? You don't want those passwords in the clear.
57:59
You don't even want those passwords encrypted because maybe the encryption that Amazon does,
58:04
one can do a birthday attack or a lot of other attacks
58:11
that you can on a password file. Is it possible that Alice can convince Bob she's Alice in a different mechanism
58:19
without Bob actually being able to turn around and convince someone else that they are Alice without a break in attack?
58:28
And the answer is yes, zero-knowledge proofs gives you the mechanism. Now we think about the password of Alice
58:34
as knowing the proof of a hard theorem. So you can think of Alice as someone who takes
58:39
an x, squares it, calls that y. And says, hey, I know a square root of y mod n.
58:45
That's a hard theorem. But whoever knows it, that's Alice. How does she convince Amazon, a mainframe, an ATM, someone
58:54
who just wants to know that Alice is the right person, but shouldn't really know Alice's
59:00
proof for the hard theorem. Zero-knowledge proof. So they would go through a few steps of interaction
59:07
at the end of which it says, hmm, she knows a square root. She just given me a zero-knowledge proof
59:13
of knowledge. And that identifies her. So somehow it's possible to verify
59:19
that Alice knows the proof without knowing the proof yourself. It's not the only example of an application.
59:28
But in order to get many more applications, including applications in the realm of blockchains,
59:36
we need to do one more thing, and that is a big thing.
59:41
We've seen the example that two graphs are isomorphic. We've seen the example that y is a quadratic residue mod n.
59:49
But there are lots of other languages. So let's ask a really big question.
59:54
Do all NP languages have a zero-knowledge interactive proof. Whoa, that would be amazing.
1:00:00
But how are we going to do that? Are we going to go for every single NP language and show that they have zero-knowledge proof?
1:00:06
No. So in 1986, Goldreich, Micali, Widgerson
1:00:11
showed that if one way functions exist, then every language in NP has a zero-knowledge interactive
1:00:18
proof. Let's dwell on the statement. There's a condition here. When we showed that graph isomorphism has
1:00:26
perfect zero-knowledge or quadratic residues of perfect zero-knowledge, there was no condition. Here the condition is that one way functions exist.
1:00:33
This is essentially the simplest condition or the simplest assumption that we use in cryptography.
1:00:39
It will be covered in the supplementary material. But for now, let's just assume that factoring is hard
1:00:45
or discrete logs are hard or bilinear maps or hard.
1:00:51
That will be an instantiation of one-way function. And then they showed that for every language in NP,
1:00:57
there is a zero-knowledge interactive proof, a computational zero-knowledge interactive proof. It won't be a perfect one, but it
1:01:03
will be using the general definition of computational. There were two main ideas in the proof.
1:01:09
The first key idea it is to show that an NP, an example of an NP
1:01:16
complete problem that has a zero-knowledge interactive proof. That will be sufficient to establish
1:01:21
that every language in an NP has a computational zero-knowledge interactive proof. Why is that?
1:01:27
Due to NP completeness irreducibility, if a language is an NP complete, then every string x
1:01:34
can be reduced, let's say if we're talking about the three coloring NP complete language, every instance
1:01:40
x will be reduced to a graph G sub x, such that if x is in the language,
1:01:45
then the graph is three-colorable. And if x is not in the language, then the graph is not three-colorable.
1:01:52
That means that if I had a way now to have a zero-knowledge interactive proof
1:01:58
of whether the graph G sub x is three-colorable, it will also imply that I have zero-knowledge
1:02:05
of interactive proof of x being in the language, for every language, which is an NP. So what they showed in their paper
1:02:12
is a zero-knowledge interactive proof for a particular NP complete problem, the three coloring problem.
1:02:18
And I'll show you in a minute how to do that. But they needed one ingredient, and that is where
1:02:23
the one-way functions come in. They needed, essentially, to use the one-way function
1:02:31
to get a primitive, cryptographic primitive, called a commitment scheme.
1:02:37
And that is the second idea. So when we functions imply actually a big commitment scheme.
1:02:42
What's a commitment scheme? Essentially a commitment scheme or commitment protocol is a pair of protocols, a commit protocol and decommit.
1:02:50
A commit protocol takes as input an m. Usually, I want to think of m as a bit, it's either zero or one.
1:02:56
And essentially, metaphorically, puts m in an envelope, seals it so it's an opaque envelope.
1:03:02
There's a sender and a receiver. The sender commits, the receiver gets the envelope, can't tell whether there's a zero or one being
1:03:09
committed to it. Then there's a decommit protocol, where the receiver can actually open the envelope and show--
1:03:15
the sender opens the envelope and shows the receiver
1:03:21
that what was in there was either zero or one. The properties of these two protocol
1:03:27
is that they satisfy hiding and binding. Hiding means that while it's committed, you can't tell whether it's zero or one better than 50/50.
1:03:35
And binding means that when you open the envelope, you can't have committed to zero and open to one.
1:03:41
Whatever it is you committed to, you are actually bound to it to reveal it.
1:03:48
We can go in a little bit more detail here talking about exact definition for hiding
1:03:53
and that is that really the view of the receiver when you commit to a bit B or a bit B prime is incomputationally
1:04:03
indistinguishable. And binding is that you are not able to decommit
1:04:10
to two different values, B and B prime. What is an example of how did that get a big commitment
1:04:16
scheme? The simplest example is using encryption. You can think of commit as the sender essentially encrypting
1:04:23
the bit. If you want to commit to a bit B, you encrypt a bit B.
1:04:28
And you can think of decommitting then as giving the receiver either the decryption key
1:04:35
or the randomness you used in order to encrypt the bit B. It's very important that it will be a randomized scheme
1:04:41
for hiding to hold because I really want to be able to hide very strongly so you cannot tell apart whether what
1:04:49
you've committed to is zero or one. And for that, you need a probabilistic encryption scheme.
1:04:54
So let's go to the main act. And that is how do you show that a graph is three-colorable without giving the coloring in fact
1:05:01
in computational zero-knowledge? Having access to this commitment and decommitment primitives.
1:05:07
Here is the idea. So the prover, again, he knows all. He doesn't only have the graph, like the verifier
1:05:13
and the prover both have the graph. He actually has a coloring. So let's say he has a coloring of the vertices
1:05:19
to red, blue, and green. Or we can call these colors the zero color, the one color,
1:05:27
and the two color. The first step what the prover does, it's very different by the way, than the protocols
1:05:32
we've seen before. What he does now he picks a random permutation, which is a step that's unclear why but we'll
1:05:40
explain it in a minute. Rather than using the original coloring, he takes actually a permutation of those three colors.
1:05:46
So there are six permutations of that, like red could be now blue, blue could be green, green could be red, or any of the other five possibilities.
1:05:56
So you pick a random permutation of those colors. And now you go to all the vertices of the graph and you recolor them, take the old coloring
1:06:05
and recolor it according to the random permutation that you chose.
1:06:10
Now the graph is three colored. If the prover is claiming a correct proof,
1:06:15
there is a three-coloring and you just colored it again with a permutation of this coloring.
1:06:22
And now what the prover does is he commits to each of these colors by running a commit protocol.
1:06:27
In other words, he sends to the verifier a commitment to, for every vertex, it will be either a commitment
1:06:34
to red, to blue, or to green. The commitment means it's hidden. The verifier gets this, but he can't tell
1:06:39
what the heck are the colors. What the verifier now does is the following.
1:06:45
He thinks to himself, well, either this is a proper coloring or it isn't. If it isn't, it means that there's
1:06:51
at least one edge in this graph that if you look at the two endpoints, they're going to have the same color or maybe
1:06:58
some other color altogether. But to be proper three coloring means that you only use red, green, and blue.
1:07:05
And for every edge, the two endpoints are different colors. So what the verifier says, I have no idea which
1:07:11
one of these edges is wrong. Maybe they're all correct. But I'm trying to catch the mistake.
1:07:16
So what I'm going to do is I'm going to select a random edge among all the edges. And I'll send it to the prover.
1:07:22
And I'll say, you see this edge? I want you to commit the colors at the endpoints of the two endpoints of this edge.
1:07:28
And that's exactly what the prover is supposed to do. He's supposed to, sort of, open the envelopes that have to do with vertex a and vertex b.
1:07:36
And now there is the edge a,b has been decommitted in some sense.
1:07:41
The colors of endpoints. And the verifier, of course, if the colors
1:07:46
are not two different colors, he rejects immediately. Otherwise, it goes back to step one and repeats it again.
1:07:53
And after k iterations, maybe k's 100, if he never rejected, he never found an edge that has anything but two different colors,
1:08:03
he will accept. Let's analyze this.
1:08:08
I will analyze it in the next slide. But I want you to think for a second about this zero-knowledge aspect.
1:08:13
What has the verifier found? One iteration they found the colors of a single edge.
1:08:21
But what about the second iteration? And someone asked me in class, maybe he can build up after 100 iterations or more,
1:08:31
a partial coloring or maybe the entire coloring, no. And that is why. Why?
1:08:36
Because in step one, remember, I picked a random permutation of the base coloring. Why did I do that?
1:08:41
I did it so that even though I'm repeating this again and again and again, each time selecting maybe different edges,
1:08:48
the verifier is selecting different edges, the colors mean different things. Whereas before blue meant blue, now when
1:08:55
I pick a random permutation of the colors, blue might mean something completely different. In fact, you can prove that these colorings
1:09:02
are uncorrelated between repetitions. OK. So we need to prove that this is zero-knowledge.
1:09:09
We need to prove completeness, soundness, and zero-knowledge in this. Completeness, what does that mean?
1:09:15
If the graph is three-colorable, the prover, an honest prover can always convince the verifier to accept.
1:09:20
Yes, because you can always color it properly. And no matter what edge is being requested, you can always give the proper color.
1:09:26
What about soundness? If the graph is not three-colorable, now think about it.
1:09:31
No matter what the prover P star does, there is one edge there that's not properly colored.
1:09:37
What's the probability that when the verifier chose that random edge, he will actually hit on the wrong--
1:09:42
on the edge that is not properly colored, pretty small. Maybe everything is well colored except for one edge.
1:09:48
What's the chance you get that edge? Well, the chance is one in the number of edges.
1:09:54
So the probability that after one trial, one iteration of this, the probability that the verifier will accept when the graph is not
1:10:01
three-colorable is pretty good. It's one minus one in E. That's not good enough.
1:10:06
We want the probability that he accepts to be small in this case. So repeat again. But how many repetitions?
1:10:12
Twice won't be enough because one minus one in E times one minus one in E, it's a little smaller than one
1:10:19
minus one in E, but not much. But if I repeat this the number of edges, number of times,
1:10:24
then it will disappear exponentially. We will have one in natural log to one in little E
1:10:32
to the number of edges. And that is an exponentially small probability. And we get this gap between completeness and soundness.
1:10:40
You will always accept, the verifier will always accept when the graph is three-colorable. And you will accept with exponentially small probability
1:10:47
when the graph is not three-colorable. Now zero-knowledge, as I said, it's easy to see informally.
1:10:56
It's messy to prove it formally. So how do we see it?
1:11:01
At least let's give you-- I give you some inkling of the proof. And let's do it for the honest verifier.
1:11:07
So the honest verifier competition zero-knowledge works like this. This is the simulation. The simulation, again, works in a different order.
1:11:14
Rather than first taking a coloring and committing, how can he do that?
1:11:19
The simulator doesn't know coloring. There's no way you can do that. Can't even get off the ground. So what the simulator does is it chooses at random in advance
1:11:28
the challenge of the honest verifier, which is just a random edge. Then it chooses a bunch of colors,
1:11:39
really don't matter, he can color the whole graph in the same color, except for that edge that in the lucky execution, the verifier will ask him.
1:11:48
That's the a,b edge. And it colors it in two different colors, two different random colors. And what is the simulated view it outputs?
1:11:56
It commits to the transcript, which is a bunch of commitments. The commitments are not supposed to give anything
1:12:02
to a computationally bounded distinguisher because they're just commitments there or if you think about how we implement the commitments,
1:12:09
a bunch of encryptions. So we can't see anything. Then you give an edge the honest verifier put the random edge.
1:12:15
And then you have a decommitment transcript to those colors. And the decommitment transcript will give two different colors
1:12:21
to a and b because my commitment made it so that I essentially--
1:12:28
the only colors that were different were on that edge a and b.
1:12:35
This is exactly a kosher transcript. But is it?
1:12:40
Not really. If you think about what has been committed to is not a legal coloring. So this transcript is very different than what happens
1:12:46
in the real interaction. But it is computationally indistinguishable. And that depends on the hiding property
1:12:53
of the commitment protocol. So what does the simulation look like?
1:12:59
The simulation, which doesn't talk about honest verifies,
1:13:04
but for every verify, that's harder. It's here on the slide and I will leave it for the TA
1:13:16
to discuss in the supplementary lecture.
1:13:22
The upshot of this. Now that we know that all of NP can be done in interactive--
1:13:27
has an interactive zero-knowledge proof, it means that we have many--
1:13:32
many-- many examples which are interesting for us as many as there are NP languages.
1:13:39
Obviously, we can use this protocol also for the statements we already know perfect zero-knowledge
1:13:45
for, but we can get a stronger guarantee with perfect zero-knowledge. But the more interesting case is when
1:13:50
we don't a perfect zero-knowledge protocol and we have to go through this three coloring protocol. So an example.
1:13:57
Any satisfiable boolean formula to prove that it has a satisfying assignment can be done in zero-knowledge without actually
1:14:04
giving the assignment. Given an encrypted input E of x and a program, program, PROG,
1:14:12
I can prove to you in zero-knowledge that if you ran this program on an x that you only see the encryption of, you will get y.
1:14:20
In fact, I can give you an encrypted input, an encrypted program, and prove to you that if you ran that program on the input,
1:14:27
you would get back y. And that is without revealing the input or the program.
1:14:32
Why is that important? Here are applications. The first major application that they already
1:14:39
noticed in the original paper is a protocol design application. Essentially, this is a tool to enforce
1:14:46
owners behavior in cryptographic protocols without revealing any knowledge or information.
1:14:53
The idea is the following. Suppose you take a protocol and you've proved that if all players follow honestly the protocol
1:14:59
steps, it's a safe, secure protocol. Now you run it in the wild. The players may not follow the protocol.
1:15:06
But you want to make sure that you can still use your security proof. What do you do?
1:15:11
You tell the players, OK, I want you along with every message you send to give me a zero-knowledge proof,
1:15:18
a zero-knowledge interactive proof possibly that the next message that you're sending that is the message you're sending
1:15:25
is what you should have sent if you were honest. In other words, it's what the protocol rules would
1:15:31
tell you to send on the history of communication so far and your internal randomness, r, and maybe
1:15:37
some other internal inputs. How do you prove that in zero-knowledge?
1:15:42
Essentially, you commit to the internal randomness, you commit your internal secrets once
1:15:47
and for all when the protocol starts. And then every time you send a message, you attach a zero-knowledge proof
1:15:53
that on these committed randomness, on these committed private inputs, this is the right message to be sent.
1:15:59
Why can this be done? Because that is an NP statement. So if you think about the language,
1:16:04
there exists some randomness such that the next message is what is equal to the protocol on the history of communication in r
1:16:13
and in fact r has been committed to, that's an NP statement.
1:16:18
Again, it's a mouthful. I advise you to mill over this. But it is an amazingly powerful tool.
1:16:26
Zero-knowledge has been used for many things. In the 80s, it was mostly, the two applications I already
1:16:33
mentioned, which is identity-- preventing identity theft and a tool for protocol transformation from honest to dishonest players.
1:16:42
But since then, it's been used in the context of computation delegation, if you want to delegate computation
1:16:47
to the cloud, but only give the cloud encrypted data. It's even been discussed as a tool for nuclear disarmament.
1:16:56
That's a very interesting application of the concept of zero-knowledge that actually
1:17:01
nuclear physicists have been, at least about 10 years ago, there was a lot of work in this field.
1:17:09
People have suggested to use it in the context of forensics to prove, for example, that your DNA is not
1:17:15
the DNA on the crime scene without revealing your DNA. But in the context of this class and the huge boom
1:17:24
that has happened to zero-knowledge, it's mostly started with a paper by BenSasson, Chiesa,
1:17:31
and others on how to do Bitcoin in a private and anonymous manner.
1:17:36
So adding zk proofs in the context of cryptocurrency. More recently, there's some work by Bamberger and Rebecca
1:17:45
Wexler, and Ron Canetti, and Evan Zimmerman and myself that shows zero-knowledge might
1:17:51
be a very important tool in the context of the legal domain where there's many verification dilemmas in the law that
1:18:00
necessitate right now revealing a lot of information that you might not want to reveal and zero-knowledge
1:18:05
can be used instead. The last thing I want to say is that zero-knowledge
1:18:11
has been not only useful for cryptographic-type
1:18:16
applications, but it's actually been, sort of, revolutionary in the context of complexity theory.
1:18:21
And in fact, it's not so much zero-knowledge, but really the concept of interactive proofs. So I'm going to spend the last five minutes talking about that
1:18:29
before we end the class today. So when we talk about what's efficiently solvable, what's
1:18:34
an efficient algorithm, we usually talk about P, polynomial time, things that run in polynomial time, or things
1:18:42
that run in polynomial time plus coins. When we talk about what's efficiently verifiable,
1:18:48
we used to talk about NP. But in this lecture, I suggested a new form of proof and interactive where essentially you take NP
1:18:57
and you add interaction and randomness on the part of the verifier.
1:19:03
Notice that our verifier was pretty simple
1:19:11
in the perfect zero-knowledge examples. He was just choosing a coin and sending it over. And also in the NP three coloring zero-knowledge proof,
1:19:21
the verified shows a random edge. Is there something more sophisticated the verifier can do?
1:19:26
Here is an example. I'll show you an example of an interactive proof for a statement, which is not an NP statement, where
1:19:35
the verifier is doing something a little bit more than just tossing coins.
1:19:42
And this will answer two questions at the same time. One is can you interactively convince a verifier
1:19:49
in polynomial time of statements that we don't know how to convince using a classical, old NLP proof,
1:19:56
just sending a witness? And the answer is going to be yes. And second of all, is there something else
1:20:04
that a verifier can do except for tossing coins. And the answer for the next minute will be maybe.
1:20:12
Let me show you an example. Suppose I wanted to prove as a prover to the verifier
1:20:18
that actually these two graphs, which are different from the other graphs are not isomorphic to each other.
1:20:23
Is this any different than the previous painting, picture? Yes. I've added an edge here on the left graph, which
1:20:29
is zero between seven and four and on the right between four and ten. What adding this edges has done is
1:20:36
we've maintained the number of vertices and edges. But it's no longer true that these two graphs are important to each other.
1:20:42
How do I prove that to the verifier? Think about it for a minute.
1:20:47
I can't give an isomorphism because they're not isomorphous. I guess one thing to do is to go through all possible
1:20:54
isomorphisms and to show one by one that neither all of them-- neither one of them works or none of them work.
1:21:02
But there are a lot of isomorphism. So that is going to take a long time. There's an exponential number of isomorphism.
1:21:09
And in fact, [INAUDIBLE] But I want to convince an efficient verifier. So even though I don't have a short proof
1:21:15
to send over like an NP type proof, I will show you how to convince an efficient verifier
1:21:22
interactively that two graphs are not isomorphic to each other so that completeness
1:21:27
and soundness hold, and also zero-knowledge actually. Here's the idea.
1:21:33
Let me fill everything in and then go through it.
1:21:38
Step one, the verifier flip-- so the input is two graphs G0 and G1. And the claim is that they are not isomorphic to each other.
1:21:45
There is no isomorphism that maps the vertices of G0 to G1. Step one, the verifier flips a coin zero, one.
1:21:56
And he does that in order to select either G0 or G1. And he also picks a random isomorphism, a permutation
1:22:05
of the n vertices. And then he applies his isomorphism to either--
1:22:11
to the G sub of the coin. So let's say if the coin was 0, he applies at the G0. If the coin was one, he applies it G1.
1:22:16
That gives him a graph H, which he sends over to the prover. Now this graph is an isomorphic copy of G sub C. Notice
1:22:25
that if the two graphs were isomorphic, so it was an incorrect claim, this graph actually H is isomorphic to G0, but it also
1:22:32
is isomorphic to G1. How does a prover know which is the case?
1:22:38
If the two graphs are not isomorphic to each other, and he's an all powerful person, remember that's how we were thinking about the prover,
1:22:45
he just examines whether h is isomorphic to zero or G1 and he tells back to the verifier which is the case.
1:22:54
If the verifier knows whether he took an isomorphism of G0 or G1, if b is equal to his coin,
1:23:00
he's happy. If b is not equal to his coin, he immediately rejects. He says, hey, this guy couldn't tell whether it
1:23:07
was an isomorphism of G0 or G1. He must be a liar. These two graphs must be isomorphic to each other.
1:23:12
I reject. However, as usual, he could have been lucky. He could have guessed the right coin.
1:23:19
Even though h is isomorphic to only-- to both G0 or G1, he could have guessed
1:23:25
that the coin flip was zero. And convinced the verifier, or at least not
1:23:33
convince the verifier or left the verifier ambivalent.
1:23:39
So the probability that he succeeds to do that is going to be at most a half.
1:23:44
We do this as usual, k times the probability that you will always get the result of the coin of the verifier is a half the first time, a quarter
1:23:53
twice in a row, and eight three times in a row and one into two to k, k times in a row.
1:23:59
So when the two graphs are isomorphic, you'll catch them. When they are not isomorphic, he can always convince you,
1:24:06
so completeness and soundness hold. But does zero-knowledge hold for this protocol?
1:24:13
Let's think about it. Even intuitively, before we try to do a simulation and fail, it doesn't.
1:24:19
Why is that? Because the honest verifier, yes. The honest verifier, no problem. But if the verifier was not honest,
1:24:26
maybe he didn't just take a random H, apply it to the G sub c, and send over H. If he was honestly
1:24:32
did that, all he finds back is the result of his coin which he knows if it's what the coin was.
1:24:39
But maybe he's a cheater. If he's a cheater, he might be sending Hs here that he just wants to-- he's finding out whether this graph
1:24:46
H is as isomorphic to G0 or G1. So when this honest verifier is working
1:24:51
with an honest prover who's giving him, essentially he's telling him whether this new H is
1:24:56
isomorphic to G0 or G1, this is knowledge that I don't know how to simulate. And in fact, this is an example of a protocol,
1:25:04
which is an interactive proof. It's a nontrivial interactive proof. Like it convinces the verifier.
1:25:11
We don't know how to convince the verifier of non-isomorphism with an NP proof, but it's not zero-knowledge.
1:25:16
We will need to modify it to be zero-knowledge.
1:25:21
How do we modify it to be zero-knowledge? The verifier essentially before the prover answers
1:25:28
will have to prove to the prover. So now it's, sort of, a switcheroo.
1:25:34
He's going to send them H and then he will prove to him that actually he knows
1:25:41
that he really did these steps. He really applied this isomorphism to G sub C.
1:25:54
And it's beyond scope here, but there is a way for the verifier
1:26:00
to do that. What's interesting about this protocol is that it was very important for this protocol
1:26:07
to work that the verifier here did more than just flip a coin.
1:26:14
He actually picked-- a flipped a coin to pick this random number
1:26:19
and he didn't reveal to the proof or the result of his coin tosses. It's actually kind of interesting
1:26:24
that the prover is the one who gives back b. But the verifier flips them coins in secrecy
1:26:31
and then sends over H. If you think about it, this actually is very similar to the example of the colorblind
1:26:37
in the beginning of the lecture. The issue is that it brings up a general question.
1:26:42
And that is a question that came up around the same time that zero-knowledge paper came.
1:26:48
There was a proposal something called an Arthur-Merlin game by Babai and Moran, which is an interaction between a prover
1:26:55
and verifier, he called it Merlin and Arthur. The difference was that Arthur wasn't a probabilistic polynomial time algorithm that tossed
1:27:02
coin and did computation. He was just a coin tosser. He threw coins, get back, threw coins got back.
1:27:09
This was the case actually in the perfect zero-knowledge proofs that we've seen also in the three coloring case.
1:27:14
But it was not the case for this last example that I showed you.
1:27:19
And the question was asked, is it really the case that maybe you can prove more theorems
1:27:25
like non-isomorphism if you let the verifier Arthur hide his coins?
1:27:31
Or in other words, is IP, interactive proofs, more powerful than Arthur-Merlin, what they called
1:27:38
Arthur-Merlin games? Is the privacy coin necessary in order for the--
1:27:43
we were to convince statements which are not in NP?
1:27:49
The answer was no. Actually, you can take any interactive proof like the one we just showed for graph and isomorphism
1:27:56
and turn it automatically to a system where the author or the verifier only tosses coins.
1:28:02
It turns out that this transformation is such that it makes it so that even if Merlin
1:28:09
was efficient to begin with, he will become inefficient. But again, this is a complexity course.
1:28:15
There are lots of other questions people asked and that was how exactly powerful
1:28:22
are interactive groups? So you can do graph and isomorphism. Can you do more than that? The answer is that you can do actually a lot more than that.
1:28:31
But before I show you that, I want to say that protocol is where Arthur or the verifier,
1:28:37
is only a coin tosser, a very interesting protocol in practice because it has been suggested by Fiat and Shamir
1:28:46
in a paper on-- suggesting something called a Fiat-Shamir paradigm or at least since then, we call it
1:28:52
the Fiat-Shamir paradigm is that when you have a protocol where the approver is sending messages,
1:29:00
but the verifier always doing the sending coins, you could possibly get rid of interaction.
1:29:06
Now getting rid of interaction is a big one. If we can transform all this to like the prover just sending a string, that would be amazing.
1:29:13
How could you get rid of interaction. The suggestion of Fiat-Shamir was this.
1:29:18
They said, let's assume for a minute that we had access to some H, big H which
1:29:24
we think of as a cryptographic hash function. Again this is for the supplementary material. For the purposes of my lecture, let's just
1:29:31
think of H as a random oracle. What does that mean? H, basically, I can apply it to a string and get random coins.
1:29:38
Something that really looks unpredictable. Then if such an H existed, what the prover can do is say,
1:29:47
well, there's some interactive proof. And let's say we prove completeness and soundness about it, what I can do instead of really interacting, sending
1:29:57
A1, getting back coin, sending A2, and so forth, what I'll do is I will send you a string, which is my first message A1
1:30:07
and instead of waiting for your message with coins, I will, by myself, apply big H, this hash
1:30:13
function to my own message. And since I'm told this H really just takes
1:30:19
the message and outputs something that looks random, I will now view this as your question, your coin question
1:30:26
and answer that. And this transcript rather than A1 coins A2,
1:30:31
its A1, the result of applying the hash function to A1, A2 should be just as good.
1:30:37
And the verifier can run his decision procedure on this history rather than on a true interaction
1:30:44
and then decide it to accept or reject, it should be satisfied completeness and soundness
1:30:50
in the same way as a real interaction did. A lot of people use this Fiat-Shamir in practice, this paradigm.
1:30:57
It's heuristic. Why do I say it's heuristic? Because we don't really have such cryptographic hash
1:31:02
functions that take a string and give me something at random. That is an idealization. It's called a random oracle model.
1:31:09
But it is used in practice all the time. What you can say that if h is behaving like a random oracle,
1:31:17
then completeness and soundness twofold. Warning, this does not mean that all interactive zero-knowledge
1:31:26
proofs can be made non-interactive. Even though IP is equal to AM, it's not true
1:31:31
that all interactive proof protocols where the verifier hides his coin can be
1:31:40
turned into zero-knowledge interactive proofs where Arthur doesn't hide his coins.
1:31:46
But it can benefit many protocols. And just one other thing is notice
1:31:52
that what I did here in this slide, I looked at a case where the first message is from Marylyn,
1:31:58
the second message is coins. But in some of the protocols we've seen, the first message is actually from the verifier.
1:32:04
Then how do you make that non-interactive. Well usually what happens is--
1:32:10
and that is going to be used in the course extensively, is that we will post the first message coins as, sort of, a publicly chosen randomness for all
1:32:17
to see. And then apply the Fiat-Shamir heuristics to get non-interactive proofs.
1:32:22
The notion of interactive proofs has been really a catalyst for complexity theory.
1:32:29
Because it was the first time that we really decoupled correctness from the knowledge of the proof.
1:32:34
And it enabled people to ask a lot of new questions about the nature of the proof. These questions have been asked and some of them
1:32:40
been answered for the last 30 plus years. And it's leading up to actually current research on provably
1:32:47
outsourcing computation and some research in quantum computation, some highlights.
1:32:53
Well, classically, before interactive proofs, the notion of efficient verification
1:32:58
was NP, that is that there exists a solution. So I just send you the solution. And you as a verifier check it.
1:33:06
We didn't know how to verify whether Co-NP statements were
1:33:12
correct, like to do graphs are not isomorphic to each other, Co-NP are the complement to NP languages.
1:33:19
To count how many solutions are there to a statement. So for example, if you have a Boolean formula, how many--
1:33:29
and you want to find out does there exist a solution, that's an NP statement. There's no solutions, that's a co-NP statement.
1:33:35
There are exactly 37 correct solution,
1:33:41
that's what's called a sharpie statement. We don't know how to convince the verifier of that efficiently using an NP proof.
1:33:48
Or even a more complex statement where you have an alternation of quantifiers like for all x, there exist a y such that for all x2 the exist a z,
1:33:56
and so forth. We have no idea how to convince a polynomial of time prover of such statements.
1:34:01
However, if we use interactive proofs, it turns out we can. So just by adding interaction and randomness,
1:34:10
it has been shown in an amazing paper by Fortnow, Karlof, Babai, Lund Nissan
1:34:22
and then by Shamir, that you can convince a polynomial time
1:34:27
probabilistic verifier with a very powerful prover, by a polynomial number of messages
1:34:33
that even statements in P space can be proved using an interactive proof.
1:34:39
Not only that, but people have thought they said, well interaction helps, coins help, maybe there's
1:34:46
other ways to define probabilistic proof system. And in fact, in a joint paper with Benor, Killian, Widgerson,
1:34:52
we came with one such statement. And we said, one prover, we we're able to do p space, what if we add another one.
1:34:59
So to begin with, you say why would one-- two be better than one? I mean, they're all powerful, what does that add?
1:35:05
The idea was that we will let these two provers, this one will interact with the verifier. And this one will interact with the verifier,
1:35:12
but they won't see each other's messages. And we likened it as if there was an interrogation of these two provers like interrogating
1:35:18
someone in the crime. What's the crime? There's a claim. If the claim is true, there is no crime.
1:35:24
If the claim is false and he's trying to convince you that it's true, there is a crime. There's a bug in the proof, you're trying to find it.
1:35:31
And we were able to show indeed that if you use this kind of proof system, you can get
1:35:37
unconditional zero-knowledge. So perfect zero-knowledge for all of NP.
1:35:43
But more interestingly, it turned out that in some incredible sequence of events,
1:35:49
it was shown that two provers can actually convince you of even more statements than P is based.
1:35:55
The kind of intuition is the power of two provers which are in different interrogation
1:36:01
rooms is that you can catch inconsistency. So they have to be consistent for you to accept
1:36:08
their proof of a claim. And catching inconsistency is an incredibly powerful device.
1:36:13
And in fact, it's been shown you can even convince a polynomial time verifier of non-deterministic exponential time statements.
1:36:23
This has led to incredible theorem called the PCP theorem
1:36:29
saying that even if you stuck back to NP statements, back to the usual good old NP statements where you have
1:36:36
short witnesses for, there is a way to verify them being correct with very high probability
1:36:44
by only reading a constant number of bits of the proof. So this is like going somewhere completely different. But it is a result of interactive proofs
1:36:52
because we are allowing the verifier to make an error. We are allowing him to toss coins and what has been shown
1:36:59
is that by coming up with a very different mechanism for writing
1:37:05
proofs down, you could write them in such a way that you could only need to read a few random locations in order
1:37:12
to find an error. It's another way to think of a two-prover proof system. As I said, it had an impact on quantum computing.
1:37:20
And one of the beautiful results there is the result of some people from Berkeley, Umesh Vazirani
1:37:27
and others. And that is how do we know that a quantum computer is actually
1:37:32
using quantum power if we only have classical powers? And what they showed is a way to take,
1:37:39
essentially, a claimed efficient quantum computation, two copies
1:37:45
of it, likening the two provers, make them sit in separate rooms, but be entangled and show
1:37:52
how you could convince a classical verifier of the correctness of the computation by choosing coins
1:38:01
and by using entanglement. And then this leads up to something very, very recent showing that actually, if you have two provers, so
1:38:09
not necessarily efficient quantum computers, but two quantum computers who might be taking a long time,
1:38:17
they can convince a classical verifier of languages,
1:38:22
which are all they recursively enumerable languages. So this is, kind of, an amazing statement and it's an amazing theorem.
1:38:29
There's a lot of buzz around it today. All right. Thank you.
