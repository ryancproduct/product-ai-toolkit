
Let's start by saying, I'm not a writer :) But I've been putting together some work for our internal PM team around how I use AI, and that got me thinking, why not share it more broadly? I hope it helps you, or another PM you work with, get kickstarted with the superpower that is AI.

Let's get into it!


You're probably copy-pasting feature specs into ChatGPT/Claude/Gemini. Maybe you're using it to polish your PRDs or draft user stories. Perhaps you've even made a custom GPT here or there with your company's product principles.

And it's... fine. Mildly helpful. Occasionally impressive. But fundamentally, you're still doing most of the work — gathering context, making connections, validating outputs. The AI is just a faster typist.

There's a better way.

This post and setup below all stemmed from an internal question asked one day at an engineering town hall: "Can PMs use Claude Code?" At the time I was thinking, of course — that seemed like an odd question as I was using it A LOT. But after some digging, I found out there's still stigma around Claude Code and who it's aimed at.

So, let's try and change that.


## The copy-paste trap

The problem with how most product managers use AI isn't the quality of the models. It's that we're treating them like search engines or autocomplete on steroids.

We paste in a feature idea and ask for user stories. We copy-paste our product strategy and ask for feedback. We feed it meeting notes and ask for a summary. Each interaction is isolated, stateless, and context-free. The AI has no memory of your product, your users, your constraints, or your company's strategic priorities.

So you end up doing the hard part anyway: pulling together analytics data, cross-referencing design patterns, checking what's feasible, validating assumptions against actual user research. The AI gives you a starting point, but you're still the integration layer between all your tools and knowledge sources.

The result? AI becomes a glorified writing assistant. Useful for wordsmithing, but not fundamentally changing how you work.

## This is not a new concept - Context engineering, not prompt engineering

What if instead of copy-pasting context into AI, you could encode context *around* it?

That's context engineering. You're not crafting the perfect prompt — you're building systems that give AI direct access to the context it needs: your product analytics, your design system, your issue tracker, your company's decision-making frameworks, your past research.

When I spec a feature, I don't want to manually copy analytics data into a chat window. I want the AI to pull that data itself, analyse it against established frameworks, and surface insights I might have missed.

When I'm evaluating an experiment, I don't want to describe my company's experimentation methodology in prose. I want the AI to know it, apply it, and validate that the instrumentation I need actually exists in our analytics taxonomy.

This shift - from prompting to tooling - is what makes AI genuinely useful for product work.

## What this looks like in practice

I built a bit of an AI operating system for product management on top of Claude Code. It's called the AI PM Kit (real original), and it's a collection of commands, skills, and specialist agents that handle real PM workflows end-to-end.

Here are four examples of what changes when you give AI the right context and tools.

**Evaluating feature ideas with `/debate`**

I typed: `/debate "Add a bulk actions feature for managers"`

What came back wasn't a generic pros-and-cons list. It was a structured debate between two specialist agents. One playing Champion, the other Sceptic. The Champion made the case with evidence from our Amplitude data on power user behaviour. The Sceptic raised feasibility concerns grounded in our actual tech stack and flagged edge cases I hadn't considered.

The output: a risk register, a suggested MVP scope, and a go/no-go recommendation based on actual usage patterns. Not hypotheticals.

I didn't copy-paste any analytics data. The system pulled it directly via MCP integrations.

**Designing experiments with `/experiment`**

I ran: `/experiment "Test whether inline guidance increases form completion"`

The system generated a full experimental design: hypothesis, success metrics, sample size calculation, and a week-by-week rollout plan. But more importantly, it validated that the events I needed for measurement already existed in our analytics taxonomy. When they didn't, it told me which events to instrument.

It applied our company's statistical rigour standards, power analysis, multiple testing corrections, minimum detectable effects, without me having to specify any of that. The context was already encoded.

**Prototyping with `/rapid-prototype`**

For this one, I went the extra mile and used the Figma MCP to review our design system and build out a working HTML file and claude.md file containing all it needed to know. This was a great step, as I simply needed to describe a feature concept in a few sentences and the system generated a clickable HTML prototype using components from our actual design system, complete with realistic data and interaction states.

Not a static mockup. Not a generic wireframe. A functional prototype I could put in front of users within minutes, matching our established patterns and visual language.

The other part I LOVE about this process is the ability to tweak and change this WITH A CUSTOMER. During an interview you can work together and refine what the must-haves and nice-to-haves are, live.

**Building a knowledge base with `/learn`**

This one's subtle but it's been the biggest unlock. Run `/learn "JTBD framework for B2B SaaS"` and the system does a deep research dive, web sources, your internal docs, whatever context it can pull, then saves a structured knowledge file that persists across sessions.

Next time you run `/jtbd` or `/debate`, that knowledge is already there. You don't re-explain it. You don't re-paste it. It compounds. And when you need to pull something back up, `/recall` gives you instant access to everything you've built up, no digging through notes or wikis.

I've used this to build up domain knowledge on everything from experimentation methodology to competitor positioning to regulatory frameworks. Each `/learn` adds to a growing knowledge base that makes every other command smarter. The AI doesn't start from zero each session — it starts from everything it's learned so far.

This is the part most people miss about context engineering. It's not just about connecting tools. It's about building systems where knowledge accumulates and compounds over time.

## What's in the toolkit

The above are some examples, but I thought I'd try share the full toolkit with you.

The AI PM Kit includes:

- **15 commands** for common PM tasks — experiments, competitive analysis, JTBD, user stories, PRDs, impact sizing, and more
- **14+ multi-step skills (default and my own)** that chain together research, analysis, and synthesis with parallel agent orchestration
- **9 specialist agents** (Market Research, Data Analysis, UX Design, Technical Architecture, etc.) that can work in parallel
- **Deep MCP integrations** with Amplitude, Jira, Confluence, Slack, Figma, and more
- **Encoded frameworks** from Teresa Torres (Opportunity Solution Trees), Jobs-to-be-Done, INVEST criteria, and other established PM methodologies

It's not a chatbot. It's a system. Each command delegates to the right combination of agents, pulls the right context from the right tools, and applies the right frameworks automatically.

## Built in public, shared for free

I built this because I was frustrated with how shallow most "AI for PMs" tools felt. They're either generic productivity apps with AI bolted on, or they're so abstracted from real product work that they're not actually useful.

I wanted something that understood how I worked — the messy reality of juggling analytics, research, design, engineering constraints, multiple products and stakeholder opinions while trying to make good decisions quickly.

The entire system is open source. Every command, every agent, every skill. You can use it as-is, fork it, rip out the parts that don't fit your context, or just read through it to see one approach to context engineering.

If you're curious what product management looks like when AI has proper context and tooling (not just a text box) — check it out: https://github.com/ryancproduct/product-ai-toolkit

The future of AI-augmented product work isn't better prompts. It's better systems.
