# AI Interaction Protocol

This document outlines the best practices for instructing our AI coding agent to ensure predictable, high-quality output, incorporating principles for advanced models like Claude and Gemini.

## The "System Prompt" First Workflow

For any new project or major feature, the interaction must begin with the **System Prompt**.

1.  **Define the Persona:** Fill out the `00_SYSTEM_PROMPT_TEMPLATE.md`. This tells the AI *who it is* and establishes the ground rules for the entire session.
2.  **Initiate the Session:** Start a new chat session with the AI. Your *very first message* should be the completed System Prompt. This sets the context for everything that follows.
3.  **Proceed with Modular Tasks:** Once the AI has acknowledged the System Prompt, you can begin feeding it modular tasks using the other templates (`02_FEATURE_SPEC_TEMPLATE.md`, `03_COMPONENT_SPEC_TEMPLATE.md`, etc.).

## Guiding Principles

1.  **Be Explicit, Not Implicit:** The AI does not have business context. Spell everything out. Never assume it "knows" what you mean.
2.  **One Task, One Prompt:** Each prompt should correspond to a single, well-defined task (e.g., "Create this component," "Write this function"). Do not bundle unrelated requests.
3.  **Provide Examples:** When specifying a complex component or function, include a small, concrete example of the data structures (props) it will receive and, if applicable, the output it should generate. This dramatically improves accuracy.
4.  **Specify the "Don'ts":** If there's something you specifically want to avoid (e.g., "Do not use the `useState` hook; use `useReducer` instead"), state it clearly in the specification.

## Feedback & Iteration

If the AI's output needs changes, provide clear, specific feedback.

-   **Bad Feedback:** "That's wrong, try again."
-   **Good Feedback:** "This is a good start. However, you used a `<div>` for the button. Per our accessibility standards, please change it to a `<button>` element. Also, please ensure the `delete-task` event is emitted as specified in the original spec."