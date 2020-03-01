I often get asked how I landed a job in industry after my postdoc. After my PhD at McGill, I started a postdoc at UCLA in July 2014. After about 6 months, like many a postdoc I started to got worried about my financial security and academic job prospects. So I started exploring jobs outside of academia. Here's my short guide to getting a job in industry.

### Getting a recruiter on the line

I dusted off my CV and arranged it in a way that I thought would highlight hot marketable trends and skills. [You can see what it might have looked like](https://www.dropbox.com/s/qx66dpl39b0hdoz/pro-cv-machinelearningresearcher.pdf?dl=0). This is not quite the CV I used to get the job (I had many versions going around) but it's around the right time and had most of the stuff in. Looking at the CV now it's pretty clear that I was keyword stuffing and I could have cut down the content by 30%. UML! Numeric C! Actionscript! Deep learning! Please hire me I know computer things!

Three types of people will look at your CV (and LinkedIn profile):

* Recruiters. They are the gatekeepers.
* Engineers and researchers who will not interview you (for some specialized roles only). They'll look at the CVs the recruiters send their way and decide whether you're a fit.
* Engineers that are interviewing you and might ask questions about something listed on your CV.

People agonize over how their CVs are arranged, but honestly I think the only thing that matters is 1) the algorithm that ranks you on LinkedIn and puts you in front of recruiters and 2) making the content not aggravating by engineers that will actually have printed your CV. My CV definitely optimized for the first thing although at that time I had no clue.

Why you get calls or not and from whom is completely opaque to me. When you're often on LinkedIn and update your CV an ML pipeline probably picks it up and marks you as actively looking for a job and gives you a higher ranking in searches. You can also mark yourself as actively looking for a job. I also presume that some recruiters have lists of *hot* universities where they look for candidates - UCLA is a hotspot for math research - Terrance Tao is there - so I assume, I got contacted by a lot of finance recruiters.

Something else that might have tipped the balance is that I used to do development professionally before grad school, and ran an open source project. It probably also helped that I'd been working in Python on and off since 2006. I put that in the CV as well. So I was also getting contacted by tech recruiters. 

### The thing about recruiters is...

Recruiters get paid a substantial commission when a candidate gets hired. They have to sift through a see a people who are just looking, are a poor fit, or who will ultimately bomb the interview. Generally they tend not to be technical people (although some recruiters are quite technically inclined especially for more specialized roles). You will get a lot of emails about things which are seemingly unrelated to your skills. 

If you have good rapport with a recruiter they can be real buds and advocate for you when finding a job. They will prep you for interviews and give you a lot of guidance you need in these scary times. They're also generally nice people since they have to deal with people a lot. So, be nice to recruiters.

### The types of jobs out there

I was getting cold-called about a lot of different jobs with adult-sounding titles and I didn't quite know what they meant at the time.

They included things like:

* Research scientist: the closest thing to postdoc or PI in industry. Develop your own research agenda. Sweet gig. Stressful.
* Research engineer: someone who can code research ideas. If working on ML, that might mean being real good with CUDA. Two people you might know who are in research engineer roles: Francois Chollet (keras) and Soumith Chintala (PyTorch)
* Software engineer: in a tech company, a jack-of-all-trades position that can run the gamut from doing kernel stuff to writing JS for a front-end app to doing pipelines on exabyte datasets. Highly respected at tech companies, drives a lot of the research. At a finance company, someone who writes C++, not so highly respected.
* Data scientist: in some places, especially big tech companies, a statistician (or, rarely, a washed-up computational neuroscientist). In others, a programmer who works on data pipelines and does a bit of stats and maybe ML. Extremely variable role. 
* Quant: a data scientist of the statistician variety or maybe ML in a finance firm.
* Data engineer: someone who does the piping on exabyte datasets but not the stats.
* Business Intelligence: someone who does stuff in Excel.
* Consultant: I've asked people many times what a consultant does and have yet to figure it out. I'm pretty sure it's someone with an MBA.

There's a lot of title inflation in startups. CTO! Senior architect! These titles are only really meaningful when you start to have a medium-sized business (past series A, at least 50 employees), and even then it's almost entirely made up. It varies tremendously from place to place. On the other hand, at a place like Google a senior software engineer means a very specific thing - with a level, a comp, years of experience, etc. So unless you're applying for a big company don't worry too much about the title - and at a big company they will determine your level anyway, so don't worry about it either.

Of course, there are many other jobs out there for a person with a PhD, like teacher, science communicator, or dog photographer to the stars - these just happen to be the jobs that I was getting calls about.

