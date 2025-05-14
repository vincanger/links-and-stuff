# EFFECTIVE AF PROMPTS

## For Creating and Improving Rules

- “Where do my blind spots tend to be when I prompt? Help me create a set of cursor rules files that fills these gaps in my knowledge and positively augments my abilities…”
- “Based on this conversation, could we create or improve some cursor rules? Think about which ones would be the most impactful given the codebase at hand and the way I prompt”

## For Implementation Planning

- “I want to create a <insert app type here> with the current template project I'm in which uses <insert tech stack here>. Leveraging this stack’s features, let's build the app using a modified vertical slice implementation approach that's suitable for LLM-assisted coding based on the following spec:
    - <feature 1>
    - <feature 2>
    - <feature 3>
    - …
    
    With these specifications in mind, I want you to first evaluate the project template and think about a few possible Product Requirement Document (PRD) approaches before landing on the best one. Provide reasoning why this would be the best approach. Remember, we want to use a vertical slice implementation approach so we can start with basic implementations of features first, and add on complexity from there.”
    
- “From this PRD, create an actionable, step-by-step plan that we can use as a guide for LLM-assisted coding. Before you create the plan, think about a few different plan styles that would be suitable for this project and the implementation style before selecting the best one. Give your reasoning for why you think we should use this plan style. Remember that we will constantly refer to this plan to guide our coding implementation so it should be well structured, concise, and actionable, while still providing enough information to guide the LLM. Write the plan to a new [`plan.md`](http://plan.md) document”

## For General Reasoning

- “Before we continue, think about 3 possible implementation strategies based on my current project and aims. Chose the best strategy of these 3 and give me your rationale for choosing it.”