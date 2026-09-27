# 2026-SEP-25

## London vs Detroit TDD

After this topic came up, I found the following [Medium article](https://medium.com/@adrianbooth/test-driven-development-wars-detroit-vs-london-classicist-vs-mockist-9956c78ae95f), which nicely covering the topic.

- Detroit - also called Classicist, Inside-out, black-box, or social testing
- London - Mockist, outside-in, white box, or solitary testing


Detroit/Classicist (avoiding the use of mocks) treat the entire method call like a black box meaning that when the method is called, you should expect an explicit result to come back: (`sum (1,1) excepts a value of 2`)

London/Mockists (using mocks during testing) doesn’t focus on the general correctness of the method because it will communicate with another object that will be tested in the return value of elsewhere. All that matters is that it passes the information along: `expect(sum()).toHaveBeenCalledWith(1,1))`

A nice summary between the two was covered in the comment section the article:

"A test architecture designed by a London school practitioner, with an extensive set of mocks, will likely produce many false positives and handicap any future refactoring efforts"
[if there’s a set of mocks for separate methods, a refactor to any of those methods will force you to update all of the tests using that specific method].

"Whilst a Classicist test suite will include less isolated unit tests that would break due to no fault of the particular subject under test."
[a bug may be introduced in an unrelated component that directly impacts your unit test

Basically, both methods have their place and use cases. I think it's a blend of both where each covers the weaknesses by the other.

## Over rotating on DORA

DORA metrics function as to identify:

Leading indicators for organizational performance and employee well-being

Lagging indicators for software development and delivery practices.

The metrics are grouped into

Throughput: measure of how many changes can move through the system over a period of time.

- Change lead time
- Deployment frequency
- Failed deployment recovery time

Instability: a measure of how well the software deployments go.

- Change fail rate
- Deployment rework rate

From what I gathered, there was some concern about letting metrics become the goal [Goodhart's Law](https://en.wikipedia.org/wiki/Goodhart%27s_law).

Charles Munger also has a useful quote adjacent to this idea: "Show me the incentive and I’ll show you the outcome."

But the counterpoint was that the organization hasn’t done well at tracking these metrics across teams to begin with, so how can we over rotate on them if we aren’t even tracking them effectively. I think the consensus was that we should aim to effectively capture this information first.

## Speed is relative

"Speed is relative..." basically, the deployment frequency, the number of features delivered, etc are limited by the slowest element in your development process (e.g., path-to-prod)

For example, deploying in an external environment, may be several times slower than PX and should be a consideration/risk that should be understood by product team and the wider organization. However, that shouldn’t stop the team from iterating locally on features.

## Team Coach Role

Basically, we determine that the team well-being shouldn’t only be relegated to the PM, everyone should have a vested interest in the team’s health

## Trunk based of development 🌶️

The dark horse of lean coffee, basically a topic came up during the PM practice time and led to an interesting discussion on best practices and trade-off between each.

Trunk based development is the practice of working directly off of your main production branch (origin main).

This means that there are no branches whatsoever and all commits going straight into the same single "trunk".

Branch based development is creating a separate branch off of main, they're used to keep a code change separate until completed.

Obviously, there's some subtlety with the specifics here, but I think this captures the idea.

For Trunk Based Development seems the most useful where teams rotate often, communicate, and the features/stories are small and targeted enough to be accomplished in few days... If there are any merge conflicts, resolving them is trivial.

Branch base development seems most useful when spiking on a feature that touches the entire application or having a "safety net" for code that isn't the highest quality. I think the difference here might also be on how long those feature branches stay around.

"In an ideal world you don't ever want to crash, but opt to put on a seatbelt..."

A good metric during Dev norming is to consider how long branches are sticking around. This may also be useful indicator for the product side that the stories are too big, too complex, or aren't targeted enough.

I think that maybe we're too caught up in semantics here. I saw a take on Reddit comment summed it up nicely, "...it's _never_ about not having branches but about **NOT** having _long-lived_ branches [and regularly pulling latest so that you're changes aren't out-of-date].