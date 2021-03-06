---
date: 2020-04-27T23:00:00Z
hero_image: "/content/images/sonja-punz-N47B_zibNGo-unsplash.jpg"
title: 'Beyond algorithms: a discussion with Philip Schrodt'
author: Daniel Roy

---
It was during the second week of confinement, late at night, in the French countryside, that I discovered the world of ‘event data’. I was contemplating how to apply NLP techniques on 1919 press articles, in order to model the public and equity markets response to the Spanish flu.

One query calling onto another, google finally led me to Philip’s work. It is always quite a moment, when you discover such a body of expertise at the intersection of data, machine learning, epistemology and political history. I went through his presentations, writings - I highly recommend the reading of ‘[Patterns, Rules and Learning](http://eventdata.parusanalytics.com/papers.dir/Schrodt.PRL.2.0.pdf "Patterns, Rules and Learning")’. This post is the fruit of the conversations that followed.

Before going further, let’s first introduce Philip. To best describe his profession would be to refer to him as a ‘political scientist’. He is well known for his work in automated data and political news event coding. In particular, he built the [Kansas Event Data System](https://en.wikipedia.org/w/index.php?title=Kansas_Event_Data_System&action=edit&redlink=1) (KEDS), that won the “_Outstanding Computer Software Award_” from the [American Political Science Association](https://en.wikipedia.org/wiki/American_Political_Science_Association) in 1995. Fascinatingly, Philip’s work stands at the intersection of apparently disjoint universes. Notably, Schrodt’s work were successfully incorporated into the predictive algorithms used by Lockheed Martin’s Integrated Conflict Early Warning System. In 2014, he left his job as professor at Penn to found [Parus Analytics](http://philipschrodt.parusanalytics.com/. "Parus Analytics").

_Hi Philip - so I guess my first question would be… why? what was your initial motivation for choosing historical/event data as your field of study? You stand at the intersection of a fairly complex Venn diagram…_

I was trained as an applied mathematician but that approach never took off in mainstream political science (cost/benefit ratio never worked out -- too little payback for the amount of training required, whereas by around 1990 the payoff was definitely there for high-level statistics (and now machine learning) so that, rather than modelling, is where the field went (which is fine: certainly did okay by that), and the very interesting efforts in artificial intelligence back in the 1980s were premature.

![](/content/images/suewz.jpg)

_When first reading you, I was struck by our shared preference for simple modes. During my years in banking, I saw an arm race towards ever more complex models. Complexity justifies many headcount in banks/hedge funds as well as data providers (Reuters, Bloomberg, ‘alternative data’ etc.) In reality a few variables can often efficiently and more elegantly explain and model reality. Why do simple models work? Are series, more correlated than most people believe?_

The first reason is the one you indicate: series are sufficiently correlated that you pretty quickly hit a point where you've got all of the signal that is available.

The second, which one sees in most Machine Learning literature now, is over-fitting (less an issue with Machine Learning methods, which almost always are evaluated in split samples, but relevant to the older statistical approaches which tended to evaluated in-sample, at least in the academic work.)

Third is the failure to consider what the intrinsic unpredictability of a process is -- that is, aspects which are going to be random for an open complex process in any conceivable data set, due to things like weather, earthquakes, uh, virus pandemics. Closely related -- Kahneman talks about this a lot -- is the very strong psychological tendency to build retrospective stories that make outcomes seem to have less randomness than they do.

“_The longer you look back, the farther you can look forward._” _I love that quote of Winston Churchill. Let’s talk about data sets and particularly long-term event series. At the difference of stock price series, readily available, it is a piece of work in itself to generate events datasets. Is there some unified corpus?_

Well, as you've probably already picked up, yes, I think a lot could be learned -- I spend a _lot_ of time reading history -- but at the moment we don't really have much in the way of long historical time series (and, for example, we've got the Correlates of War data that cover 1815 to the present, but that crosses a huge change in technology (mainly the mechanization of warfare) and political organization (colonization and then decolonization) whereas we'd probably learn more if we had the same thing over a period when things were more constant (say the "gunpowder empires" era of about 1400CE - 1820CE or so).

One of my hopes from Natural Language Processing is people will figure out way to extract these from existing records (say Wikipedia, which isn't flawless but is reasonably good or Financial Times or New York Times), since any such project will be \[way\] too big for human coding (which is not nearly as good, or consistent, as the coders tend to believe...).

![](/content/images/gabriel-sollmann-Y7d265_7i08-unsplash.jpg)

Several years ago, for example, I heard a presentation by some guy, I think from Harvard, who had done this with a bunch of biographies of Chinese high-level bureaucrats (Ming dynasty maybe?), that sort of thing. Various people have, in fact, applied older, human-coding methods to some of that diplomatic correspondence (e.g. the pre-WWI and Suez crises, which are quite accessible, and even more so with modern OCR methods) but I can't think of much that has come from it beyond that the qualitative studies. Though also they were mostly using older statistical approaches. The Santa Fe Institute has been doing a lot of stuff on internal political and economic dynamics in Renaissance Florence.

_Although, aren’t we too often satisfying ourselves with models perfect at describing the present, and fitting with the dataset, even if split, with no real predictive value? Recommender systems, for instance, are falsely predictive. They reveal what already exists. How to imagine models able to more dynamically ‘predict’?_

The whole SFI "complex adaptive systems" approach did a huge amount on this, particularly in its early phases of SFI (lots of books, articles, competitions of best approaches etc). But, as evidenced by the fact that almost all work is still being done with essentially five methods (logistic, neural networks, random forests, nearest neighbor, and, conversely, separation methods like SVM) nothing turned up the was consistently useful. SFI (and, big time, DARPA) invested vast amounts of money in agent-based models and while they've been useful in a few domains (traffic modelling, apparently) they haven't generalised. Not to say something else won't show up -- and in ML, both random forests and the gadzillion variants on deep neural nets have been recent game changers in quite a few domains -- but there is a large (albeit interesting) set of things, per SFI, that haven't worked.

I'm guessing that the answer here is "eventually" but the hardware we currently have is several orders of magnitude simpler -- estimates vary widely, leaving aside we don't know such simple things as how memories are stored, but clearly it is a lot -- than the human brain (or pretty much any brain) that it isn't surprisingly that at present we seem to be nowhere close to this. It may not be a good analogy, but when the quantitative political instability first got going with serious funding in the 1960s, the models worked very poorly. By the mid-2000s, we had models that worked pretty well, and actually if someone had the proverbial time machine and could send an article describing those models back to the 1960s, the data and technology to implement those existed, but about fifty years of experimentation (often very slow because people followed a whole lot of dead-ends) were needed to get there. So it is possible we might be, at least in theory, closer than we know (just as credible natural language translation went from seemingly impossible to routine in a relatively short period of time; same happened earlier with chess and more recently with Go) but in addition to possible hardware limitations, very few people are working on this and, e.g. problems thought to be relevant, such as chess-playing, have proven to be dead-ends (except, of course, for chess-playing. And poker, and Go, and any other game that can be described by a small number of rules)

_Could it be we are focusing too much to on models mimicking physics properties? Shall we rather explore models more similar to biology?_

Kahneman's _Thinking Fast and Slow_ -- and more generally, the decades of work he did with Tversky, Slovik and others, now into the second or third (at least) academic generation, would be my go-to place on that. I was familiar with the early work when I wrote Patterns, Rules, and Learning, but it has all gone way, way further, both conceptually and empirically, since then.

> **_Human beings, possessing associative memories, are extraordinarily skillful at pattern recognition. This task they find not only relatively painless, but, to judge from the popularity of crossword puzzles, Trivial Pursuits and Wheel of Fortune, downright pleasurable. In contrast, humans are resistant to logical deductive reasoning and avoid using it whenever possible._**

_On the subject of NLP… a friend pointed to me that natively English speaking countries (Britain, NZ, Australia…) are all islands. Even the US is more or less an island, only sharing physical borders with Mexico and Canada, another English speaking country. And at some point during the 19th century two cultures, Spanish and Anglo-Saxon, settled on the Rio Grande. Today, the development gap is flagrant. How do you culturally and linguistically explain this development gap? Spain, despite the wealth it did extract from South America - as Portugal did - as never been able to thrive. Is the English language particularly efficient?_

Well, English does have the advantage of being both a very simple language (as I've noted on occasion, the Vikings weren't great at language...) and has an extraordinary vocabulary due to initially merging two languages (Anglo-Saxon and Old Norse), and then the vocabulary of most of a third (French), and then being a complete sponge for every other language it encounters, and thanks to English colonialism, it encountered a lot.

As for Spain, I'd probably go with a combination of the "resource curse" -- Mexican and Peruvian gold and silver were so abundant they distorted the economy -- and then the really bad luck of having Philip II as king for a very long time when England and France (and incongruously, even the Netherlands) were expanding under reasonably competent economic and political leadership. Portugal, like the Netherlands, was astonishing in acquiring an overseas empire in the first place. And once industrialization gets going, the Iberian peninsula doesn't have the easily accessed iron and coal reserves the northern Europe had.

_In conjecto’s first post, I was focusing onto Cambridge Analystica, and more specifically the Machine Learning algos they might have used. What’s your view on theses?_

I'm not familiar with Cambridge Analystica’s algorithms specifically, but in general clustering can be highly effective on high dimensional problems (lots of variables) provided you've got enough data to pick up all of the subsets of the data of interest and their behaviour remains consistent over time.

Two of the five machine learning methods -- random forests (mix of quantitative and qualitative) and nearest neighbour (quantitative; typically using a very early approach called K-Means but there are numerous variants) -- are clustering algorithms and the nearest neighbour method was one of the first successfully applied to practical problem (random forests per se came quite a bit later -- they are very memory-intensive so weren't really practical on earlier hardware, but the method at their core, called ID3, was also developed quite early.) There are also some very effective statistical clustering methods, particularly something called correspondence analysis, which are widely used in Europe but almost never seen in the US.

_Your work did resonate particularly well within defence. I wonder if you ever had been approach by finance/hedge funds to iterate your models… I can quite well imagine running events data models on the archives of the Financial Times or The Times and correlate the outcome with equity markets._

Not really, and that always puzzled me. The best explanation I've had is that we're working on the wrong temporal scale: the 6 to 24 month window relevant to defence and intelligence applications is far, far too long for algorithmic trading, but probably too short for a buy-and-hold investor with, say, a 10-year horizon.

Also virtually all of the conflict forecasting work to date has been done at the level of the nation-state, though this is changing (e.g. [https://www.pcr.uu.se/research/views/](https://www.pcr.uu.se/research/views/ "https://www.pcr.uu.se/research/views/")) Also I think over the past ten or fifteen years, the point at which this stuff became cheap and easy (due combination of open source data and software, and first very powerful low-cost desktop computers (driven, ironically, by the demands of video games...) and now cloud computing) there's been plenty of other low-hanging fruit (ad placement and product recommendation, for example) that it's taken up most of the available funding and talent.

_To conclude, Philip, as this blog is specialised on Python… what are your recommended librairies?_

I’ll reply first with a digression  on a fundamental problem of too many people being taught to use libraries as a substitute for knowing idiomatic programming and data structures…

That said, Python and R are both absolutely amazing because of the proliferation of specialized libraries. For data science, just the standards everyone is using: Pandas, NumPy, SciPy, Scikit-Learn, MatplotLib for complicated plots and plotly.

For NLP in general, spaCy, and for topic modeling, GenSim. "newspaper3k" is phenomenal for downloading basic news sites (Reuters, Xinhua).