One thing you need to be aware of is that even within one company there can be multiple pipelines for hiring, especially for research. If you interview for a general software engineering job at Google you're unlikely to get matched to Google Brain; Brain has its own posted job offers which generally have research-something-or-other in their title. Candidates will often try to get in through the front door (in tech companies, as software engineer) and get transfered to a research job within a couple of years. I know a lot of very smart people who went through this route, it is definitely possible, but it's a gamble. However, if you just want to be considered for a research job you can also make it clear to your recruiter; just know that those jobs are a lot harder to get.

### Prepping for interviews

Generally you'll get a prep call with a recruiter, and then a phone screen. In a phone screen, they'll ask you technical questions that are sufficiently straightforward that they can be answered in a shared google doc or over the phone. These questions may be about:

* Algorithms and data structures (for a software engineering role)
* System design (software)
* Basic stats (data science)
* Basic finance math (finance)
* ML (research position)
* Are you a good person or someone who will make work miserable? (behavioural questions)

Your recruiter will help you prep for the phone screen, however the book everybody recommends is [Cracking the Coding Interview](https://www.amazon.ca/Cracking-Coding-Interview-Programming-Questions/dp/098478280X). This gives you prep questions about algorithms (highly specific to SWE jobs and tech jobs in general) and about behaviour (good to remember). 

People give preparing for technical interviews a bad reputation. It's a lot like GREs - you can either use it as an opportunity to brush up on your knowledge, and love it, or it can feel like a miserable slog. I personally loved it. Being self-taught in programming, I had never done anything theoretical data structures and algorithms, so I was really happy to go through [Algorithms and Data Structures with Tim Roughgarden](https://www.coursera.org/specializations/algorithms). I don't think it's an exaggeration to say that it was life changing - a revelation. All of a sudden the range of problems that I could tackle with code blew up.

I also followed an edX curriculum on data science, which I didn't like as much. I felt like I already knew most of the theoretical things that were taught and the rest wasn't very useful to me at the time (using Spark). With hindsight, it introduced me to out-of-core computation, pandas and ggplot, so it was actually very useful.

I went to a data science meetup in LA and met somebody (now a friend) who wanted to work on a Kaggle problem together. I learned a lot from that (it's probably the first time I used sklearn!). We finished in the top 5% so I also had something to put on my CV about my supposed knowledge of machine learning.

I also picked up a book on portfolio theory for finance interviews. Give yourself a solid 4-8 weeks to prep for your interviews, and do a little bit of prep everyday, with a sprint on the weekends.

### Styles of interviews

I mostly dealt with run-of-the-mill whiteboard interviews (standard for tech jobs but also common for finance). Read the coding interview book to figure out how these work. I had other types of interviews/screens as well:

* Take home assignments. Common for data science. Don't be too smart and don't take longer than you should. If you bomb it's great practice for the next one.
* Timed exams in secret bunker locations. Had a few of these for finance. Nerve-wracking.
* Presentations. If about your own research, don't pander by throwing in buzzwords; just do it like an academic talk. If about their problem (linked to take-home assignment), doing one creative thing is fine.

I have a friend who got asked a Fermi estimation question! I've never gotten one of those, but I really wish I did - they're super fun.

### Bombing different interviews

I have a friend who is trying to date better so as guy-who-has-dated (I'm married now) I recommended that she go on a different date every night for a whole week. The idea is you to push yourself out of the scarcity mentality (there's no one out there for me) and move towards an abundance mentality (there's too many people out there for me! I better be selective!). What I failed to warn her about is that if you do that you will also inevitably have a lot of failed awkward dates, which is part of the often arbitrary, fickle process of dating.

I had a lot of failed, awkward interviews. I flew to London for a two-day interview with a finance company (one of their researchers had been a PhD student with David Mackay! I love London!). I did ok on the technical questions but completely bombed my interview once I inquired about their policy for publishing research (most finance places don't allow you to publish, [with some notable exceptions](https://ieeexplore.ieee.org/abstract/document/6114424)).

I had an interview in Chicago with another finance company (I stayed in the fancy Trump Hotel! I wore a suit and tie! Pre-2016 was different!). I did ok on the technical and they just had one more interview loop - a 4 hour behavioural interview with a psychologist in a hotel next to LAX! I started crying around the one-hour mark when he started asking about my relationship with my dad (he passed away in 2008 and I never really got over it). I never really recovered after that. But then I got a free therapy session out of it so there's that.

There was an interview with a secretive Bay Area ML stealth-mode startup, where I showed some monkey physiology research to a confused crowd during lunch time. I can still remember the smell of the lemon salmon in that room.

There was that one time I brushed off the CTO of an LA startup when he asked about whether I had cross-validated my results. I was like - would I show results if they weren't cross-validated? Apparently a lot of candidates did! There was one time I spent 2 hours out of of a three hour technical test debugging some weird corner issue in pandas that was causing my ipython kernel to crash on their sample dataset.

Every interview you will become a little bit better and a little stronger. Pace yourself.

### Showing your best self

* Don't be a jerk - sometimes people ask seemingly dumb questions because a lot of people in their applicant pool can't answer these questions. If you answer as though a question is beneath you, that's a huge red flag.
* Keep talking and you'll be fine. The number one mistake people do in whiteboard interviews is they freeze when they don't know the answer. One thing that saved me in one interview is starting to talk about an almost completely unrelated problem where I found that you could solve it in O(sqrt(N)) memory because of a scheme I had thought was pretty clever. The interviewer seemed to agree that it was pretty clever and helped me make that scheme work for the problem on the whiteboard. 
* If it's because it became clear that a business isn't a good fit after a phone screen, don't feel obligated to keep going. Your interviewers will feel relief when they see "interview cancelled" and you haven't wasted their time. Once you realize that exciting startup is really "Uber, but for dogs" (actual phone pitch), you can just say thanks but no thanks.
* Don't be a jerk - seriously, people won't want to work with you if you're a jerk. The
* Practice makes perfect. One rejection is sad. 10 rejections isn't. Get back on the horse.

I think the most humiliating part for me is that I was broke and I had to ask for reimbursement after rejections sometimes. I had lost my passport for a couple of months so I had to take the bus from LA to SF for some Bay Area interviews. Imagine my sad sad emails asking for reimbursing 50$ for a bus ticket. I still cringe thinking.

## I took a jerb

After failing many times I ended up in a SWE interview at Google, kept my composure and said good enough words in approximately the right order. It took about 5 months from "I need a job" to "I have a job offer". 

At that point you'll have to deal with acquiring a work visa if you're not in your own country. In the US that means getting an H1B which is brutal - these days H1Bs get handed out once a year and they don't fill all the requests so you might have to wait a couple years in a remote office to actually get to your dream job. It's no joke! As a Canadian though it's easy peasy - show up at the border, get visa. The company will pay for your visa. 

There's negotiation over comp but the only way to get better comp in many places is to have a competing offer, and I didn't know that so I took the offer they gave me. That was 4.5X was I was making as a postdoc so I couldn't fathom asking for more anyway. Job offer to job start took 3 months because of the visa wait and finishing the last bit of my postdoc.

### Silicon Valley things

The giant tech companies have vastly different ratings on [employer ratings sites](https://www.glassdoor.com/blog/best-tech-companies-2019/) (i.e. Glassdoor), and this reflects that these places have vastly different cultures that may or may not lead to thriving happy humans. Facebook and Google always make the top 5. You'll have to scroll down a lot to see Apple, and Amazon and Netflix are nowhere to be seen. A lot of Facebook early employees came from Google and they share a lot of the same don't-be-a-jerk culture. Apple is secretive and that can make it isolating. [Amazon is grueling according to the nytimes](https://www.nytimes.com/2015/08/16/technology/inside-amazon-wrestling-big-ideas-in-a-bruising-workplace.html). Read the reviews before you sign an offer!

For a postdoc it might be easier to go to a giant tech company than a highly specialized startup. I didn't have a lot of marketable real world skills at this point. I distinctly remember being completely lost during Noogler training when they taught us about their source control and having to ask the guy next to me how to use their command line source control tool. His answer: it's like the git command line. Next question: how does the git command line work? I had only used the GUI! 

Big tech companies will take a chance on someone who's smart and willing to be trained. Startups generally want someone who is productive on day one (spoiler: I was not productive on day one). Then you learn a bunch of stuff and you get to put *giant tech company* on your resume. People suddenly reply to your emails. It's a pretty sweet deal. 

At big tech companies, most jobs get hired into a big pool and they'll figure out your team later. Yeah! Weird system right? I matched with a team almost entirely at random and ended up in what turned out was the perfect spot - with a bunch of statisticians. I learned a lot of stats! 

There's a lot of internal mobility and it's in everyone's interest to land in a place where you can eventually be productive and do something interesting. After about three months at Google it was pretty clear that I was no Jeff Dean but I was a pretty sharp data scientist and I knew a thing or two about visual perception so I ended up doing a mix of both. 

Of course once you've got that first job, it's a lot easier to get a job elsewhere, and people recommend switching jobs every 18 to 24 months to maximize your compensation. I was a lot wiser for the second round, and when a recruiter from Facebook contacted me about a data engineer job, I told them I was only interested in the brain-computer interface work that I had read about in an [news article](https://mashable.com/2017/01/12/facebook-job-postings-building-8/). That was a highly specialized gig so I went through a completely different - and much faster - pipeline. It took a couple of weeks from initial call to offer, and I was way less stressed because I had been through the ringer.

So that's how I did it. AMA.