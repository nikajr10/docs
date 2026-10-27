# Laws of UX

This file collects the 30 Laws of UX from [lawsofux.com](https://lawsofux.com/) by Jon Yablonski. The guidance is rewritten here in plain words so an agent can use it as a design reference. For the original wording and further reading, open each law's own page on the site.

**How to use this file:** before you design or build any screen, flow, component or piece of copy, skim the laws that apply. Each law has the same parts:

- the core idea
- what it means in practice
- key takeaways
- real-world examples (where the site gives them)
- where the idea came from
- how to apply it when building

The checklist at the end is a quick final review.

---

## Contents

1. [Aesthetic-Usability Effect](#1-aesthetic-usability-effect)
2. [Choice Overload](#2-choice-overload)
3. [Chunking](#3-chunking)
4. [Cognitive Bias](#4-cognitive-bias)
5. [Cognitive Load](#5-cognitive-load)
6. [Doherty Threshold](#6-doherty-threshold)
7. [Fitts's Law](#7-fittss-law)
8. [Flow](#8-flow)
9. [Goal-Gradient Effect](#9-goal-gradient-effect)
10. [Hick's Law](#10-hicks-law)
11. [Jakob's Law](#11-jakobs-law)
12. [Law of Common Region](#12-law-of-common-region)
13. [Law of Proximity](#13-law-of-proximity)
14. [Law of Prägnanz](#14-law-of-prägnanz)
15. [Law of Similarity](#15-law-of-similarity)
16. [Law of Uniform Connectedness](#16-law-of-uniform-connectedness)
17. [Mental Model](#17-mental-model)
18. [Miller's Law](#18-millers-law)
19. [Occam's Razor](#19-occams-razor)
20. [Paradox of the Active User](#20-paradox-of-the-active-user)
21. [Pareto Principle](#21-pareto-principle)
22. [Parkinson's Law](#22-parkinsons-law)
23. [Peak-End Rule](#23-peak-end-rule)
24. [Postel's Law](#24-postels-law)
25. [Selective Attention](#25-selective-attention)
26. [Serial Position Effect](#26-serial-position-effect)
27. [Tesler's Law](#27-teslers-law)
28. [Von Restorff Effect](#28-von-restorff-effect)
29. [Working Memory](#29-working-memory)
30. [Zeigarnik Effect](#30-zeigarnik-effect)

---

## 1. Aesthetic-Usability Effect

> Users often perceive aesthetically pleasing design as design that's more usable.

People don't judge an interface only by how well it works. Looks shape that judgment too. A clean, attractive design gives people a good first feeling, and that feeling makes them believe the product works better than it may actually work.

**Key takeaways**

- Good-looking design triggers a positive emotional response, which makes people believe it works better.
- People forgive small usability problems more easily when the product looks good.
- The flip side: polish can hide real usability problems, so they slip through usability testing unnoticed.

**Origin.** The effect was first studied in human–computer interaction in 1995. Masaaki Kurosu and Kaori Kashimura of the Hitachi Design Center showed 252 participants 26 versions of an ATM interface and asked them to rate each one for beauty and for ease of use. How beautiful people found a design predicted how easy they *thought* it was more strongly than it predicted how easy it actually was. In other words, looks color how people judge function.

**Apply it when building.** Invest in visual polish: consistent spacing, good type, a calm palette. It earns trust and patience. But during testing, watch what users *do*, not just what they *say*, because a pretty UI can hide broken flows.

---

## 2. Choice Overload

> The tendency for people to get overwhelmed when they are presented with a large number of options. Often called the *paradox of choice*.

More options feel like freedom, but past a certain point they make deciding harder and less satisfying. Users may freeze, give up, or feel worse about whatever they finally pick. This idea is closely related to Hick's Law.

**Key takeaways**

- Too many options hurt people's ability to decide, and they can sour how people feel about the whole experience.
- When people really do need to compare, such as pricing tiers, put the related options side by side.
- Shape the design around the decision. Show the most relevant content first (for example, a featured product), and give people search and filters to narrow things down early.

**Origin.** The term *overchoice* was introduced by Alvin Toffler in his 1970 book *Future Shock*. It describes the paradox that a large variety of options can make decisions worse, not better.

**Apply it when building.** Default to fewer, curated options. Add a "recommended" or "most popular" marker, give filters on long lists, and offer comparison views for plans or products.

---

## 3. Chunking

> A process by which individual pieces of an information set are broken down and then grouped together in a meaningful whole.

Raw information is hard to take in. When you split it into small, meaningful groups, people can scan it, find what matters for their goal, and act faster. Chunking is closely related to Miller's Law.

**Key takeaways**

- Chunked content is easy to scan. Users quickly spot what matches their goal and process it faster.
- Visually distinct groups with a clear hierarchy match how people actually read and evaluate digital content.
- Grouping content into modules, with rules separating them and a clear hierarchy, helps users see how the pieces relate.

**Origin.** The word comes from George A. Miller's famous 1956 paper, *"The Magical Number Seven, Plus or Minus Two."* Miller noticed that short-term memory didn't behave like a fixed-capacity information channel. People could hold more when they grouped items into chunks.

**Apply it when building.** Format long numbers (phone, card, IBAN) in groups. Split long forms into steps or labelled sections. Write content with headings, short paragraphs and lists. Group dashboard widgets by topic.

---

## 4. Cognitive Bias

> A systematic error of thinking or rationality in judgment that influences our perception of the world and our decision-making ability.

To save mental energy, we don't reason through every situation from scratch. We rely on rules of thumb built from past experience. These shortcuts make us fast, but they also bend our judgment in ways we don't notice.

**Key takeaways**

- Mental shortcuts (heuristics) let us decide quickly without full analysis, but they quietly influence our judgment.
- Knowing about our own biases won't remove them. It does make them easier to spot in ourselves and others, which guards against bad reasoning, unintended discrimination and costly mistakes.
- A common example is *confirmation bias*: we seek out, interpret and remember information in ways that confirm what we already believe. That's why polarizing topics are so hard to discuss logically.

**Origin.** Amos Tversky and Daniel Kahneman introduced the idea in 1972. They noticed that people couldn't reason intuitively about large orders of magnitude. Through a series of repeatable experiments, they showed that real human judgment differs from rational choice theory. Heuristics give quick estimates, but they can cause severe, systematic errors.

**Apply it when building.** Know the common biases (anchoring, framing, defaults, social proof) and use them to *help* users decide well, never to trick them. No dark patterns. Also watch for your own bias as a designer: test with real users instead of assuming.

---

## 5. Cognitive Load

> The amount of mental resources needed to understand and interact with an interface.

Everyone has a limited amount of mental capacity at any moment. When an interface asks for more than that, tasks feel harder, details get missed, and people feel overwhelmed. Cognitive load is closely related to Miller's Law.

**Key takeaways**

- When incoming information exceeds the mental space available, people struggle: tasks get harder, details are missed, and they feel overwhelmed.
- **Intrinsic load** is the effort that belongs to the task itself: holding onto information relevant to the goal, taking in new information, and keeping track of progress.
- **Extraneous load** is wasted effort spent on things that don't help the user understand, such as distracting or unnecessary design elements. This is the part designers can and should remove.

**Origin.** John Sweller developed cognitive load theory in the late 1980s from studies of problem solving, building on George Miller's information-processing work. His 1988 paper, *"Cognitive Load Theory, Learning Difficulty, and Instructional Design,"* argued that good design can lower the load on learners. Researchers later found ways to measure perceived mental effort as an indicator of load.

**Apply it when building.** Cut decoration that carries no meaning. Use progressive disclosure, so advanced options sit behind "More". Show only what the current step needs, and use familiar patterns so users don't have to learn new ones.

---

## 6. Doherty Threshold

> Productivity soars when a computer and its users interact at a pace (<400ms) that ensures that neither has to wait on the other.

When the system answers fast enough, people stay in a smooth back-and-forth with it and their attention doesn't drift. Under about 400 milliseconds, the interaction feels instant and engaging.

**Key takeaways**

- Give system feedback within 400ms to keep people's attention and productivity up.
- *Perceived* performance matters as much as real performance. Make waiting feel shorter.
- Animation can keep people visually engaged while work happens in the background.
- Progress bars make waits tolerable, even when they aren't perfectly accurate.
- Surprisingly, adding a deliberate delay can make a process feel more valuable and trustworthy, even when the work itself takes much less time.

**Origin.** In 1982, Walter J. Doherty and Ahrvind J. Thadani published a paper in the *IBM Systems Journal* setting the computer response-time requirement at 400ms, down from the earlier standard of 2 seconds. Systems that responded faster than this threshold were found to be almost "addicting" to use.

**Apply it when building.** Acknowledge every click right away: pressed states, spinners, optimistic UI updates. Use skeleton screens instead of blank pages. Prefetch likely next views, show progress for longer jobs, and debounce search-as-you-type so it still feels instant.

---

## 7. Fitts's Law

> The time to acquire a target is a function of the distance to and size of the target.

The bigger and closer something is, the faster and more accurately people can hit it. Small, far-away targets are slow to reach and easy to miss, especially when people move fast.

**Key takeaways**

- Touch targets must be big enough to select accurately.
- Leave enough space between touch targets so people don't hit the wrong one.
- Put targets where they're easy to reach in the interface.

**Origin.** In 1954, psychologist Paul Fitts studied the human motor system. He showed that the time to reach a target grows with its distance and shrinks with its size. Speed and accuracy trade off: fast movements toward small targets cause more errors. This is why interactive buttons are large, especially on touch devices, and why a button should sit close to where the user's attention already is.

**Apply it when building.** Make primary buttons large, with tap targets of at least 44×44px on mobile. Make the whole row or card clickable, not just its text. Place actions near the content they affect, and keep key mobile actions within thumb reach. Space destructive actions away from common ones.

---

## 8. Flow

> The mental state in which a person performing some activity is fully immersed in a feeling of energized focus, full involvement, and enjoyment in the process of the activity.

Flow is that "in the zone" feeling: deep focus, a sense of control, and losing track of time. Products can encourage it or break it.

**Key takeaways**

- Flow happens when a task's difficulty matches the person's skill. It feels like intense focus on the present with a sense of total control.
- A task that's too hard causes frustration, and one that's too easy causes boredom. Match the challenge to the user's skill.
- Give clear feedback so users always know what they've done and what they've achieved.
- Remove needless friction, keep the system responsive, and make features easy to discover so people don't disengage.

**Origin.** Psychologist Mihály Csíkszentmihályi coined the term in 1975. It's now used across many fields, notably occupational therapy, though the idea is said to have existed for thousands of years under other names.

**Apply it when building.** In editors, creative tools and long tasks, avoid interruptions like modals, forced popups and surprise navigation. Keep responses fast, give instant feedback, offer shortcuts for experts and gentle guidance for beginners.

---

## 9. Goal-Gradient Effect

> The tendency to approach a goal increases with proximity to the goal.

The closer people feel to finishing, the harder and faster they push toward the finish line. Seeing progress is itself a motivator.

**Key takeaways**

- The closer users are to finishing a task, the faster they work toward it.
- Giving people some artificial progress up front (a head start) makes them more likely to finish.
- Show progress clearly to keep people motivated.

**Origin.** Behaviorist Clark Hull proposed the goal-gradient hypothesis in 1932. In a classic 1934 experiment, he found that rats in a straight alley ran faster and faster as they neared the food. Later research applied the idea to human behavior, especially reward and loyalty programs.

**Apply it when building.** Use progress bars and step indicators ("Step 2 of 4") in multi-step flows. Show onboarding checklists with some items already ticked ("Account created ✓"). Design loyalty cards and streaks that start with progress, and tell users how close they are ("1 more step to finish").

---

## 10. Hick's Law

> The time it takes to make a decision increases with the number and complexity of choices.

Every extra option adds a little more thinking time. When speed matters, fewer and simpler choices win.

**Key takeaways**

- Cut down choices wherever response time is critical.
- Break complex tasks into smaller steps to reduce cognitive load.
- Highlight recommended options so users aren't overwhelmed.
- Use progressive onboarding so new users aren't hit with everything at once.
- But don't simplify so far that things become vague or abstract.

**Examples**

- **Google homepage.** It keeps decisions to a minimum by removing anything that could distract from typing a search.
- **Apple TV remote.** It has very few buttons, so it puts little load on working memory. The complexity moves into the TV interface, where menus organize options and reveal them step by step.
- **Slack's progressive onboarding.** Instead of a full app after a few slides, Slack uses a bot to teach messaging with no consequences. All features except the message input are hidden at first, and more appear once users get the basics.

**Origin.** Named after psychologists William Edmund Hick (British) and Ray Hyman (American), it's also called the Hick-Hyman Law. In 1952 they studied how the number of stimuli affects reaction time. The more options people had, the longer they took to decide. Bombarding users with choices hands them work they don't want.

**Apply it when building.** Keep navigation short. Put a clear default or recommended choice first. Split long forms into steps, and hide advanced settings behind progressive disclosure.

---

## 11. Jakob's Law

> Users spend most of their time on other sites. This means that users prefer your site to work the same way as all the other sites they already know.

People arrive with habits learned elsewhere. When your product matches those habits, they can focus on their task instead of learning your interface.

**Key takeaways**

- Users carry expectations from familiar products over to anything that looks similar.
- Building on existing mental models lets users focus on their task, not on learning a new system.
- When you make big changes, ease the shock by letting users keep the familiar version for a while.

**Examples**

- **Form controls.** Toggles, radio buttons and even buttons copy the design of their physical counterparts, so people already know how to use them.
- **YouTube redesign (2017).** After years of nearly the same design, YouTube let desktop users preview the new Material Design UI, give feedback, and switch back if they wanted. Letting people move when they were ready avoided a clash with their mental models.

**Origin.** Coined by Jakob Nielsen, co-founder of the Nielsen Norman Group with Don Norman. Nielsen started the "discount usability engineering" movement for fast, cheap UI improvements, and he invented methods such as heuristic evaluation.

**Apply it when building.** Follow conventions: logo top-left linking home, search at the top, cart top-right, underlined or colored links, standard form controls, and familiar icons with their usual meanings. Innovate on the value you offer, not on basic interaction patterns. For redesigns, offer an opt-in preview or a way to revert.

---

## 12. Law of Common Region

> Elements tend to be perceived into groups if they are sharing an area with a clearly defined boundary.

Put things inside the same box and people assume they belong together.

**Key takeaways**

- Common region creates a clear structure and helps users quickly understand how elements and sections relate.
- A border around an element or group is an easy way to create a common region.
- A shared background behind a group works too.

**Origin.** It's one of the Gestalt principles of grouping. Gestalt psychologists proposed these to explain why people naturally see organized patterns rather than scattered parts (the overall idea is called *Prägnanz*). They argued that the mind has a built-in tendency to find patterns following certain rules, grouped into proximity, similarity, continuity, closure and connectedness.

**Apply it when building.** Use cards, panels and background-tinted sections to group related content. Box related form fields together (for example, a "Shipping address" block). Separate settings categories into distinct containers.

---

## 13. Law of Proximity

> Objects that are near, or proximate to each other, tend to be grouped together.

Distance alone tells people what belongs together. Whitespace is a grouping tool, not empty space.

**Key takeaways**

- Being close together creates a relationship between objects.
- Elements that sit near each other are assumed to share a function or trait.
- Proximity helps users organize and understand information faster.

**Example**

- **Google search results.** The spacing between results makes the page easy to scan, and it makes each result read as its own cluster of related information.

**Origin.** It's one of the Gestalt principles of grouping (see the Law of Common Region above).

**Apply it when building.** Keep each label closer to its own input than to the next field. Put more space *between* groups than *within* them. Keep a button next to the content it acts on, and use consistent spacing tokens so grouping stays predictable.

---

## 14. Law of Prägnanz

> People will perceive and interpret ambiguous or complex images as the simplest form possible, because it is the interpretation that requires the least cognitive effort of us.

The brain prefers the simplest explanation of what it sees. It turns complex shapes into simple, orderly ones.

**Key takeaways**

- The eye looks for simplicity and order in complex shapes so we don't get overwhelmed.
- Research shows people process and remember simple figures better than complex ones.
- The eye simplifies complex shapes by merging them into a single, unified shape.

**Origin.** In 1910, psychologist Max Wertheimer watched lights flashing at a railroad crossing. Like the bulbs around a theater marquee, they seemed to be one light moving, though really separate bulbs were switching on and off. That observation led to the Gestalt principles of visual perception, which sit at the heart of almost all graphic design.

**Apply it when building.** Keep icons, logos and illustrations simple and easy to recognize. Use simple geometric layouts, and avoid visual noise and unnecessary detail that makes people work to read a shape.

---

## 15. Law of Similarity

> The human eye tends to perceive similar elements as a complete picture, shape, or group, even if those elements are separated.

Things that look alike are read as belonging together and doing the same job, even when they're far apart on the screen.

**Key takeaways**

- Visually similar elements are seen as related.
- Color, shape, size, orientation and motion can all signal that elements share a group, meaning or function.
- Make links and navigation look clearly different from normal text.

**Origin.** It's one of the Gestalt principles of grouping (see the Law of Common Region above).

**Apply it when building.** Give the same style to everything that behaves the same: all links one style, all primary buttons one style. Never style non-clickable text like a link. Make different functions look different, and keep a consistent design system so similarity stays meaningful.

---

## 16. Law of Uniform Connectedness

> Elements that are visually connected are perceived as more related than elements with no connection.

A visible connection, such as a line, an arrow, a shared frame or a shared color, binds elements together more strongly than mere closeness or likeness.

**Key takeaways**

- Visually connect similar functions with colors, lines, frames or other shapes.
- Or use a physical connector, such as a line or arrow, from one element to the next.
- Use connectedness to show context or to stress how similar items relate.

**Example**

- **Google search results.** Borders around special items like videos and featured snippets connect that content visually and set it apart from other results, giving it more priority.

**Origin.** It's one of the Gestalt principles of grouping (see the Law of Common Region above).

**Apply it when building.** Use steppers and timelines with connecting lines. Visually join tabs to their content panel and tooltips to their trigger. Use breadcrumb separators and flow diagrams with arrows.

---

## 17. Mental Model

> A compressed model based on what we think we know about a system and how it works.

Everyone carries a simplified idea of how a system works and uses it to predict what will happen next. When the product matches that idea, it feels intuitive. When it doesn't, it feels broken. This idea is closely related to Jakob's Law.

**Key takeaways**

- We build a working model of how a system behaves and apply it to similar new systems.
- Matching the design to users' mental models lets them carry knowledge over from other products without relearning.
- Good experiences happen when design and mental model line up. E-commerce sites, for example, all use product cards, carts and checkout flows because users expect them.
- One of the hardest parts of design is closing the gap between *our* mental model and the *user's*. That's why we do user research: interviews, personas, journey maps, empathy maps.

**Origin.** Psychologist Kenneth Craik proposed the idea in his 1943 book *The Nature of Explanation*. He said people carry a small-scale model of how the world works and use it to anticipate events, reason and explain things.

**Apply it when building.** Use metaphors and terms users already know (cart, inbox, folder, trash). Make actions behave the way their names and icons suggest. When unsure, check with real users instead of guessing.

---

## 18. Miller's Law

> The average person can only keep 7 (plus or minus 2) items in their working memory.

Short-term memory is small. If you ask people to juggle too many items at once, they'll drop some.

**Key takeaways**

- Don't use the "magical number seven" to justify arbitrary design limits, like "menus must have 7 items".
- Organize content into smaller chunks so it's easier to process, understand and remember.
- Short-term memory capacity varies from person to person, depending on prior knowledge and context.

**Example**

- **Chunking.** Grouping content into chunks helps users process, understand and memorize it.

**Origin.** In 1956, George Miller argued that both immediate memory span and absolute judgment are limited to around seven pieces of information. Past that "channel capacity", confusion leads to wrong judgments.

**Apply it when building.** Chunk information instead of counting items. Don't make users memorize codes or values between screens. Show them where they need them.

---

## 19. Occam's Razor

> Among competing hypotheses that predict equally well, the one with the fewest assumptions should be selected.

In design: if two solutions work equally well, choose the simpler one.

**Key takeaways**

- The best way to reduce complexity is to never add it.
- Look at every element and remove as many as you can without hurting the overall function.
- A design is done only when nothing else can be removed.

**Origin.** Also called Ockham's razor or the *law of parsimony*. It's credited to William of Ockham (c. 1287–1347), an English Franciscan friar, philosopher and theologian.

**Apply it when building.** For every element, ask "does this need to be here?" Prefer one clear path over several clever ones, and strip features, fields and decoration that don't serve the user's goal.

---

## 20. Paradox of the Active User

> Users never read manuals but start using the software immediately.

People want to get their task done *now*. They skip documentation and learn by doing, even if that means mistakes, and even though learning the system properly would save them time later.

**Key takeaways**

- Users focus on their immediate task and don't want to spend time reading up front.
- It's a paradox because learning the system first would save them time in the long run.
- Put guidance *inside* the product, in context, so it helps people whatever path they take (for example, tooltips with useful hints).

**Origin.** Mary Beth Rosson and John Carroll defined the idea in 1987 in their work *Interfacing Thought: Cognitive Aspects of Human-Computer Interaction*. They saw that new users skipped the manuals and dove straight in, even when that meant running into errors and dead ends.

**Apply it when building.** Make the UI self-explanatory. Use inline hints, helpful empty states, contextual tooltips and good defaults. Treat docs as a backup, not the main way people learn, and make errors easy to recover from.

---

## 21. Pareto Principle

> For many events, roughly 80% of the effects come from 20% of the causes.

Effort and results are rarely balanced. A small share of features, users or issues usually drives most of the outcome.

**Key takeaways**

- Inputs and outputs are often unevenly distributed.
- A large group may contain only a few members that really matter to the outcome.
- Spend most of your effort where it benefits the most users the most.

**Origin.** It comes from economist Vilfredo Pareto, who noticed that 80% of Italy's land was owned by 20% of the population. The 80/20 lens works for analyzing any lopsided system, including UX strategy.

**Apply it when building.** Find the few features and flows most users rely on and make them excellent first. Fix the bugs that hit the most people. Don't over-invest in edge features at the cost of the core experience.

---

## 22. Parkinson's Law

> Any task will inflate until all of the available time is spent.

If a task *can* take longer, it will. Good UX shrinks the time a task takes so it finishes faster than people expect.

**Key takeaways**

- Keep task time within what users expect it to take.
- Finishing faster than expected makes the whole experience better.
- Use features like autofill to save time on important form data, so purchases, bookings and similar tasks finish quickly without dragging on.

**Origin.** C. Northcote Parkinson wrote it as the opening line of a humorous essay in *The Economist* in 1955, later reprinted in *Parkinson's Law: The Pursuit of Progress* (1958). He drew it from years of experience in the British Civil Service.

**Apply it when building.** Support browser autofill, saved addresses and payment methods, one-click actions and sensible defaults. Remove optional fields from critical flows, and show estimated times ("Takes 2 minutes") then beat them.

---

## 23. Peak-End Rule

> People judge an experience largely based on how they felt at its peak and at its end, rather than the total sum or average of every moment of the experience.

Memory doesn't average. People remember the most intense moment and the final moment, and they judge the whole experience by those two. This idea is closely related to Cognitive Bias.

**Key takeaways**

- Pay close attention to the most intense points and the final moments of the user journey.
- Find where your product is most helpful, valuable or fun, and design those moments to delight.
- People remember negative experiences more vividly than positive ones.

**Examples**

- **Mailchimp.** Sending an email campaign can be stressful, especially the first time. Mailchimp goes beyond a plain confirmation and adds illustration, subtle animation and humor to ease that moment.
- **Uber.** Negative moments are peaks too. By focusing on how people perceive time and waiting, Uber lowered cancellations after a ride request and avoided a negative emotional peak.

**Origin.** The 1993 study *"When More Pain Is Preferred to Less: Adding a Better End"* by Kahneman, Fredrickson, Schreiber and Redelmeier gave key evidence. Participants held one hand in 14°C water for 60 seconds. They held the other hand in 14°C water for 60 seconds and then an extra 30 seconds while it warmed slightly to 15°C. When asked which trial to repeat, most chose the *longer* one, simply because it ended less badly and they remembered it better.

**Apply it when building.** Make success and confirmation screens feel rewarding. Handle errors, waits and failures with care, since they become negative peaks. End flows on a high note: a clear next step, a thank-you, a small celebration.

---

## 24. Postel's Law

> Be liberal in what you accept, and conservative in what you send.

Accept whatever users give you, in whatever messy form, and return clean, consistent, predictable output.

**Key takeaways**

- Be empathetic, flexible and tolerant toward whatever actions or input users might give.
- Expect almost any kind of input, access method or ability, and still provide a reliable, accessible interface.
- The more you anticipate and plan for in design, the more resilient it will be.
- Accept varied input, translate it into what you need, set clear boundaries, and give clear feedback.

**Origin.** Also called the *Robustness Principle*, it was formulated by Internet pioneer Jon Postel as a guideline for TCP: implementations should be conservative in what they do and liberal in what they accept from others. Senders should follow the spec exactly, and receivers should accept slightly non-standard input as long as the meaning is clear.

**Apply it when building.** Accept phone numbers with or without spaces and dashes, dates in several formats, and emails with stray whitespace. Make search case-insensitive and typo-tolerant. Normalize input on the backend, and support all devices, input methods and assistive tech. Make error messages specific and helpful.

---

## 25. Selective Attention

> The process of focusing our attention only to a subset of stimuli in an environment — usually those related to our goals.

People filter out most of what's on the screen and notice only what seems relevant to their goal. Anything that doesn't seem relevant, or looks like noise, gets ignored. This idea is closely related to the Von Restorff Effect.

**Key takeaways**

- People filter out irrelevant information to stay focused on their task. Designers have to guide attention, prevent overload and distraction, and help people find what matters.
- **Banner blindness:** users ignore anything that looks like an ad, sits near ads, or appears where ads usually go. Don't style real content like ads or mix it into ad areas.
- **Change blindness:** big changes in an interface can go unnoticed when attention is limited and cues are weak. Check your design for changes that happen at the same time and compete for attention.

**Origin.** The theory took shape in the mid-20th century through several key contributions:

- **Cherry's Cocktail Party Effect (1953):** E. Colin Cherry studied how people focus on one voice while ignoring others.
- **Broadbent's Filter Theory (1958):** Donald Broadbent proposed an attention "bottleneck" that filters information by physical features before meaning is processed.
- **Treisman's Attenuation Model (1960):** Anne Treisman suggested unattended information is turned down, not blocked completely.
- **Deutsch & Deutsch's Late Selection Theory (1963):** all input is processed for meaning before selection happens.

Mackworth's 1950 vigilance research, motivated by WWII radar operators, was part of this work. Kahneman's 1973 capacity model later framed attention as a limited resource shared between tasks.

**Apply it when building.** Put key content and actions where users are already looking. Never make important information look like an ad. When something changes on screen (an error, a new item, updated state), give it a strong, clear cue, and avoid many changes happening at once.

---

## 26. Serial Position Effect

> Users have a propensity to best remember the first and last items in a series.

In any list, the start and the end stick in memory. The middle fades.

**Key takeaways**

- Put the least important items in the middle of lists, since people remember them least.
- Put key actions at the far left and far right of elements like navigation so they're easier to remember.

**Origin.** Hermann Ebbinghaus coined the term. It combines the *primacy effect* (first items are remembered well) and the *recency effect* (last items are remembered well). Companies such as Apple, Electronic Arts and Nike use it in their designs.

**Apply it when building.** In nav bars and bottom tab bars, put the most important items first and last. In lists, onboarding and feature summaries, open and close with the strongest points.

---

## 27. Tesler's Law

> Also known as the Law of Conservation of Complexity: for any system there is a certain amount of complexity which cannot be reduced.

Some complexity can't be removed, only moved. The question is who carries it: the system (designers and developers) or the user.

**Key takeaways**

- Every process has a core of complexity that can't be designed away. Either the system or the user has to carry it.
- Take as much of that burden off users as possible by dealing with complexity during design and development.
- Don't design for an idealized, perfectly rational user. Real people don't always behave rationally.
- Put guidance in context so it helps new users whatever path they take (for example, tooltips).

**Origin.** Larry Tesler worked at Xerox PARC in the mid-1980s and realized that how users interact with an application matters as much as the application itself. In an interview in Dan Saffer's *Designing for Interaction*, he argued that an engineer should spend an extra week cutting complexity rather than make millions of users spend an extra minute each. Bruce Tognazzini added a twist: when apps get simpler, people start attempting more complex tasks.

**Apply it when building.** Let the system do the hard work: smart defaults, autofill, auto-detecting card types and addresses, input formatting, and sensible error recovery. Handle edge cases in code instead of pushing them onto the user.

---

## 28. Von Restorff Effect

> Also known as the Isolation Effect: when multiple similar objects are present, the one that differs from the rest is most likely to be remembered.

The odd one out stands out and is remembered. That makes it a powerful tool for emphasis, but only when used sparingly.

**Key takeaways**

- Make important information and key actions visually distinct.
- Use restraint: too many emphasized elements compete with each other, and loud elements can be mistaken for ads.
- Don't rely only on color to show contrast, or you exclude people with color-vision deficiency or low vision.
- Be careful with motion as a way to stand out, since some users are motion-sensitive.

**Origin.** Named after German psychiatrist and pediatrician Hedwig von Restorff (1906–1962). In her 1933 study, people shown a list of similar items with one distinct item remembered that distinct item better.

**Apply it when building.** Give one primary CTA per view a distinct style, and highlight the recommended pricing plan. Use shape, size, icons or labels together with color, and respect `prefers-reduced-motion`.

---

## 29. Working Memory

> A cognitive system that temporarily holds and manipulates information needed to complete tasks.

Working memory is the mind's scratchpad. It's small and it fades fast, so interfaces should rely on what people *recognize*, not on what they must *recall*. This idea is closely related to Cognitive Load.

**Key takeaways**

- Working memory holds about 4–7 chunks at a time, and each fades after roughly 20–30 seconds. People also struggle to remember what they've already seen. Show only information that's necessary and relevant.
- Brains are good at recognizing things seen before but bad at holding new information ready to use. Support *recognition over recall*, for example by styling visited links differently and showing breadcrumbs.
- Put the memory burden on the system, not the user. Carry important information from screen to screen when needed, for example with comparison tables.

**Origin.** George A. Miller, Eugene Galanter and Karl H. Pribram coined the term in the 1960s, when theories compared the mind to a computer. In 1968, Atkinson and Shiffrin used it for their "short-term store". Today "working memory" usually replaces or includes "short-term memory", with more emphasis on *manipulating* information, not just holding it. Research on its brain basis goes back over a century to studies of the prefrontal cortex. Hitzig and Ferrier ran early ablation experiments, and Carlyle Jacobsen showed effects on delayed response in 1935–36.

**Apply it when building.** Keep users' earlier choices visible, such as order summaries and selected filters. Show breadcrumbs and visited-link styles. Use comparison views, and never ask users to remember a value from one screen to type it on another.

---

## 30. Zeigarnik Effect

> People remember uncompleted or interrupted tasks better than completed tasks.

An unfinished task nags at us. That pull can motivate people to come back and complete what they started.

**Key takeaways**

- Invite people to explore by clearly signaling that there's more content.
- Giving artificial progress toward a goal makes people more likely to finish.
- Show progress clearly to motivate completion.

**Origin.** Soviet psychologist Bluma Zeigarnik (1900–1988), a member of the Berlin School of experimental psychology and later the Vygotsky Circle, discovered the effect in the 1920s. Her memory study compared completed and incomplete tasks and found the incomplete ones easier to remember. She went on to help establish experimental psychopathology in the USSR and received the Lewin Memorial Award in 1983.

**Apply it when building.** Use profile-completion meters ("Your profile is 70% complete"), "continue where you left off" prompts, saved drafts, and partially visible content that hints there's more below or to the side (scroll cues, cut-off carousels).

---

## Quick checklist for agents

Before you ship any UI, run through this:

- **Looks & trust:** Is it visually polished? Did we test real behavior, not just impressions? *(Aesthetic-Usability)*
- **Choices:** Are options few, with a clear recommended default? *(Hick's Law, Choice Overload)*
- **Familiarity:** Does it follow common conventions and users' mental models? *(Jakob's Law, Mental Model)*
- **Grouping:** Are related things close, boxed, alike or connected, and unrelated things apart? *(Proximity, Common Region, Similarity, Uniform Connectedness)*
- **Simplicity:** Can anything else be removed? Is every shape and icon simple? *(Occam's Razor, Prägnanz)*
- **Memory:** Is content chunked? Does the system remember things so the user doesn't have to? *(Miller's Law, Chunking, Working Memory, Cognitive Load)*
- **Targets:** Are buttons big, well spaced and within easy reach? *(Fitts's Law)*
- **Speed:** Is there feedback within 400ms, plus loaders and progress for anything slower? *(Doherty Threshold)*
- **Input:** Does it accept messy input and return clean output? *(Postel's Law)*
- **Complexity:** Does the system handle the hard parts instead of the user? *(Tesler's Law)*
- **Emphasis:** Does exactly one key action stand out, without relying on color alone? *(Von Restorff, Selective Attention)*
- **Order:** Are the most important items first and last? *(Serial Position Effect)*
- **Motivation:** Is progress visible, ideally with a head start? *(Goal-Gradient, Zeigarnik)*
- **Moments:** Are the peak and the ending delightful, and are errors handled gracefully? *(Peak-End Rule)*
- **Learning:** Can someone use it without reading docs? *(Paradox of the Active User)*
- **Priority:** Did we polish the 20% of features that matter most? *(Pareto Principle)*
- **Effort:** Does the task finish faster than users expect? *(Parkinson's Law)*
- **Focus:** Does it support deep focus without needless interruptions? *(Flow)*
- **Ethics:** Are we using psychology to help users, not to manipulate them? *(Cognitive Bias)*
