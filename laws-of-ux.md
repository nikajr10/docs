# Laws of UX

> Source: https://lawsofux.com/. Before you design or build any UI, check it against these laws.

## Heuristics

| # | Law | Explanation | Best use cases |
|---|-----|-------------|----------------|
| 1 | **Aesthetic-Usability Effect** | Users see good-looking design as more usable, and they forgive small usability issues when the design looks good. | Landing pages, onboarding, first impressions. A polished UI earns trust, but it shouldn't hide real usability problems in testing. |
| 2 | **Doherty Threshold** | Productivity rises when the system responds in under ~400ms, so neither the user nor the computer is waiting. | Search-as-you-type, button feedback, page transitions. Use optimistic UI, skeleton loaders and progress bars when work takes longer. |
| 3 | **Fitts's Law** | The time to reach a target depends on its distance and size. Big, close targets are faster to hit. | Primary CTAs, mobile tap targets (≥44px), placing actions near the user's cursor or thumb, edge or corner menus. |
| 4 | **Goal-Gradient Effect** | Motivation goes up as people get closer to a goal. | Progress bars, multi-step checkout, onboarding checklists, loyalty cards (start users with some progress already done). |
| 5 | **Hick's Law** | Decision time grows with the number and complexity of choices. | Navigation menus, pricing pages, forms. Cut options, highlight a recommended choice, and break complex tasks into steps. |
| 6 | **Jakob's Law** | Users spend most of their time on other sites, so they expect yours to work the same way. | Standard patterns: logo top-left links home, cart icon top-right, familiar form controls. Don't reinvent common conventions. |
| 7 | **Miller's Law** | The average person keeps about 7 (±2) items in working memory. | Group content into small chunks, such as phone numbers, nav items and dashboard widgets. Don't use it as a hard limit on menu length. |
| 8 | **Parkinson's Law** | A task expands to fill the time available for it. | Checkout and forms: autofill, saved details and one-click actions so tasks finish faster than users expect. |
| 9 | **Postel's Law** | Be liberal in what you accept and conservative in what you send. | Form inputs: accept many phone or date formats, trim whitespace, give clear and consistent output and error messages. |

## Gestalt

| # | Law | Explanation | Best use cases |
|---|-----|-------------|----------------|
| 10 | **Law of Common Region** | Elements inside a clearly bounded area are seen as a group. | Cards, panels, bordered form sections, grouped settings. |
| 11 | **Law of Proximity** | Objects that are close to each other are seen as a group. | Spacing in forms (label next to its input), grouping related buttons, separating sections with whitespace. |
| 12 | **Law of Prägnanz** | People read complex or ambiguous images in their simplest form. | Icons, logos, illustrations. Keep shapes simple and recognizable. |
| 13 | **Law of Similarity** | Elements that look alike are seen as a group, even when they're apart. | Consistent styling for links, buttons and tags. Make different functions look different. |
| 14 | **Law of Uniform Connectedness** | Visually connected elements (lines, shared backgrounds) look more related than unconnected ones. | Steppers, timelines, connected tabs, linking a tooltip to its trigger. |

## Cognitive biases & psychology

| # | Law | Explanation | Best use cases |
|---|-----|-------------|----------------|
| 15 | **Choice Overload** | Too many options overwhelm people and lead to no decision (the paradox of choice). | Product listings, pricing tiers, settings. Add filters, comparison views and sensible defaults. |
| 16 | **Chunking** | Breaking information into small groups that make sense together. | Long forms split into steps, formatted card or phone numbers, scannable content with headings and bullets. |
| 17 | **Cognitive Bias** | Systematic errors in thinking that shape how we perceive things and decide. | Know biases like anchoring and framing to design ethically. Use them to help users, never for dark patterns. |
| 18 | **Cognitive Load** | The mental effort needed to understand and use an interface. | Remove clutter, use progressive disclosure, show only what's needed for the current task. |
| 19 | **Flow** | A state of energized focus and full involvement in an activity. | Editors, games, creative tools. Cut interruptions, give instant feedback, match the challenge to the user's skill. |
| 20 | **Mental Model** | A compressed model of what we think we know about how a system works. | Match the UI to users' existing models: a cart metaphor, folder structures. Research users before designing. |
| 21 | **Peak-End Rule** | People judge an experience mostly by its peak and its end, not the average. | Success screens, order confirmations, delightful moments, handling error states gracefully. |
| 22 | **Selective Attention** | People focus only on stimuli related to their goals and ignore the rest. | Avoid banner blindness: don't make important info look like an ad. Put key content where users are already looking. |
| 23 | **Serial Position Effect** | People remember the first and last items in a series best. | Put key nav items at the start and end, such as bottom tab bars and list ordering. |
| 24 | **Von Restorff Effect** | Among similar items, the one that differs is the one people remember (isolation effect). | Highlight the primary CTA or the recommended pricing plan. Use it sparingly, and don't rely on color alone (accessibility). |
| 25 | **Working Memory** | A short-term cognitive system that holds and handles information during a task. | Don't make users remember things across screens: show previous choices, use breadcrumbs, mark visited links. |
| 26 | **Zeigarnik Effect** | People remember unfinished or interrupted tasks better than finished ones. | Profile-completion meters, "continue where you left off", saved drafts, incomplete-task reminders. |

## Principles

| # | Law | Explanation | Best use cases |
|---|-----|-------------|----------------|
| 27 | **Occam's Razor** | Among solutions that work equally well, pick the one with the fewest assumptions. | Strip every element that doesn't serve the user's goal. The simplest design that works wins. |
| 28 | **Paradox of the Active User** | Users never read manuals. They start using the software right away. | Contextual tooltips, inline hints, empty-state guidance instead of long tutorials or docs. |
| 29 | **Pareto Principle** | Roughly 80% of the effects come from 20% of the causes. | Prioritize the 20% of features most users rely on. Focus testing and polish there first. |
| 30 | **Tesler's Law** | Every system has complexity that can't be removed. Someone has to deal with it, either the system or the user. | Move complexity to the system: smart defaults, autofill, auto-detecting address or card type. |
