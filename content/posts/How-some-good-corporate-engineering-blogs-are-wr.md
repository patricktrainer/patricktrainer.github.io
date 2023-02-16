
---
    title: How-some-good-corporate-engineering-blogs-are-wr
    date: 2021-01-01    
    draft: true
    tags: []
---
# How-some-good-corporate-engineering-blogs-are-wr# How (some) good corporate engineering blogs are written
Created: March 29, 2020 8:56 AM
URL: https://danluu.com/corp-eng-blogs/
I've been comparing notes with people who run corporate engineering blogs and one thing that I think is curious is that it's pretty common for my personal blog to get more traffic than the entire corp eng blog for a company with a nine to ten figure valuation and it's not uncommon for my blog to get an order of magnitude more traffic.
To try to understand what companies with good corporate engineering blog have in common, I interviewed folks at three different companies that have compelling corporate engineering blogs (Cloudflare, Heap, and Segment) as well as folks at three different companies that have lame corporate engineering blogs (which I'm not going to name).
At a high-level, the compelling engineering blogs had processes that shared the following properties:
- Easy approval process, not many approvals necessary
- Few or no non-engineering approvals required
- Implicit or explicit fast [SLO](https://en.wikipedia.org/wiki/Service-level_objective) on approvals
- Approval/editing process mainly makes posts more compelling to engineers
- Direct, high-level (co-founder, C-level, or VP-level) support for keeping blog process lightweight
The less compelling engineering blogs had processes that shared the following properties:
- Slow approval process
- Many approvals necessary
- Significant non-engineering approvals necessary
- Non-engineering approvals suggest changes authors find frustrating
- Back-and-forth can go on for months
- Approval/editing process mainly de-risks posts, removes references to specifics, makes posts vaguer and less interesting to engineers
- Effectively no high-level support for blogging
- Leadership may agree that blogging is good in the abstract, but it's not a high enough priority to take concrete action
- Reforming process to make blogging easier very difficult; previous efforts have failed
- Changing process to reduce overhead requires all "stakeholders" to sign off (14 in one case)
- Any single stakeholder can block
- No single stakeholder can approve
- Stakeholders wary of approving anything that reduces overhead
- Approving involves taking on perceived risk (what if something bad happens) with no perceived benefit to them
One person at a company with a compelling blog noted that a downside of having only one approver and/or one primary approver is that if that person is busy, it can takes weeks to get posts approved.
Here are the processes, as described to me, for the three companies I interviewed (presented in `sha512sum` order, which is coincidentally ordered by increasing size of company, from a couple hundred employees to nearly one thousand employees):
### Heap
- Someone has an idea to write a post
- Writer (who is an engineer) is paired with a "buddy", who edits and then approves the post
- Buddy is an engineer who has a track record of producing reasonable writing
- This may take a few rounds, may change thrust of the post
- CTO reads and approves
- Usually only minor feedback
- May make suggestions like "a designer could make this graph look better"
- Publish post
The first editing phase used to involve posting a draft to a slack channel where "everyone" would comment on the post.
### Segment
- Someone has an idea to write a post
- Often comes from: internal docs, external talk, shipped project, open source tooling (built by Segment)
- Writer (who is an engineer) writes a draft
- May have a senior eng work with them to write the draft
- Until recently, no one really owned the feedback process
- Calvin French-Owen (co-founder) and Rick (engineering manager) would usually give most feedback
- Maybe also get feedback from manager and eng leadership
- Typically, 3rd draft is considered finished
- Now, have a full-time editor who owns editing posts
- Also socialize among eng team, get get feedback from 15-20 people
- PR and legal will take a look, lightweight approval
Some changes that have been made include
- At one point, when trying to establish an "engineering brand", making in-depth technical posts a top-level priority
- had a "blogging retreat", one week spent on writing a post
- added writing and speaking as explicit criteria to be rewarded in performance reviews and career ladders
Although there's legal and PR approval, Calvin noted "In general we try to keep it fairly lightweight.
### Cloudflare
- Someone has an idea to write a post
- Internal blogging is part of the culture, some posts come from the internal blog
- John Graham-Cumming (CTO) reads every post, other folks will read and comment
- John is approver for posts
- Matthew Prince (CEO) also generally supportive of blogging
- "Very quick" legal approval process, SLO of 1 hour
- This process is so lightweight that one person didn't really think of it as an approval, another person didn't mention it at all (a third person did mention this step)
- Comms generally not involved
One thing to note is that this only applies to technical blog posts.
### Cloudflare
- [https://blog.cloudflare.com/how-verizon-and-a-bgp-optimizer-knocked-large-parts-of-the-internet-offline-today/](https://blog.cloudflare.com/how-verizon-and-a-bgp-optimizer-knocked-large-parts-of-the-internet-offline-today/)
- Talks about a real technical problem that impacted a lot of people, reasonably in depth
- Timely, released only eight hours after the outage, when people were still really interested in hearing about what happened; most companies can't turn around a compelling blog post this quickly or can only do it on a special-case basis, Cloudflare is able to crank out timely posts semi-regularly
- [https://blog.cloudflare.com/the-relative-cost-of-bandwidth-around-the-world/](https://blog.cloudflare.com/the-relative-cost-of-bandwidth-around-the-world/)
- Exploration of some data
- [https://blog.cloudflare.com/the-story-of-one-latency-spike/](https://blog.cloudflare.com/the-story-of-one-latency-spike/)
- A debugging story
- [https://blog.cloudflare.com/when-bloom-filters-dont-bloom/](https://blog.cloudflare.com/when-bloom-filters-dont-bloom/)
- A debugging story, this time in the context of developing a data structure
### Segment
- [https://segment.com/blog/when-aws-autoscale-doesn-t/](https://segment.com/blog/when-aws-autoscale-doesn-t/)
- Concrete explanation of a gotcha in a widely used service
- [https://segment.com/blog/gotchas-from-two-years-of-node/](https://segment.com/blog/gotchas-from-two-years-of-node/)
- Concrete example and explanation of a gotcha in a widely used tool
- [https://segment.com/blog/automating-our-infrastructure/](https://segment.com/blog/automating-our-infrastructure/)
- Post with specific details about how a company operates; in theory, any company could write this, but few do
### Heap
- [https://heap.io/blog/engineering/basic-performance-analysis-saved-us-millions](https://heap.io/blog/engineering/basic-performance-analysis-saved-us-millions)
- Talks about a real problem and solution
- [https://heap.io/blog/engineering/clocksource-aws-ec2-vdso](https://heap.io/blog/engineering/clocksource-aws-ec2-vdso)
- Talks about a real problem and solution
- In HN comments, engineers (malisper, kalmar) have technical responses with real reasons in them and not just the usual dissembling that you see in most cases
- [https://heap.io/blog/analysis/migrating-to-typescript](https://heap.io/blog/analysis/migrating-to-typescript)
- Real talk about how the first attempt at driving a company-wide technical change failed
One thing to note is that these blogs all have different styles.
