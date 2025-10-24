---
created: 2025-10-24
source: https://apenwarr.ca/log/20230605
author: Avery Pennarun  
published: 2023-06-05
tags: [technical-debt, engineering, finance, systems-thinking, metaphor]
status: complete
project: TailScale
---

# Summary

Pennarun defends and extends the technical debt metaphor by deeply understanding financial debt. He distinguishes between "consumer debt" (instant gratification paid later) versus "capital investment" (debt that generates more revenue than interest costs). High-interest debt (credit cards, store cards) should be paid off quickly or converted to lower-interest options (lines of credit, mortgages with collateral).

Applied to tech: high-interest tech debt includes code without tests/docs (quick but costly), while low-interest includes architectural choices like microservices (takes longer to change but might be worth keeping). Key insight: sometimes it's rational not to pay off debt—just as companies strategically maintain financial leverage, teams should evaluate whether "paying down" tech debt actually delivers more value than the cost of refactoring. The metaphor works when you understand that profitable companies deliberately carry debt, making the engineering version more nuanced than "debt = always bad."

When there's only one

[![](https://apenwarr.ca/img/ave-home.jpg)](https://apenwarr.ca/)

...there's only one choice

_Everything here is my opinion. I do not speak for your employer._

_← [April 2023](https://apenwarr.ca/log/?m=202304)_

_[October 2023](https://apenwarr.ca/log/?m=202310) →_

## 2023-06-05  [»](https://apenwarr.ca/log/20230605)

**Tech debt metaphor maximalism**

I really like the "tech debt" metaphor. A lot of people don't,
but I think that's because they either don't extend the metaphor far enough,
or because they don't properly understand financial debt.

So let's talk about debt!

**Consumer debt vs capital investment**

Back in school my professor, [Canadian economics superhero Larry\\
Smith](http://lwsmith.ca/), explained debt this way (paraphrased): debt is
stupid if it's for instant gratification that you pay for later, with
interest. But debt is great if it means you can make more money than the
interest payments.

A family that takes on high-interest credit card debt
for a visit to Disneyland is wasting money. If you think you can pay it off
in a year, you'll pay 20%-ish interest for that year for no reason. You can
instead save up for a year and get the same gratification next year without
the 20% surcharge.

But if you want to buy a $500k machine that will earn your factory an additional
$1M/year in revenue, it would be foolish _not_ to buy it now, even with 20%
interest ($100k/year). That's a profit of $900k in just the first year!
(excluding depreciation)

There's a reason profitable companies with CFOs take on debt, and often the
total debt increases rather than decreases over time. They're not idiots.
They're making a rational choice that's win-win for everyone. (The
company earns more money faster, the banks earn interest, the interest gets
paid out to consumers' deposit accounts.)

Debt is bad when you take out the wrong kind, or you mismanage it, or it has
weird strings attached (hello Venture Debt that requires you to put all your
savings in [one underinsured\\
place](https://www.washingtonpost.com/business/2023/03/15/svb-billions-uninsured-assets-companies/)).
But done right, debt is a way to move faster instead of slower.

**High-interest vs low-interest debt**

For a consumer, the highest interest rates are for "store" credit cards, the
kinds issued by Best Buy or Macy's or whatever that only work in that one
store. They aren't as picky about risk (thus have more defaults) because
it's the ultimate loyalty programme: it gets people to spend more at their
store instead of other stores, in some cases because it's the only place
that would issue those people debt in the first place.

The second-highest interest rate is on a general-purpose credit card like
Visa or Mastercard. They can get away with high interest rates because
they're also the payment system and so they're very convenient.

(Incidentally, when I looked at the stats a decade or so ago, in Canada
credit cards make _most_ of their income on payment fees because Canadians
are annoyingly persistent about paying off their cards; in the US it's the
opposite. The rumours are true: Canadians really are more cautious about
spending.)

If you have a good credit rating, you can get better interest rates on a
bank-issued "line of credit" (LOC) (lower interest rate, but less convenient
than a card). In Canada, one reason many people pay off their credit card
each month is simply that they transfer the balance to a lower-interest LOC.

Even lower interest rates can be obtained if you're willing to provide
collateral: most obviously, the equity in your home. This greatly reduces
the risk for the lender because they can repossess and then resell your home
if you don't pay up. Which is pretty good for them even if you don't pay,
but what's better is it makes you much more likely to pay rather
than lose your home.

Some people argue that you should almost never plan to pay off your
mortgage: typical mortgage interest rates are lower than the rates you'd get
long-term from investing in the S&P. The advice that you should "always buy
the biggest home you can afford" is often perversely accurate, especially if
you believe property values will keep going up. And subject to your risk
tolerance and lock-in preferences.

What's the pattern here? Just this: high-interest debt is quick and
convenient but you should pay it off quickly. Sometimes you pay it off just
by converting to longer-term lower-rate debt. Sometimes debt is
collateralized and sometimes it isn't.

**High-interest and low-interest tech debt**

Bringing that back to tech debt: a simple kind of high-interest short-term
debt would be committing code without tests or documentation. Yay, it works,
ship it! And truthfully, maybe you should, because the revenue (and customer
feedback) you get from shipping fast can outweigh how much more bug-prone
you made the code in the short term.

But like all high-interest debt, you should plan to pay it back fast. Tech
debt generally manifests as a slowdown in your development velocity (ie.
overhead on everything else you do), which means fewer features
launched in the medium-long term, which means less revenue and customer
feedback.

Whoa, weird, right? This short-term high-interest debt both _increases_
revenue and feedback rate, and _decreases_ it. Why?

- If you take a single pull request (PR) that adds a new feature, and launch
it without tests or documentation, you will definitely get the benefits of
that PR sooner.

- Every PR you try to write after that, before adding the tests and docs
(ie. repaying the debt) will be slower because you risk creating
undetected bugs or running into undocumented edge cases.

- If you take a long time to pay off the debt, the slowdown in future
launches will outweigh the speedup from the first launch.


This is exactly how CFOs manage corporate financial debt. Debt is a drain on
your revenues; the thing you did to incur the debt is a boost to your
revenues; if you take too long to pay back the debt, it's an overall loss.

CFOs can calculate that. Engineers don't like to. (Partly because tech debt
is less quantifiable. And partly because engineers are the sort of people who
pay off their loans sooner than they mathematically should, as a matter of
principle.)

**Debt ceilings**

The US government has imposed a [famously ill-advised debt\\
ceiling](https://www.reuters.com/world/us/biden-signs-bill-lifting-us-debt-limit-2023-06-03/)
on itself, that mainly serves to cause drama and create a great place to
push through unrelated riders that nobody will read, because the bill to
raise the debt ceiling will always pass.

Real-life debt ceilings are defined by your creditworthiness: banks simply
will not lend you more money if you've got so much outstanding debt that
they don't believe you can handle the interest payments. That's your credit
limit, or the largest mortgage they'll let you have.

Banks take a systematic approach to calculating the debt ceiling for each
client. How much can we lend you so that you take out the biggest loan you
possibly can, thus paying as much interest as possible, without starving to
death or (even worse) missing more than two consecutive payments? Also,
morbidly but honestly, since debts are generally not passed down to your
descendants, they would like you to be able to just barely pay it all off
(perhaps by selling off all your assets) right before you kick the bucket.

They can math this, they're good at it. Remember, they don't want you to pay
it off early. If you have leftover money you might use it to pay down your
debt. That's no good, because less debt means lower interest payments.
They'd rather you incur even more debt, then use that leftover monthly
income even for bigger interest payments. That's when you're trapped.

The equivalent in tech debt is when you are so far behind that you can
barely keep the system running with no improvements at all; the perfect
balance. If things get worse over time, you're underwater and will
eventually fail. But if you reach this zen state of perfect equilibrium, you
can keep going forever, running in place. That's your tech debt ceiling.

Unlike the banking world, I can't think of a way to anthropomorphize a
villain who wants you to go that far into debt. Maybe the CEO? I guess maybe
someone who is trying to juice revenues for a well-timed acquisition.
Private Equity firms also specialize in maximizing both financial and
technical debt so they can extract the assets while your company slowly
dies.

Anyway, both in finance and tech, you want to stay well away from your
credit limit.

**Debt to income ratios**

There are many imperfect rules of thumb for how much debt is healthy.
(Remember, some debt is very often healthy, and only people who don't
understand debt rush to pay it all off as fast as they can.)

One measure is the debt to income ratio (or for governments, the
debt to GDP ratio). The problem with debt-to-income is debt and income are two
different things. The first produces a mostly-predictable repayment cost
spread over an undefined period of time; the other is a
possibly-fast-changing benefit measured annually. One is an amount, the
other is a rate.

It would be better to measure interest payments as a fraction of revenue. At
least that encompasses the distinction between high-interest and
low-interest loans. And it compares two cashflow rates rather
than the nonsense comparison of a balance sheet measure vs a cashflow
measure. Banks love interest-to-income ratios; that's why your income level
has such a big impact on your debt ceiling.

In the tech world, the interest-to-income equivalent is how much time you
spend dealing with overhead compared to building new revenue-generating
features. Again, getting to zero overhead is probably not worth it. I like
this [xkcd explanation](https://xkcd.com/1205/) of what is and is not worth
the time:

![](https://imgs.xkcd.com/comics/is_it_worth_the_time.png)

Tech debt, in its simplest form, is the time you didn't spend making tasks
more efficient. When you think of it that way, it's obvious that zero tech
debt is a silly choice.

(Note that the interest-to-income ratio in this formulation has nothing to
do with financial income. "Tech income" in our metaphor is feature
development time, where "tech debt" is what eats up your development time.)

(Also note that by this definiton, nowadays tech stacks are so big, complex,
and irritable that every project starts with a giant pile of someone else's
tech debt on day 1. Enjoy!)

**Debt to equity ratios**

Interest-to-income ratios compare two items from your cashflow statement.
Debt-to-equity ratios compare two items from your balance sheet. Which means
they, too, are at least not nonsense.

"Equity" is unfortunately a lot fuzzier than income. How much is your
company worth? Or your product? The potential value of a factory isn't just
the value of the machines inside it; it's the amortized income stream you
(or a buyer) could get from continuing to operate that factory. Which means
it includes the built-up human and business expertise needed to operate the
factory.

And of course, software is even worse; as many of us know but few
businesspeople admit, the value of proprietary software without the people
is zero. This is why you hear about acqui-hires (humans create value even if
they might quit tomorrow) but never about acqui-codes (code without
humans is worthless).

Anyway, for a software company the "equity" comes from a variety of factors.
In the startup world, Venture Capitalists are -- and I know this is
depressing -- the best we have for valuing company equity. They are, of
course, not very good at it, but they make it up in volume. As software
companies get more mature, valuation becomes more quantifiable and comes
back to expectations for the future cashflow statement.

Venture Debt is typically weighted heavily on equity (expected future value)
and somewhat less on revenue (ability to pay the interest).

As the company builds up assets and shows faster growth, the assumed
equity value gets bigger and bigger. In the financial world, that means
people are willing to issue more debt.

(Over in the consumer world: your home is equity. That's why you can get a
huge mortgage on a house but your unsecured loan limit is much smaller. So
Venture Debt is like a mortgage.)

Anyway, back to tech debt: the debt-to-equity ratio is how much tech debt
you've taken on compared to the accumulated value, and future growth rate,
of your product quality. If your product is acquiring lots of customers
fast, you can afford to take on more tech debt so you can acquire more
customers even faster.

What's weirder is that as the absolute value of product equity increases,
you can take on a larger and larger absolute value of tech debt.

That feels unexpected. If we're doing so well, why would we want to take on
_more_ tech debt? But think of it this way: if your product (thus company)
are really growing that fast, you will have more people to pay down the tech
debt next year than you do now. In theory, you could even take on so much
tech debt this year that your current team can't even pay the interest...

...which brings us to leverage. And risk.

**Leverage risk**

Earlier in this article, I mentioned the popular (and surprisingly, often
correct!) idea that you should "buy the biggest house you can afford." Why
would I want a bigger house? My house is fine. I have a big enough house.
How is this good advice?

The answer is the amazing multiplying power of leverage.

Let's say housing goes up at 5%/year. (I wish it didn't because this rate is
fabulously unsustainable. But bear with me.)
And let's say you have $100k in savings and $100k in annual
income.

You could pay cash and buy a house for $100k. Woo hoo, no mortgage! And
it'll go up in value by about $5k/year, which is not bad I guess.

Or, you could buy a $200k house: a $100k down payment and a $100k mortgage
at, say, 3% (fairly common back in 2021), which means $3k/year
in interest. But your $200k house goes up by 5% = $10k/year. Now you have an
annual gain of $10k - $3k = $7k, much more than the $5k you were making
before, with the same money. Sweet!

But don't stop there. If the bank will let you get away with it, why not a
$1M house with a $100k down payment? That's $1M x 5% = +$50k/year in value,
and $900k x 3% = $27k in interest, so a solid $23k in annual (unrealized)
capital gain. From the same initial bank balance! Omg we're printing money.

(Obviously we're omitting maintenance costs and property tax here. Forgive
me. On the other hand, presumably you're getting intangible value from
living in a much bigger and fancier house. $AAPL shares don't have skylights
and rumpus rooms and that weird statue in bedroom number seven.)

What's the catch? Well, the catch is massively increasing risk.

Let's say you lose your job and can't afford interest payments. If you
bought your $100k house with no mortgage, you're in luck: that house is
yours, free and clear. You might not have food but you have a place to live.

If you bought the $1M house and have $900k worth of mortgage payments to
keep up, you're screwed. Get another job or get ready to move out and
disrupt your family and change everything about your standard of living, up
to and possibly including bankruptcy, which we'll get to in a bit.

Similarly, let's imagine that your property value stops increasing, or (less
common in the US for stupid reasons, but common everywhere else) mortage
rates go up. The leverage effect multiplies your potential losses just like
it multiplies your potential gains.

Back to tech debt. What's the analogy?

Remember that idea I had above, of incurring extra tech debt this year to
keep the revenue growth rolling, and then planning to pay it off next year
with the newer and bigger team? Yeah, that actually works... if you keep
growing. If you estimated your tech debt interest rate correctly. If that
future team materializes. (If you can even motivate that future team to work
on tech debt.) If you're rational, next year, about whether you borrow more
or not.

That thing I said about the perfect equilibrium running-in-place state, when
you spend all your time just keeping the machine operating and you have no
time to make it better. How do so many companies get themselves into that
state? In a word, leverage. They guessed wrong. The growth rate fell off,
the new team members didn't materialize or didn't ramp up fast enough.

And if you go past equilibrium, you get the worst case: your tech debt
interest is greater than your tech production (income). Things get worse and
worse and you enter the downward spiral. This is where desperation sets in.
The only remaining option is ~~bankruptcy~~ Tech Debt
Refinancing.

**Refinancing**

Most people who can't afford the interest on their loans don't declare
bankruptcy. The step before that is to make an arrangement with your
creditors to lower your interest payments. Why would they accept such an
agreement? Because if they don't, you'll declare bankruptcy, which is annoying
for you but hugely unprofitable for them.

The tech metaphor for refinancing is _premature deprecation_. Yes, people
love both service A and service B. Yes, we are even running both services at
financial breakeven. But they are slipping, slipping, getting a little worse
every month and digging into a hole that I can't escape. In order to pull
out of this, I have to stop my payments on A so I can pay back more of B; by
then A will be unrecoverably broken. But at least B will live on, to fight
another day.

Companies do this all the time. Even at huge profitable companies, in some
corners you'll occasionally find an understaffed project sliding deeper and
deeper into tech debt. Users may still love it, and it may even be net
profitable, but not profitable enough to pay for the additional engineering
time to dig it out. Such a project is destined to die, and the only
question is when. The answer is "whenever some executive finally notices."

**Bankruptcy**

The tech bankruptcy metaphor is an easy one: if refinancing doesn't work and
your tech debt continues to spiral downward, sooner or later your finances
will follow. When you run out of money you declare bankruptcy; what's
interesting is your tech debt disappears at the same time your financial
debt does.

This is a really important point. You can incur all the tech debt in the
world, and while your company is still operating, you at least have some
chance of someday paying it back. When your company finally dies, you will
find yourself off the hook; the tech debt never needs to be repaid.

Okay, for those of us grinding away at code all day, perhaps that sounds
perversely refreshing. But it explains lots of corporate behaviour. The more
desperate a company gets, the less they care about tech debt. _Anything_ to
turn a profit. They're not wrong to do so, but you can see how the downward
spiral begins to spiral downward. The more tech debt you incur, the slower
your development goes, and the harder it is to do something productive that
might make you profitable. You might still pull it off! But your luck will
get progressively worse.

The reverse is also true. When your company is doing well, you have time to
pay back tech debt, or at least to control precisely how much debt you take
on and when. To maintain your interest-to-income ratio or debt-to-equity
ratio at a reasonable level.

When you see a company managing their tech debt carefully, you see a company
that is planning for the long term rather than a quick exit. Again, that
doesn't mean paying it all back. It means being careful.

**Student loans that are non-dischargeable in bankruptcy**

Since we're here anyway talking about finance, let's talk about the idiotic
US government policy of guaranteeing student loans, but also not allowing
people to discharge those loans (ie. zero them out) in bankruptcy.

What's the effect of this? Well, of course, banks are extremely eager to
give these loans out to anybody, at any scale, as fast as they can, because
they can't lose. They have all the equity of the US government to back them
up. The debt-to-equity ratio is effectively zero.

And of course, people who don't understand finance (which they don't teach
you until university; catch-22!) take on lots of these loans in the hope of
making money in the future.

Since anyone who wants to go to university can get a student loan,
American universities keep raising their rates until they find the maximum amount
that lenders are willing to lend (unlimited!) or foolish borrowers are
willing to borrow in the name of the American Dream (so far we haven't found
the limit).

Where was I? Oh right, tech metaphors.

Well, there are two parts here. First, unlimited access to money. Well, the
tech world has had plenty of that, prior to the 2022 crash anyway. The
result is they hired way too many engineers (students) who did a lot of dumb
stuff (going to school) and incurred a lot of tech debt (student loans) that
they promised to pay back later when their team got bigger (they earned
their Bachelor's degree and got a job), which unfortunately didn't
materialize. Oops. They are worse off than if they had skipped all that.

Second, inability to discharge the debt in bankruptcy. Okay, you got me.
Maybe we've come to the end of our analogy. Maybe US government policies
actually, and this is quite an achievement, manage to be even dumber than
tech company management. In this one way. Maybe.

OR MAYBE YOU [OPEN SOURCED WVDIAL](https://apenwarr.ca/log/20091224) AND PEOPLE STILL EMAIL YOU
FOR HELP DECADES AFTER YOUR FIRST STARTUP IS LONG GONE.

Um, sorry for that outburst. I have no idea where that came from.

**Bonus note: bug bankruptcy**

While we're here exploring financial metaphors, I might as well say
something about bug bankruptcy. Although I [have been known to make fun of\\
bug bankruptcy](https://apenwarr.ca/log/20171213), it too is an excellent metaphor, but only if
you take it far enough.

For those who haven't heard of this concept, bug bankruptcy happens when
your bug tracking database is so full of bugs that you give up and delete
them all and start over ("declare bankruptcy").

Like financial bankruptcy, it is very tempting: I have this big pile of
bills. Gosh, it is a big pile. Downright daunting, if we're honest. Chances
are, if I opened all these bills, I would find out that I owe more money
than I have, and moreover, next month a bunch more bills will come and I
won't be able to pay them either and this is hopeless. That would be
stressful. My solution, therefore, is to throw all the bills in the
dumpster, call up my friendly neighbourhood bankruptcy trustee, and
conveniently discharge all my debt once and for all.

Right?

Well, not so fast, buddy. Bankruptcy has consequences. First of all, it's
kind of annoying to arrange legally. Secondly, it sits on your financial
records for like 7 years afterwards, during which time probably nobody will
be willing to issue you any loans, because you're empirically the kind of
person who does not pay back their loans.

And that, my friends, is also how bug bankruptcy works. Although the process
for declaring it is easier -- no lawyers or trustees required! -- the
long-term destruction of trust is real. If you run a project in which a lot
of people spent a bunch of effort filing and investigating bugs (ie. lent
you their time in the hope that you'll pay it back by fixing the bugs
later), and you just close them all wholesale, you can expect that those
people will eventually stop filing bugs. Which, you know, admittedly feels
better, just like the hydro company not sending you bills anymore feels
better until winter comes and your heater doesn't work and you can't figure
out why and you eventually remember "oh, I think someone said this might
happen but I forget the details."

Anyway, yes, you can do it. But refinancing is better.

**Email bankruptcy**

Email bankruptcy is similar to bug bankruptcy, with one important
distinction: nobody ever expected you to answer your email anyway. I'm
honestly not sure why people keep sending them.

ESPECIALLY EMAILS ABOUT WVDIAL where does that voice keep coming from

**Related**

[The evasive evitability of enshittification](https://apenwarr.ca/log/20250530) (2025)

[Bankrupting third-world countries](https://apenwarr.ca/log/20081201) (2008)

**Unrelated**

[Systems design explains the world: volume 1](https://apenwarr.ca/log/20201227) (2020)

I'm CEO at **[Tailscale](https://tailscale.com/)**, where
we make network problems disappear.

**Why would you follow [me on twitter](https://twitter.com/apenwarr)? Use [RSS](https://apenwarr.ca/log/rss.php).**

apenwarr on gmail.com
