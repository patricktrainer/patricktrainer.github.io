
---
    title: Algorithms-interviews-theory-vs-practice
    date: 2021-01-01    
    draft: true
    tags: []
---
# Algorithms-interviews-theory-vs-practice# Algorithms interviews: theory vs. practice
Created: May 23, 2020 11:28 AM
URL: https://danluu.com/algorithms-interviews/
When I ask people at trendy big tech companies why algorithms quizzes are mandatory, the most common answer I get is something like "we have so much scale, we can't afford to have someone accidentally write an `O(n^2)` algorithm and bring the site down"[1](https://danluu.com/algorithms-interviews/).
Both the examples in this post as well as the ones I haven’t included have these properties:
- The example could be phrased as an interview question
- If phrased as an interview question, you'd expect most (and probably) all people on the relevant team to get the right answer in the timeframe of an interview
- The cost savings from fixing the example is worth more annually than my lifetime earnings to date
- The example persisted for long enough that it's reasonable to assume that it wouldn't have been discovered otherwise
At the start of this post, we noted that people at big tech companies commonly claim that they have to do algorithms interviews since it's so costly to have inefficiencies at scale.
I actually worked at a company that used the strategy of "don't ask algorithms questions in interviews, but do incentivize things that are globally good for the company".
Another trend at the time was for behavioral interviews and a number of companies I interviewed with had 100% behavioral interviews with zero technical interviews.
Some companies will give very large out-of-band bonuses to people regularly, but that work wasn't for a company that does a lot of that, so there's nothing the company could do to indicate that it valued additional work once someone did "enough" work to get the best possible rating on a performance review.
But even for companies that do, most people don't have jobs where they're designing high-scale algorithms (maybe they did at Google circa 2003, but from what I've seen at three different big tech companies, most people's jobs are pretty light on algorithms work).
[[return]](https://danluu.com/algorithms-interviews/)
The reason it's arguably zero is that the only software interview where I inarguably got a "real" interview and was coming in cold was at Google, but that only happened because the interviewers that were assigned interviewed me for the wrong ladder -- I was interviewing for a hardware position, but I was being interviewed by software folks, so I got what was basically a standard software interview except that one interviewer asked me some questions about state machine and cache coherence (or something like that).
