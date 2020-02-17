# How I got a job in industry

I often get asked how I landed a job in industry after my postdoc. After my PhD at McGill, I started a postdoc at UCLA in July 2014. After about 6 months, like many a postdoc I started to got worried about my financial security and academic job prospects. So I started exploring jobs outside of academia.

## Getting a recruiter on the line

I dusted off my CV and arranged it in a way that I thought would highlight what the market wanted. In early 2015 that would have meant deep learning, machine learning, data science and big data. I honestly didn't really know what each of these things actually meant in the real world but I thought it would help me get a job so I put it in there. I uploaded it on LinkedIn and pretty soon I was getting emails from recruiters in finance and tech.

This part of the process (why you get calls or not and from whom) is completely opaque to me. I think that when you're often on LinkedIn and update your CV some ML pipeline picks it up and marks you as actively looking for a job and give you a higher ranking in searches. I also presume that some recruiters have lists of *hot* universities where they look for candidates - UCLA is a hotspot for math research (Terrance Tao is there). This is why, I assume, I got contacted by a lot of finance recruiters.

Something else that might have tipped the balance is that I used to do development professionally before grad school, and ran an open source project. It probably also helped that I'd been working in Python on and off since 2006. So I was also getting contacted by tech recruiters.

Rant: no one in industry is using Matlab, and as a PI if you force your grad students to use Matlab you're really hurting their future job prospects outside of academia (99% of grad students end up not in academia).

## The thing about recruiters is...

Recruiters get paid a substantial commission when a candidate gets hired. They also have to sift through a see a people who are just looking, are a poor fit, or who will ultimately bomb the interview. So you will get a lot of emails about things which are seemingly unrelated to your skills (hey do you want to develop a Java server pages app for transportation logistics? was a memorable one). 

OTOH if you have good rapport with a recruiter they can be real buds and advocate for you when finding a job. They will prep you for interviews and give you a lot of context you need in these scary times. They're also generally nice people since they have to deal with people a lot. So, be nice to recruiters.

## The types of jobs out there

I was getting cold-called about a lot of different jobs with adult-sounding titles and I didn't quite know what they meant at the time.

They included things like:

* Research scientist: the closest thing to postdoc in industry. Develop your own research agenda. Sweet gig.
* Research engineer: someone who can code research ideas. If working on ML, that might mean being real good with CUDA. 
* Software engineer: in a tech company, a jack-of-all-trades position that can run the gamut from doing kernel stuff to writing JS for a front-end app to doing pipelines of exabyte datasets. In a finance company, someone who writes C++.
* Data scientist: a statistician with working knowledge of SQL. 
* Data engineer: someone who does the piping on exabyte datasets.

Of course, there are many other jobs out there for a person with a PhD, like teacher, science communicator, or dog photographer to the stars - these just happen to be the jobs that I was getting calls about.

One thing you need to be aware of is that even within one company there can be multiple pipelines for hiring, especially for research. If you interview for a general software engineering job at Google you're unlikely to get matched to Google Brain; Brain has its own posted job offers which generally have research-something-or-other in their title. Something people will try is to get in through the front door (in tech companies, software engineer) and get transfered to a research job within a couple of years. I know a lot of very smart people who went through this route, it is definitely possible. However, if you just want to be considered for research job you can also make it clear to your recruiter; just know that those jobs are a lot harder to get.

## Prepping for interviews

Generally you'll get a prep call with a recruiter, and then a phone screen. In a phone screen, they'll ask you technical questions that are sufficiently straightforward that they can be answered in a shared google doc or over the phone. These questions may be about:

* Algorithms and data structures (for a software engineering role)
* System design (software)
* Basic stats (data science)
* Basic finance math (finance)
* ML (research position)
* Are you a good person or someone who will make work miserable? (behavioural questions)

