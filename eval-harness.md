# Measuring whether an agent actually replaced the work

Notes on the eval problem I keep running into, written up because I keep being asked
about it in conversation and it's easier to argue from a page.

The question is not "is the model good." It's "did the human stop doing the thing."
Those come apart constantly, and almost every harness I've seen measures the first and
reports it as the second.

---

### 1. Measure the human baseline before you touch it

You cannot claim replacement without a number for the thing being replaced, and once
you've shipped the agent that number is gone. So it gets measured first, from
observation, not from someone's estimate of their own job.

Record the distribution, not the mean. The mean task takes four minutes; the one that
takes ninety is the entire reason the workflow exists, and it's the one the agent will
route around silently.

Also record the **exception rate**: what fraction of cases already end with a human
overriding the system. That's your ceiling. An agent that handles everything except the
exceptions has automated the easy half and moved the hard half somewhere less visible.

### 2. Define "done" the way the business does

Not token accuracy, not a rubric score, not the model's own confidence. Done is the
state the operator would have produced: the invoice posted, the record reconciled, the
ticket closed without a callback. If you can't write a predicate that checks it from the
system of record, you don't have an eval, you have a vibe with a decimal point.

### 3. A check with nothing to check must fail, not pass

This is the one that cost me real time. I built a required-field audit over an
application-filling pipeline that validated answers against the form's published schema.
On its first run it reported a **clean fill** on a form with thirteen required fields
blank. It hadn't broken. That vendor publishes no schema, so the audit had nothing to
compare against and passed *vacuously*.

A green check that means "I verified this" and a green check that means "I had no data"
are indistinguishable from outside, and the second is worse than no check at all because
it buys confidence. Every gate I write now has to answer "what did you actually compare?"
and returns a failure when the answer is "nothing." The fix in that case was to stop
trusting the vendor and read the rendered page itself; the unfilled count went 25 → 14 →
7 as each layer landed, and the seven that remained were correct refusals rather than
guesses.

### 4. Report per completed unit of work, end to end

Per-call latency and per-token cost are the numbers that are easy to collect, which is
why they're the ones people publish. They also hide the whole problem. The number that
matters is **time and cost per completed unit, counting the runs that failed and the
exceptions a human had to resolve.**

Here's what that difference looked like on my own pipeline. Read off its config, it
processed 40 items a day. Read off its event log: 49 attempts, 7 clean completions,
6.2 minutes per attempt, **42 minutes per completed item.** By hand, about four. It was
roughly ten times slower than the thing it was replacing, and it had been reporting
healthy the entire time, because every individual call succeeded.

That's also the answer to routing. Once cost has a denominator of *completed units*, the
frontier-versus-open-model question stops being ideological. A cheaper model that halves
your completion rate is more expensive, and you can show it.

### 5. Be willing to publish the number that says you lost

The pipeline above is a drafting tool now. That's the finding, and I'd rather have it
than the version where I never checked. An eval harness that has never once told you to
kill something isn't measuring; it's decorating.

---

*Mike Fornal · [forn.al](https://forn.al)*
