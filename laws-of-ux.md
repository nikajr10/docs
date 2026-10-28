# Laws of UX

The 30 Laws of UX from [lawsofux.com](https://lawsofux.com/) by Jon Yablonski, rewritten in plain words as a design reference for people and AI agents. For the original wording and further reading, open each law's page on the site.

---

## How to use this file

1. **Short on time?** Read the [At a glance](#at-a-glance) table and the [Checklist](#checklist-before-you-ship).
2. **Solving a specific problem?** Find it in [Which law helps with what](#which-law-helps-with-what).
3. **Mixing up two laws?** See [Laws that are easy to confuse](#laws-that-are-easy-to-confuse).
4. **Designing or building something?** Read the full entries for the laws that apply.

The laws are grouped by theme rather than alphabetically, so related ideas sit next to each other. Every entry has the same parts:

| Part | What it tells you |
|---|---|
| **Quote** | The law as stated on lawsofux.com |
| **In plain words** | What it means, in one or two sentences |
| **Key takeaways** | The main lessons |
| **Examples** | Real products that show it (where the site gives them) |
| **Do / Avoid** | How to apply it when building |
| **Origin** | Where the idea came from |
| **Related** | Laws that work together with this one |

---

## At a glance

| # | Law | In one line | Theme |
|---|---|---|---|
| 1 | [Law of Proximity](#1-law-of-proximity) | Things that are close together look like they belong together. | Seeing |
| 2 | [Law of Common Region](#2-law-of-common-region) | Things inside the same box look like a group. | Seeing |
| 3 | [Law of Similarity](#3-law-of-similarity) | Things that look alike seem to do the same job. | Seeing |
| 4 | [Law of Uniform Connectedness](#4-law-of-uniform-connectedness) | Things joined by a line or frame look the most related. | Seeing |
| 5 | [Law of Prägnanz](#5-law-of-prägnanz) | People see complex shapes in the simplest way possible. | Seeing |
| 6 | [Aesthetic-Usability Effect](#6-aesthetic-usability-effect) | Good-looking design feels easier to use. | Seeing |
| 7 | [Von Restorff Effect](#7-von-restorff-effect) | The one item that looks different gets remembered. | Seeing |
| 8 | [Selective Attention](#8-selective-attention) | People only notice what seems relevant to their goal. | Seeing |
| 9 | [Cognitive Load](#9-cognitive-load) | Every interface costs mental effort, so spend it wisely. | Memory |
| 10 | [Working Memory](#10-working-memory) | The mind's scratchpad is small and fades fast. | Memory |
| 11 | [Miller's Law](#11-millers-law) | People hold about 7 ± 2 items in mind at once. | Memory |
| 12 | [Chunking](#12-chunking) | Grouped information is easier to take in. | Memory |
| 13 | [Serial Position Effect](#13-serial-position-effect) | People remember the first and last items best. | Memory |
| 14 | [Zeigarnik Effect](#14-zeigarnik-effect) | Unfinished tasks stick in the mind. | Memory |
| 15 | [Hick's Law](#15-hicks-law) | More choices mean slower decisions. | Choices |
| 16 | [Choice Overload](#16-choice-overload) | Too many options overwhelm people. | Choices |
| 17 | [Occam's Razor](#17-occams-razor) | If two designs work equally well, pick the simpler one. | Choices |
| 18 | [Tesler's Law](#18-teslers-law) | Some complexity can't be removed, only moved. | Choices |
| 19 | [Pareto Principle](#19-pareto-principle) | About 80% of results come from 20% of causes. | Choices |
| 20 | [Doherty Threshold](#20-doherty-threshold) | Respond in under 400ms to keep people engaged. | Speed |
| 21 | [Fitts's Law](#21-fittss-law) | Big, close targets are faster to hit. | Speed |
| 22 | [Postel's Law](#22-postels-law) | Accept messy input, return clean output. | Speed |
| 23 | [Parkinson's Law](#23-parkinsons-law) | Tasks expand to fill the time they're given. | Speed |
| 24 | [Flow](#24-flow) | Deep focus happens when challenge matches skill. | Speed |
| 25 | [Jakob's Law](#25-jakobs-law) | Users expect your product to work like the others they know. | Behaviour |
| 26 | [Mental Model](#26-mental-model) | People predict how a system works from what they already know. | Behaviour |
| 27 | [Paradox of the Active User](#27-paradox-of-the-active-user) | Users never read the manual. | Behaviour |
| 28 | [Cognitive Bias](#28-cognitive-bias) | Mental shortcuts quietly bend judgment. | Behaviour |
| 29 | [Goal-Gradient Effect](#29-goal-gradient-effect) | People speed up as they get closer to a goal. | Behaviour |
| 30 | [Peak-End Rule](#30-peak-end-rule) | People judge an experience by its best or worst moment and its end. | Behaviour |

**Themes:** [Seeing and grouping](#a-seeing-and-grouping) · [Memory and mental effort](#b-memory-and-mental-effort) · [Choices and simplicity](#c-choices-and-simplicity) · [Speed and interaction](#d-speed-and-interaction) · [Behaviour, motivation and emotion](#e-behaviour-motivation-and-emotion)

---

## Which law helps with what

| If you are working on… | Look at |
|---|---|
| Page layout, cards, spacing | Proximity, Common Region, Similarity, Uniform Connectedness |
| Navigation menus and tab bars | Hick's Law, Serial Position Effect, Jakob's Law |
| Forms and checkout | Chunking, Postel's Law, Tesler's Law, Parkinson's Law, Goal-Gradient Effect |
| Pricing pages and product lists | Choice Overload, Von Restorff Effect, Hick's Law |
| Buttons and touch targets | Fitts's Law, Von Restorff Effect, Similarity |
| Loading, waiting and performance | Doherty Threshold, Peak-End Rule |
| Onboarding | Paradox of the Active User, Goal-Gradient Effect, Zeigarnik Effect, Hick's Law |
| Dashboards and dense data | Cognitive Load, Chunking, Working Memory, Selective Attention |
| Success, error and empty states | Peak-End Rule, Paradox of the Active User, Selective Attention |
| Redesigns | Jakob's Law, Mental Model, Aesthetic-Usability Effect |
| Icons, logos and illustrations | Law of Prägnanz, Occam's Razor |
| Editors and power-user tools | Flow, Doherty Threshold, Fitts's Law |
| Deciding what to build first | Pareto Principle, Occam's Razor |
| Persuasion, defaults and nudges | Cognitive Bias (help users, never trick them) |

---

## Laws that are easy to confuse

| These laws… | …differ like this |
|---|---|
| **Hick's Law** vs **Choice Overload** | Hick's Law is about *speed*: more options make decisions slower. Choice Overload is about *feeling*: too many options make people freeze, give up, or regret their pick. |
| **Miller's Law** vs **Working Memory** vs **Cognitive Load** | Miller's Law gives a rough *number* (7 ± 2 items). Working Memory is the *system* that holds those items for a short time. Cognitive Load is the *total effort* an interface asks for. |
| **Proximity** vs **Common Region** vs **Uniform Connectedness** | All three group things. Proximity uses *distance*, Common Region uses a *shared box or background*, and Uniform Connectedness uses a *visible link* like a line or arrow. Connectedness is the strongest of the three. |
| **Similarity** vs **Von Restorff Effect** | Two sides of one coin. Things that look alike are seen as one group (Similarity). The one thing that looks different stands out and is remembered (Von Restorff). |
| **Goal-Gradient Effect** vs **Zeigarnik Effect** | Goal-Gradient: people *speed up* as they near the finish. Zeigarnik: an *unfinished* task nags at people and pulls them back. Progress indicators use both. |
| **Jakob's Law** vs **Mental Model** | A mental model is the user's internal idea of how a system works. Jakob's Law is the practical result: people build those models on other sites, so match them. |
| **Occam's Razor** vs **Tesler's Law** | Occam's Razor says *remove* complexity you don't need. Tesler's Law says some complexity *can't* be removed, so the system should carry it instead of the user. |
| **Selective Attention** vs **Von Restorff Effect** | Selective Attention explains why people *ignore* most things. Von Restorff explains how to make the one important thing *noticed*. |

---

## A. Seeing and grouping

How people visually read a screen: what looks related, what stands out, and what gets ignored. Laws 1–4 are Gestalt principles of grouping.

---

### 1. Law of Proximity

> Objects that are near, or proximate to each other, tend to be grouped together.

**In plain words:** Distance alone tells people what belongs together. Whitespace is a grouping tool, not empty space.

**Key takeaways**

- Being close together creates a relationship between objects.
- Elements that sit near each other are assumed to share a function or trait.
- Proximity helps users organize and understand information faster.

**Example**

- **Google search results.** The spacing between results makes the page easy to scan, and each result reads as its own cluster of related information.

| ✅ Do | ❌ Avoid |
|---|---|
| Keep each label closer to its own input than to the next field | Even spacing everywhere, so nothing reads as a group |
| Put more space *between* groups than *within* them | A button placed far away from the content it acts on |
| Use consistent spacing tokens so grouping stays predictable | Random, one-off margins |

**Origin.** One of the Gestalt principles of grouping. Gestalt psychologists proposed these to explain why people naturally see organized patterns instead of scattered parts. They argued that the mind has a built-in tendency to find patterns following certain rules: proximity, similarity, continuity, closure and connectedness.

**Related:** [Common Region](#2-law-of-common-region) · [Uniform Connectedness](#4-law-of-uniform-connectedness) · [Chunking](#12-chunking)

---

### 2. Law of Common Region

> Elements tend to be perceived into groups if they are sharing an area with a clearly defined boundary.

**In plain words:** Put things inside the same box and people assume they belong together.

**Key takeaways**

- Common region creates a clear structure and helps users quickly see how elements and sections relate.
- A border around an element or group is an easy way to create a common region.
- A shared background behind a group works too.

| ✅ Do | ❌ Avoid |
|---|---|
| Use cards, panels and tinted sections to group related content | Putting unrelated items in the same card |
| Box related form fields together (e.g. a "Shipping address" block) | Boxes inside boxes inside boxes |
| Separate settings categories into distinct containers | One long, undivided settings page |

**Origin.** One of the Gestalt principles of grouping (see [Law of Proximity](#1-law-of-proximity)).

**Related:** [Proximity](#1-law-of-proximity) · [Uniform Connectedness](#4-law-of-uniform-connectedness) · [Chunking](#12-chunking)

---

### 3. Law of Similarity

> The human eye tends to perceive similar elements as a complete picture, shape, or group, even if those elements are separated.

**In plain words:** Things that look alike are read as belonging together and doing the same job, even when they're far apart on the screen.

**Key takeaways**

- Visually similar elements are seen as related.
- Color, shape, size, orientation and motion can all signal that elements share a group, meaning or function.
- Make links and navigation look clearly different from normal text.

| ✅ Do | ❌ Avoid |
|---|---|
| Give the same style to everything that behaves the same (all links one style, all primary buttons one style) | Styling non-clickable text like a link |
| Make different functions look different | Two different actions that look identical |
| Keep a consistent design system so similarity stays meaningful | Five slightly different button styles |

**Origin.** One of the Gestalt principles of grouping (see [Law of Proximity](#1-law-of-proximity)).

**Related:** [Von Restorff Effect](#7-von-restorff-effect) · [Jakob's Law](#25-jakobs-law)

---

### 4. Law of Uniform Connectedness

> Elements that are visually connected are perceived as more related than elements with no connection.

**In plain words:** A visible connection, such as a line, an arrow, a shared frame or a shared color, binds elements together more strongly than closeness or likeness alone.

**Key takeaways**

- Visually connect similar functions with colors, lines, frames or other shapes.
- Or use a physical connector, such as a line or arrow, from one element to the next.
- Use connectedness to show context or to stress how items relate.

**Example**

- **Google search results.** Borders around special items like videos and featured snippets connect that content visually, set it apart from other results, and give it more priority.

| ✅ Do | ❌ Avoid |
|---|---|
| Use steppers and timelines with connecting lines | Steps floating with nothing showing their order |
| Visually join tabs to their content panel, and tooltips to their trigger | A tooltip that looks detached from what it explains |
| Use breadcrumb separators and arrows in flow diagrams | Decorative lines that connect unrelated things |

**Origin.** One of the Gestalt principles of grouping (see [Law of Proximity](#1-law-of-proximity)).

**Related:** [Proximity](#1-law-of-proximity) · [Common Region](#2-law-of-common-region)

---

### 5. Law of Prägnanz

> People will perceive and interpret ambiguous or complex images as the simplest form possible, because it is the interpretation that requires the least cognitive effort of us.

**In plain words:** The brain prefers the simplest explanation of what it sees, and turns complex shapes into simple, orderly ones.

**Key takeaways**

- The eye looks for simplicity and order in complex shapes so we don't get overwhelmed.
- People process and remember simple figures better than complex ones.
- The eye simplifies complex shapes by merging them into a single, unified shape.

| ✅ Do | ❌ Avoid |
|---|---|
| Keep icons, logos and illustrations simple and easy to recognize | Detailed icons that blur at small sizes |
| Use simple geometric layouts | Visual noise and unnecessary detail |

**Origin.** In 1910, psychologist Max Wertheimer watched lights flashing at a railroad crossing. Like the bulbs around a theater marquee, they looked like one moving light, though they were really separate bulbs switching on and off. That observation led to the Gestalt principles of visual perception, which sit at the heart of almost all graphic design.

**Related:** [Occam's Razor](#17-occams-razor) · [Cognitive Load](#9-cognitive-load)

---

### 6. Aesthetic-Usability Effect

> Users often perceive aesthetically pleasing design as design that's more usable.

**In plain words:** Looks shape how people judge function. A clean, attractive design creates a good first feeling, and that feeling makes people believe the product works better than it may actually work.

**Key takeaways**

- Good-looking design triggers a positive emotional response, which makes people believe it works better.
- People forgive small usability problems more easily when the product looks good.
- The flip side: polish can hide real usability problems, so they slip through testing unnoticed.

| ✅ Do | ❌ Avoid |
|---|---|
| Invest in polish: consistent spacing, good type, a calm palette | Treating visual design as "just decoration" |
| In testing, watch what users *do*, not just what they *say* | Trusting "it looks great" as proof that it works |

**Origin.** First studied in human–computer interaction in 1995. Masaaki Kurosu and Kaori Kashimura of the Hitachi Design Center showed 252 participants 26 versions of an ATM interface and asked them to rate each for beauty and ease of use. How beautiful people found a design predicted how easy they *thought* it was more strongly than how easy it actually was.

**Related:** [Peak-End Rule](#30-peak-end-rule) · [Cognitive Bias](#28-cognitive-bias)

---

### 7. Von Restorff Effect

> Also known as the Isolation Effect: when multiple similar objects are present, the one that differs from the rest is most likely to be remembered.

**In plain words:** The odd one out stands out and is remembered. That makes it a powerful tool for emphasis, but only when used sparingly.

**Key takeaways**

- Make important information and key actions visually distinct.
- Use restraint: too many emphasized elements compete with each other, and loud elements can be mistaken for ads.
- Don't rely only on color to show contrast, or you exclude people with color-vision deficiency or low vision.
- Be careful with motion as a way to stand out, since some users are motion-sensitive.

| ✅ Do | ❌ Avoid |
|---|---|
| Give one primary CTA per view a distinct style | Highlighting everything, so nothing stands out |
| Highlight the recommended pricing plan | Showing emphasis with color alone |
| Combine color with shape, size, icons or labels | Flashing or moving elements, and ignoring `prefers-reduced-motion` |

**Origin.** Named after German psychiatrist and pediatrician Hedwig von Restorff (1906–1962). In her 1933 study, people shown a list of similar items with one distinct item remembered the distinct item better.

**Related:** [Similarity](#3-law-of-similarity) · [Selective Attention](#8-selective-attention)

---

### 8. Selective Attention

> The process of focusing our attention only to a subset of stimuli in an environment — usually those related to our goals.

**In plain words:** People filter out most of the screen and notice only what seems relevant to their goal. Anything that looks like noise gets ignored.

**Key takeaways**

- People filter out irrelevant information to stay focused on their task. Designers have to guide attention, prevent overload and distraction, and help people find what matters.
- **Banner blindness:** users ignore anything that looks like an ad, sits near ads, or appears where ads usually go.
- **Change blindness:** big changes in an interface can go unnoticed when attention is limited and cues are weak.

| ✅ Do | ❌ Avoid |
|---|---|
| Put key content and actions where users are already looking | Styling real content like an ad, or placing it in ad areas |
| Give clear, strong cues when something changes (an error, a new item, updated state) | Several changes on screen at the same time, competing for attention |

**Origin.** The theory took shape in the mid-20th century:

| Year | Researcher | Contribution |
|---|---|---|
| 1950 | Mackworth | Vigilance research, motivated by WWII radar operators |
| 1953 | E. Colin Cherry | *Cocktail party effect*: focusing on one voice while ignoring others |
| 1958 | Donald Broadbent | *Filter theory*: an attention "bottleneck" filters by physical features before meaning |
| 1960 | Anne Treisman | *Attenuation model*: unattended information is turned down, not fully blocked |
| 1963 | Deutsch & Deutsch | *Late selection*: all input is processed for meaning before selection |
| 1973 | Daniel Kahneman | *Capacity model*: attention is a limited resource shared between tasks |

**Related:** [Von Restorff Effect](#7-von-restorff-effect) · [Cognitive Load](#9-cognitive-load)

---

## B. Memory and mental effort

How much people can hold in mind, what they remember, and how to keep the mental work low.

---

### 9. Cognitive Load

> The amount of mental resources needed to understand and interact with an interface.

**In plain words:** Everyone has limited mental capacity at any moment. When an interface asks for more than that, tasks feel harder, details get missed, and people feel overwhelmed.

**Key takeaways**

- When incoming information exceeds the mental space available, tasks get harder, details are missed, and people feel overwhelmed.
- There are two kinds of load:

| Type | What it is | Can you remove it? |
|---|---|---|
| **Intrinsic load** | Effort that belongs to the task itself: holding onto goal-relevant information, taking in new information, tracking progress | No, but you can support it |
| **Extraneous load** | Wasted effort on things that don't help, such as distracting or unnecessary design elements | **Yes, and you should** |

| ✅ Do | ❌ Avoid |
|---|---|
| Cut decoration that carries no meaning | Showing every option on every screen |
| Use progressive disclosure: advanced options behind "More" | Inventing new patterns users have to learn |
| Show only what the current step needs | Decorative elements competing with content |

**Origin.** John Sweller developed cognitive load theory in the late 1980s, building on George Miller's information-processing work. His 1988 paper, *"Cognitive Load Theory, Learning Difficulty, and Instructional Design,"* argued that good design can lower the load on learners.

**Related:** [Working Memory](#10-working-memory) · [Miller's Law](#11-millers-law) · [Hick's Law](#15-hicks-law)

---

### 10. Working Memory

> A cognitive system that temporarily holds and manipulates information needed to complete tasks.

**In plain words:** Working memory is the mind's scratchpad. It's small and fades fast, so interfaces should rely on what people *recognize*, not what they must *recall*.

**Key takeaways**

- Working memory holds about **4–7 chunks** at a time, and each fades after roughly **20–30 seconds**. Show only what's necessary and relevant.
- Brains are good at recognizing things seen before, but bad at holding new information ready to use. Support **recognition over recall**, for example with visited-link styles and breadcrumbs.
- Put the memory burden on the system, not the user. Carry important information from screen to screen when needed, for example in comparison tables.

| ✅ Do | ❌ Avoid |
|---|---|
| Keep earlier choices visible (order summaries, selected filters) | Asking users to remember a value from one screen to type on another |
| Show breadcrumbs and visited-link styles | Hiding context once the user moves to the next step |
| Offer comparison views | Making users flip between tabs to compare |

**Origin.** George A. Miller, Eugene Galanter and Karl H. Pribram coined the term in the 1960s. In 1968, Atkinson and Shiffrin used it for their "short-term store". Today "working memory" usually replaces or includes "short-term memory", with more emphasis on *manipulating* information, not just holding it.

**Related:** [Cognitive Load](#9-cognitive-load) · [Miller's Law](#11-millers-law)

---

### 11. Miller's Law

> The average person can only keep 7 (plus or minus 2) items in their working memory.

**In plain words:** Short-term memory is small. Ask people to juggle too many things at once and they'll drop some.

**Key takeaways**

- Don't use the "magical number seven" to justify arbitrary limits, like "menus must have 7 items".
- Organize content into smaller chunks so it's easier to process, understand and remember.
- Memory capacity varies from person to person, depending on prior knowledge and context.

| ✅ Do | ❌ Avoid |
|---|---|
| Chunk information instead of counting items | Treating "7 items" as a hard design rule |
| Show information where it's needed | Making users memorize codes or values between screens |

**Origin.** In 1956, George Miller argued that immediate memory span and absolute judgment are both limited to around seven pieces of information. Past that "channel capacity", confusion leads to wrong judgments.

**Related:** [Chunking](#12-chunking) · [Working Memory](#10-working-memory)

---

### 12. Chunking

> A process by which individual pieces of an information set are broken down and then grouped together in a meaningful whole.

**In plain words:** Raw information is hard to take in. Split it into small, meaningful groups and people can scan it, find what matters, and act faster.

**Key takeaways**

- Chunked content is easy to scan. Users quickly spot what matches their goal and process it faster.
- Visually distinct groups with a clear hierarchy match how people actually read digital content.
- Modules separated by rules, with a clear hierarchy, help users see how the pieces relate.

| ✅ Do | ❌ Avoid |
|---|---|
| Format long numbers in groups: `+44 20 7946 0958`, not `+442079460958` | Walls of text with no headings |
| Split long forms into steps or labelled sections | One huge form on a single screen |
| Write with headings, short paragraphs and lists | Dashboards where unrelated widgets are mixed together |

**Origin.** The term comes from George A. Miller's 1956 paper, *"The Magical Number Seven, Plus or Minus Two."* Miller noticed that people could hold more in short-term memory when they grouped items into chunks.

**Related:** [Miller's Law](#11-millers-law) · [Proximity](#1-law-of-proximity) · [Common Region](#2-law-of-common-region)

---

### 13. Serial Position Effect

> Users have a propensity to best remember the first and last items in a series.

**In plain words:** In any list, the start and the end stick in memory. The middle fades.

**Key takeaways**

- Put the least important items in the middle of lists, since people remember them least.
- Put key actions at the far left and far right of elements like navigation.

| ✅ Do | ❌ Avoid |
|---|---|
| Put the most important nav and tab-bar items first and last | Burying the main action in the middle of a menu |
| Open and close lists, onboarding and feature summaries with the strongest points | Ending a list with filler |

**Origin.** Hermann Ebbinghaus coined the term. It combines the *primacy effect* (first items are remembered well) and the *recency effect* (last items are remembered well).

**Related:** [Peak-End Rule](#30-peak-end-rule) · [Working Memory](#10-working-memory)

---

### 14. Zeigarnik Effect

> People remember uncompleted or interrupted tasks better than completed tasks.

**In plain words:** An unfinished task nags at us. That pull can motivate people to come back and finish what they started.

**Key takeaways**

- Invite people to explore by clearly signaling that there's more content.
- Giving artificial progress toward a goal makes people more likely to finish.
- Show progress clearly to motivate completion.

| ✅ Do | ❌ Avoid |
|---|---|
| Show profile-completion meters ("Your profile is 70% complete") | Losing a user's progress when they leave |
| Offer "continue where you left off" prompts and saved drafts | Layouts where nothing hints that more content exists |
| Use scroll cues and cut-off carousels to hint at more | Guilt-tripping or nagging users about unfinished tasks |

**Origin.** Soviet psychologist Bluma Zeigarnik (1900–1988) discovered the effect in the 1920s. Her memory study found that incomplete tasks were easier to remember than completed ones.

**Related:** [Goal-Gradient Effect](#29-goal-gradient-effect)

---

## C. Choices and simplicity

How the number and complexity of options affect decisions, and where complexity should live.

---

### 15. Hick's Law

> The time it takes to make a decision increases with the number and complexity of choices.

**In plain words:** Every extra option adds thinking time. When speed matters, fewer and simpler choices win.

**Key takeaways**

- Cut down choices wherever response time is critical.
- Break complex tasks into smaller steps to reduce cognitive load.
- Highlight recommended options so users aren't overwhelmed.
- Use progressive onboarding so new users aren't hit with everything at once.
- But don't simplify so far that things become vague or abstract.

**Examples**

| Product | How it applies Hick's Law |
|---|---|
| **Google homepage** | Removes anything that could distract from typing a search |
| **Apple TV remote** | Very few buttons. The complexity moves into the on-screen menus, which reveal options step by step |
| **Slack onboarding** | A bot teaches messaging first. Every feature except the message box is hidden until users get the basics |

| ✅ Do | ❌ Avoid |
|---|---|
| Keep navigation short | Mega-menus with every page listed |
| Put a clear default or recommended choice first | Presenting all options as equally important |
| Hide advanced settings behind progressive disclosure | Simplifying so much that labels become vague |

**Origin.** Named after psychologists William Edmund Hick and Ray Hyman (also called the Hick-Hyman Law). In 1952 they found that the more options people had, the longer they took to react.

**Related:** [Choice Overload](#16-choice-overload) · [Cognitive Load](#9-cognitive-load)

---

### 16. Choice Overload

> The tendency for people to get overwhelmed when they are presented with a large number of options. Often called the *paradox of choice*.

**In plain words:** More options feel like freedom, but past a point they make deciding harder and less satisfying. People freeze, give up, or feel worse about what they pick.

**Key takeaways**

- Too many options hurt people's ability to decide, and can sour how they feel about the whole experience.
- When people really do need to compare, such as pricing tiers, put related options side by side.
- Shape the design around the decision: show the most relevant content first (for example, a featured product), and give search and filters to narrow things down.

| ✅ Do | ❌ Avoid |
|---|---|
| Default to fewer, curated options | Dumping the full catalogue with no guidance |
| Mark one option "recommended" or "most popular" | Pricing tiers that are hard to compare |
| Offer filters on long lists and comparison views for plans | Hiding search on large collections |

**Origin.** Alvin Toffler introduced the term *overchoice* in his 1970 book *Future Shock*.

**Related:** [Hick's Law](#15-hicks-law) · [Von Restorff Effect](#7-von-restorff-effect)

---

### 17. Occam's Razor

> Among competing hypotheses that predict equally well, the one with the fewest assumptions should be selected.

**In plain words:** If two designs work equally well, choose the simpler one.

**Key takeaways**

- The best way to reduce complexity is to never add it.
- Look at every element and remove as many as you can without hurting the overall function.
- A design is done only when nothing else can be removed.

| ✅ Do | ❌ Avoid |
|---|---|
| Ask of every element: "Does this need to be here?" | Adding features "just in case" |
| Prefer one clear path over several clever ones | Several ways to do the same thing |
| Strip fields and decoration that don't serve the goal | Optional fields in critical flows |

**Origin.** Also called the *law of parsimony*. It's credited to William of Ockham (c. 1287–1347), an English Franciscan friar and philosopher.

**Related:** [Tesler's Law](#18-teslers-law) · [Law of Prägnanz](#5-law-of-prägnanz)

---

### 18. Tesler's Law

> Also known as the Law of Conservation of Complexity: for any system there is a certain amount of complexity which cannot be reduced.

**In plain words:** Some complexity can't be removed, only moved. The question is who carries it: the system (designers and developers) or the user.

**Key takeaways**

- Every process has a core of complexity that can't be designed away. Either the system or the user has to carry it.
- Take as much of that burden off users as possible during design and development.
- Don't design for an idealized, perfectly rational user. Real people don't always behave rationally.
- Put guidance in context so it helps new users whatever path they take.

| ✅ Do | ❌ Avoid |
|---|---|
| Let the system do the hard work: smart defaults, autofill, auto-detecting card types and addresses | Making users format input the way the database wants |
| Format input and recover from errors gracefully | Pushing edge cases onto the user |
| Handle edge cases in code | Assuming users will read instructions |

**Origin.** Larry Tesler worked at Xerox PARC in the mid-1980s. He argued that an engineer should spend an extra week cutting complexity rather than make millions of users spend an extra minute each. Bruce Tognazzini added a twist: when apps get simpler, people start attempting more complex tasks.

**Related:** [Occam's Razor](#17-occams-razor) · [Postel's Law](#22-postels-law)

---

### 19. Pareto Principle

> For many events, roughly 80% of the effects come from 20% of the causes.

**In plain words:** Effort and results are rarely balanced. A small share of features, users or issues usually drives most of the outcome.

**Key takeaways**

- Inputs and outputs are often unevenly distributed.
- A large group may contain only a few members that really matter to the outcome.
- Spend most of your effort where it benefits the most users the most.

| ✅ Do | ❌ Avoid |
|---|---|
| Find the few features and flows most users rely on, and make them excellent first | Polishing edge features while the core flow is rough |
| Fix the bugs that hit the most people | Treating every request as equally important |

**Origin.** From economist Vilfredo Pareto, who noticed that 80% of Italy's land was owned by 20% of the population.

**Related:** [Occam's Razor](#17-occams-razor)

---

## D. Speed and interaction

How fast, easy and forgiving it feels to actually use the interface.

---

### 20. Doherty Threshold

> Productivity soars when a computer and its users interact at a pace (<400ms) that ensures that neither has to wait on the other.

**In plain words:** When the system answers in under about 400 milliseconds, the interaction feels instant and people's attention doesn't drift.

**Key takeaways**

- Give system feedback within 400ms to keep attention and productivity up.
- *Perceived* performance matters as much as real performance. Make waiting feel shorter.
- Animation keeps people visually engaged while work happens in the background.
- Progress bars make waits tolerable, even when they aren't perfectly accurate.
- Adding a deliberate delay can make a process feel more valuable and trustworthy, even when the work takes less time.

| Response time | How it feels | What to show |
|---|---|---|
| Under 400ms | Instant | Pressed state, or the result directly |
| Longer | A noticeable wait | Spinner, skeleton screen, or optimistic update |
| Much longer | A long job | Progress bar, ideally with an estimate |

| ✅ Do | ❌ Avoid |
|---|---|
| Acknowledge every click right away (pressed states, optimistic UI) | Blank screens while loading |
| Use skeleton screens and prefetch likely next views | Clicks with no visible response |
| Debounce search-as-you-type so it still feels instant | Long jobs with no progress shown |

**Origin.** In 1982, Walter J. Doherty and Ahrvind J. Thadani published a paper in the *IBM Systems Journal* setting the response-time requirement at 400ms, down from the earlier standard of 2 seconds. Systems faster than this were found to be almost "addicting" to use.

**Related:** [Flow](#24-flow) · [Peak-End Rule](#30-peak-end-rule)

---

### 21. Fitts's Law

> The time to acquire a target is a function of the distance to and size of the target.

**In plain words:** The bigger and closer something is, the faster and more accurately people can hit it. Small, far-away targets are slow and easy to miss.

**Key takeaways**

- Touch targets must be big enough to select accurately.
- Leave enough space between touch targets so people don't hit the wrong one.
- Put targets where they're easy to reach.

| ✅ Do | ❌ Avoid |
|---|---|
| Make primary buttons large, with tap targets of at least 44×44px on mobile | Tiny icon-only buttons |
| Make the whole row or card clickable, not just its text | Links where only the word itself is clickable |
| Keep key mobile actions within thumb reach | Main actions in hard-to-reach corners |
| Space destructive actions away from common ones | "Delete" right next to "Save" |

**Origin.** In 1954, psychologist Paul Fitts showed that the time to reach a target grows with its distance and shrinks with its size. Speed and accuracy trade off: fast movements toward small targets cause more errors.

**Related:** [Von Restorff Effect](#7-von-restorff-effect)

---

### 22. Postel's Law

> Be liberal in what you accept, and conservative in what you send.

**In plain words:** Accept whatever users give you, in whatever messy form, and return clean, consistent, predictable output.

**Key takeaways**

- Be empathetic, flexible and tolerant toward whatever actions or input users give.
- Expect almost any input, access method or ability, and still provide a reliable, accessible interface.
- The more you anticipate in design, the more resilient it will be.
- Accept varied input, translate it into what you need, set clear boundaries, and give clear feedback.

| Users might type… | Accept it as… |
|---|---|
| `07700 900123`, `07700-900-123`, `07700900123` | The same phone number |
| `  Jane@Example.com ` | `jane@example.com` |
| `12/03/2026`, `12 Mar 2026` | The same date (with clear locale rules) |
| `iphone`, `iPhone`, `iphnoe` | A matching search result |

| ✅ Do | ❌ Avoid |
|---|---|
| Normalize input on the backend | Rejecting input because of spaces or dashes |
| Make search case-insensitive and typo-tolerant | Vague errors like "Invalid input" |
| Support all devices, input methods and assistive tech | Mouse-only or desktop-only interactions |

**Origin.** Also called the *Robustness Principle*. Internet pioneer Jon Postel formulated it as a guideline for TCP: senders should follow the spec exactly, and receivers should accept slightly non-standard input as long as the meaning is clear.

**Related:** [Tesler's Law](#18-teslers-law)

---

### 23. Parkinson's Law

> Any task will inflate until all of the available time is spent.

**In plain words:** If a task *can* take longer, it will. Good UX shrinks the time a task takes so it finishes faster than people expect.

**Key takeaways**

- Keep task time within what users expect.
- Finishing faster than expected makes the whole experience better.
- Use features like autofill to save time on important form data, so purchases and bookings finish quickly.

| ✅ Do | ❌ Avoid |
|---|---|
| Support browser autofill, saved addresses and saved payment methods | Making users retype details the browser already knows |
| Use one-click actions and sensible defaults | Optional fields in critical flows |
| Show estimated times ("Takes 2 minutes"), then beat them | Open-ended flows with no sense of length |

**Origin.** C. Northcote Parkinson wrote it as the opening line of a humorous essay in *The Economist* in 1955, drawing on years in the British Civil Service.

**Related:** [Tesler's Law](#18-teslers-law) · [Goal-Gradient Effect](#29-goal-gradient-effect)

---

### 24. Flow

> The mental state in which a person performing some activity is fully immersed in a feeling of energized focus, full involvement, and enjoyment in the process of the activity.

**In plain words:** Flow is the "in the zone" feeling: deep focus, a sense of control, and losing track of time. Products can encourage it or break it.

**Key takeaways**

- Flow happens when a task's difficulty matches the person's skill.
- Too hard causes frustration, and too easy causes boredom.
- Give clear feedback so users always know what they've done and achieved.
- Remove needless friction, keep the system responsive, and make features easy to discover.

| Challenge vs skill | Result |
|---|---|
| Too hard | Frustration |
| Too easy | Boredom |
| Matched | **Flow** |

| ✅ Do | ❌ Avoid |
|---|---|
| Keep responses fast and feedback instant | Modals, forced popups and surprise navigation |
| Offer shortcuts for experts and gentle guidance for beginners | Interrupting long tasks |

**Origin.** Psychologist Mihály Csíkszentmihályi coined the term in 1975.

**Related:** [Doherty Threshold](#20-doherty-threshold) · [Cognitive Load](#9-cognitive-load)

---

## E. Behaviour, motivation and emotion

What people expect, how they really behave, and what keeps them going and makes them happy.

---

### 25. Jakob's Law

> Users spend most of their time on other sites. This means that users prefer your site to work the same way as all the other sites they already know.

**In plain words:** People arrive with habits learned elsewhere. Match those habits and they can focus on their task instead of learning your interface.

**Key takeaways**

- Users carry expectations from familiar products over to anything that looks similar.
- Building on existing mental models lets users focus on their task.
- When you make big changes, ease the shock by letting users keep the familiar version for a while.

**Examples**

| Example | How it applies Jakob's Law |
|---|---|
| **Form controls** | Toggles, radio buttons and buttons copy their physical counterparts, so people already know how to use them |
| **YouTube redesign (2017)** | Desktop users could preview the new design, give feedback, and switch back, moving over when they were ready |

| ✅ Do | ❌ Avoid |
|---|---|
| Follow conventions: logo top-left linking home, search at the top, cart top-right | Reinventing basic patterns like links, forms or navigation |
| Use standard form controls and familiar icons with their usual meanings | Familiar icons with a new meaning |
| Innovate on the value you offer, not on basic interaction | Forcing a big redesign on everyone overnight |

**Origin.** Coined by Jakob Nielsen, co-founder of the Nielsen Norman Group with Don Norman. Nielsen started the "discount usability engineering" movement and invented methods such as heuristic evaluation.

**Related:** [Mental Model](#26-mental-model) · [Similarity](#3-law-of-similarity)

---

### 26. Mental Model

> A compressed model based on what we think we know about a system and how it works.

**In plain words:** Everyone carries a simplified idea of how a system works and uses it to predict what happens next. When the product matches that idea it feels intuitive. When it doesn't, it feels broken.

**Key takeaways**

- We build a working model of how a system behaves and apply it to similar new systems.
- Matching users' mental models lets them carry knowledge over from other products.
- E-commerce sites all use product cards, carts and checkout flows because users expect them.
- The hard part is closing the gap between *our* mental model and the *user's*. That's why we do user research: interviews, personas, journey maps, empathy maps.

| ✅ Do | ❌ Avoid |
|---|---|
| Use metaphors and terms users already know (cart, inbox, folder, trash) | Internal jargon in the UI |
| Make actions behave the way their names and icons suggest | A "Save" button that also publishes |
| Check with real users when unsure | Assuming users think the way the team does |

**Origin.** Psychologist Kenneth Craik proposed the idea in his 1943 book *The Nature of Explanation*: people carry a small-scale model of how the world works and use it to anticipate events.

**Related:** [Jakob's Law](#25-jakobs-law) · [Paradox of the Active User](#27-paradox-of-the-active-user)

---

### 27. Paradox of the Active User

> Users never read manuals but start using the software immediately.

**In plain words:** People want to get their task done *now*. They skip the docs and learn by doing, even though learning the system properly would save them time later.

**Key takeaways**

- Users focus on their immediate task and don't want to read up front.
- It's a paradox because learning the system first would save them time in the long run.
- Put guidance *inside* the product, in context, so it helps whatever path people take (for example, tooltips).

| ✅ Do | ❌ Avoid |
|---|---|
| Make the UI self-explanatory | Relying on a help page to explain basic tasks |
| Use inline hints, helpful empty states, contextual tooltips and good defaults | Long upfront tutorials users must click through |
| Make errors easy to recover from | Dead ends with no way back |

**Origin.** Mary Beth Rosson and John Carroll defined the idea in 1987. They saw that new users skipped the manuals and dove straight in, even when that meant errors and dead ends.

**Related:** [Tesler's Law](#18-teslers-law) · [Mental Model](#26-mental-model)

---

### 28. Cognitive Bias

> A systematic error of thinking or rationality in judgment that influences our perception of the world and our decision-making ability.

**In plain words:** To save mental energy, we rely on rules of thumb instead of reasoning everything from scratch. These shortcuts make us fast, but they bend our judgment in ways we don't notice.

**Key takeaways**

- Mental shortcuts (heuristics) let us decide quickly, but they quietly influence our judgment.
- Knowing about biases won't remove them, but it makes them easier to spot, which guards against bad reasoning, unintended discrimination and costly mistakes.
- A common example is *confirmation bias*: we seek out, interpret and remember information that confirms what we already believe.

| Common bias | What it means | Ethical use in design |
|---|---|---|
| Anchoring | The first number seen shapes later judgments | Show the regular price next to a genuine discount |
| Framing | How something is worded changes the decision | Describe outcomes honestly and clearly |
| Defaults | People tend to keep the preset option | Pre-select the option that's best for the user |
| Social proof | People follow what others do | Show real reviews and real usage numbers |

| ✅ Do | ❌ Avoid |
|---|---|
| Use biases to *help* users decide well | Dark patterns: fake urgency, hidden costs, trick opt-ins |
| Test with real users to catch your own bias as a designer | Assuming you already know what users want |

**Origin.** Amos Tversky and Daniel Kahneman introduced the idea in 1972. Through repeatable experiments, they showed that real human judgment differs from rational choice theory: heuristics give quick estimates but can cause severe, systematic errors.

**Related:** [Peak-End Rule](#30-peak-end-rule) · [Aesthetic-Usability Effect](#6-aesthetic-usability-effect)

---

### 29. Goal-Gradient Effect

> The tendency to approach a goal increases with proximity to the goal.

**In plain words:** The closer people feel to finishing, the harder and faster they push. Seeing progress is itself a motivator.

**Key takeaways**

- The closer users are to finishing a task, the faster they work toward it.
- Giving people some artificial progress up front (a head start) makes them more likely to finish.
- Show progress clearly to keep people motivated.

| ✅ Do | ❌ Avoid |
|---|---|
| Show step indicators in multi-step flows ("Step 2 of 4") | Multi-step flows with no sense of how long is left |
| Start onboarding checklists with items already ticked ("Account created ✓") | Progress bars that jump backwards |
| Tell users how close they are ("1 more step to finish") | Hiding how many steps remain |

**Origin.** Behaviorist Clark Hull proposed the goal-gradient hypothesis in 1932. In a 1934 experiment, he found that rats in a straight alley ran faster as they neared the food. Later research applied the idea to people, especially in reward and loyalty programs.

**Related:** [Zeigarnik Effect](#14-zeigarnik-effect) · [Parkinson's Law](#23-parkinsons-law)

---

### 30. Peak-End Rule

> People judge an experience largely based on how they felt at its peak and at its end, rather than the total sum or average of every moment of the experience.

**In plain words:** Memory doesn't average. People remember the most intense moment and the final moment, and judge the whole experience by those two.

**Key takeaways**

- Pay close attention to the most intense points and the final moments of the journey.
- Find where your product is most helpful, valuable or fun, and design those moments to delight.
- People remember negative experiences more vividly than positive ones.

**Examples**

| Product | How it applies the Peak-End Rule |
|---|---|
| **Mailchimp** | Sending a campaign is stressful, so Mailchimp eases the moment with illustration, subtle animation and humor instead of a plain confirmation |
| **Uber** | Waiting is a negative peak. By focusing on how people perceive waiting time, Uber lowered cancellations after a ride request |

| ✅ Do | ❌ Avoid |
|---|---|
| Make success and confirmation screens feel rewarding | Plain, forgettable "Done" screens |
| Handle errors, waits and failures with care | Harsh or blaming error messages |
| End flows with a clear next step, a thank-you or a small celebration | Ending a flow with a dead end or an upsell wall |

**Origin.** The 1993 study *"When More Pain Is Preferred to Less: Adding a Better End"* by Kahneman, Fredrickson, Schreiber and Redelmeier. Participants held one hand in 14°C water for 60 seconds, and the other for 60 seconds plus 30 more as it warmed slightly to 15°C. Most chose to repeat the *longer* trial, because it ended less badly.

**Related:** [Serial Position Effect](#13-serial-position-effect) · [Cognitive Bias](#28-cognitive-bias) · [Doherty Threshold](#20-doherty-threshold)

---

## Checklist before you ship

Run through this before you ship any screen or flow.

| Area | Question | Laws |
|---|---|---|
| Grouping | Are related things close, boxed, alike or connected, and unrelated things apart? | Proximity, Common Region, Similarity, Uniform Connectedness |
| Simplicity | Can anything else be removed? Are shapes and icons simple? | Occam's Razor, Prägnanz |
| Looks and trust | Is it polished, and did we test real behaviour, not just impressions? | Aesthetic-Usability |
| Emphasis | Does exactly one key action stand out, without relying on color alone? | Von Restorff, Selective Attention |
| Memory | Is content chunked? Does the system remember things so the user doesn't have to? | Miller's Law, Chunking, Working Memory, Cognitive Load |
| Order | Are the most important items first and last? | Serial Position Effect |
| Choices | Are options few, with a clear recommended default? | Hick's Law, Choice Overload |
| Complexity | Does the system handle the hard parts instead of the user? | Tesler's Law |
| Priority | Did we polish the 20% of features that matter most? | Pareto Principle |
| Speed | Is there feedback within 400ms, plus loaders and progress for anything slower? | Doherty Threshold |
| Targets | Are buttons big, well spaced and within easy reach? | Fitts's Law |
| Input | Does it accept messy input and return clean output? | Postel's Law |
| Effort | Does the task finish faster than users expect? | Parkinson's Law |
| Focus | Does it support deep focus without needless interruptions? | Flow |
| Familiarity | Does it follow common conventions and users' mental models? | Jakob's Law, Mental Model |
| Learning | Can someone use it without reading docs? | Paradox of the Active User |
| Motivation | Is progress visible, ideally with a head start? | Goal-Gradient, Zeigarnik |
| Moments | Are the peak and the ending good, and are errors handled gracefully? | Peak-End Rule |
| Ethics | Are we using psychology to help users, not manipulate them? | Cognitive Bias |