Your recruiter will help you prep for the phone screen, however the book everybody recommends is [Cracking the Coding Interview](https://www.amazon.ca/Cracking-Coding-Interview-Programming-Questions/dp/098478280X). This gives you prep questions about algorithms and about behaviour. 

People give preparing for technical interviews a bad reputation. It's a lot like GREs - you can either use it as an opportunity to brush up on your knowledge, and love it, or it can feel like a miserable slog. I personally loved it. Being self-taught in programming, I had never done anything theoretical data structures and algorithms, so I was really happy to go through [Algorithms and Data Structures with Tim Roughgarden](https://www.coursera.org/specializations/algorithms). I don't think it's an exaggeration to say that it was life changing - a revelation. All of a sudden the range of problems that I could tackle with code blew up.

I also followed an edX curriculum on data science, which I didn't like as much - I felt like I already knew most of the theoretical things that were thought and the rest sounded just okay (using Spark). With hindsight, it introduced me to out-of-core computation, pandas and ggplot which obviously wasn't a waste of time.

I went to a data science meetup in LA and met somebody (now a friend) who wanted to work on a Kaggle problem together. I learned a lot from that (it's probably the first time I used sklearn!). We finished in the top 5% so I also had something to put on my CV about my supposed knowledge of machine learning.

I also picked up a book on portfolio theory for finance interviews. Give yourself a solid 4-8 weeks to prep for your interviews, and do a little bit of prep everyday, with a sprint on the weekends.

## Bombing different interviews

I have a friend who is trying to date better so as guy-who-has-dated (I'm married now) I recommended that she go on a different date every night for a whole week. The idea is you to push yourself out of the scarcity mentality (there's no one out there for me) and move towards an abundance mentality (there's too many people out there for me! I better be selective!). What I failed to warn her about is that if you do that you will also inevitably have a lot of failed awkward dates, which is part of the often arbitrary, fickle process.

I had a lot of failed, awkward interviews. I flew to London for a two day interview with a finance company (one of their researchers had been a PhD student with David Mackay! I love London!). I did ok on the technical questions but completely bombed my interview once I inquired about their policy for publishing research (most finance places don't allow you to publish, [with some notable exceptions](https://ieeexplore.ieee.org/abstract/document/6114424)).

I had an interview in Chicago with another finance company (I stayed in the fancy Trump Hotel! I wore a suit and tie! Pre-2016 were different times!). I did ok on the technical and they just had one more interview loop - a 4 hour behavioural interview with a psychologist in a hotel next to LAX! I started crying around the one hour mark when he started asking about my relationship with my dad (he passed away in 2008 and I never really got over it). I never really recovered after that. But then I got a free therapy session so there's that.

There was an interview with a secretive Bay Area ML stealth-mode startup, where I showed some monkey physiology research to a confused crowd during lunchtime. I can still remember the smell of the lemon salmon in that room.

There was that one time I brushed off the CTO of an LA startup when he asked about whether I had cross-validated my results. I was like - would I show results if they weren't cross-validated? Apparently a lot of candidates did! And of course there was that one time I spent 2 hours out of of a three hour technical test debugging some weird corner issue in pandas that was causing my ipython kernel to crash.

In general, I would say:

* Don't be an asshole - sometimes people ask seemingly dumb questions because a lot of people in their applicant pool can't answer these questions. If you answer as though a question is beneath you, that's a huge red flag.
* Keep talking and you'll be fine. The number one mistake people do in whiteboard interviews is they freeze when they don't know the answer. One thing that saved me in one interview is starting to talk about an almost completely unrelated problem where I found that you could solve it in O(sqrt(N)) memory because of a scheme I had thought was pretty clever. The interviewer seemed to agree that it was and helped me make that scheme work for the problem on the whiteboard. 
* Keep the tears on the inside. This only happened once during that weird behavioural battery test - it was one of the most surreal experiences of my life. It was sort of like someone [asking me the 36 questions](https://www.nytimes.com/2015/01/11/style/36-questions-that-lead-to-love.html) and I was not in it for that. I could have just walked out and saved myself another two hours. 
* You don't have to keep going when you're in an interview where you know the person you're talking to is trying to sell you magic beans. Silicon Valley hype is real and your BS detector must be finely attuned if you don't want to end up at "Uber, but for dogs" (actual phone pitch).
* Don't be an asshole - seriously, people won't want to work with you if you're a jerk. 
* Practice makes perfect. One rejection is sad. 10 rejections is much less than 10X as sad. Some rejections might even make you feel happy. Get back on the horse.

I think the most humiliating part for me is that I was broke and I had to ask for reimbursement after rejections sometimes. I had lost my passport for a couple of months so I had to take the bus from LA to SF for some Bay Area interviews, so you can imagine my sad sad emails asking for reimbursing 50$ for a bus ticket.

# I took a jerb

After failing many times I ended up in a SWE interview at Google, kept my composure and said good enough words in approximately the right order. It took 5 months from "I need a job" to "I have a job offer". 

For a postdoc it might be easier to go to a giant tech company than a highly specialized startup. I didn't have a lot of marketable real world skills at this point. I distinctly remember being completely lost during Noogler training when they taught us about their source control and having to ask the guy next to me what a source control was. His answer: it's like git. Next question: what's a git? etc. 

Big tech companies will take a chance on someone who's smart and willing to be trained. Startups generally want someone who is productive on day one (spoiler: I was not productive on day one). Then you learn a bunch of stuff and you put *giant tech company* on your resume. People who you cold call about jobs or research suddenly reply to your emails. 

There's a lot of internal mobility and it's in everyone's interest to land in a place where you can eventually be productive and do something interesting. After about three months at Google it was pretty clear that I was no Jeff Dean but I was a pretty sharp data scientist and I knew a thing or two about visual perception so I ended up doing a mishmash of both. 

Of course once you've got that first job it's easy enough to get a job elsewhere, and people recommend switching jobs every 18 to 24 months to maximize your compensation. I did this after 18 months, going to Facebook to work on BCI. 

So that's how I did it. But should you do it? That's a whole other thing.