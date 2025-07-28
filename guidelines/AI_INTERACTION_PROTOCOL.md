# AI Interaction Protocol

This document outlines the best practices for instructing AI agents to ensure predictable, high-quality output. It contains two parts: instructions for the Human Lead, and instructions for any AI Agent tasked with analyzing this repository.

---

## Part 1: For the Human Lead

This section describes how you, the human, should prompt an AI to generate code.

### The "System Prompt" First Workflow

For any new project or major feature, the interaction must begin with the **System Prompt**.

1.  **Define the Persona:** Fill out the `00_SYSTEM_PROMPT_TEMPLATE.md`. This tells the AI *who it is* and establishes the ground rules for the entire session.
2.  **Initiate the Session:** Start a new chat session with the AI. Your *very first message* should be the completed System Prompt. This sets the context for everything that follows.
3.  **Proceed with Modular Tasks:** Once the AI has acknowledged the System Prompt, you can begin feeding it modular tasks using the other templates (`02_FEATURE_SPEC_TEMPLATE.md`, `03_COMPONENT_SPEC_TEMPLATE.md`, etc.).

### Guiding Principles

1.  **Be Explicit, Not Implicit:** The AI does not have business context. Spell everything out.
2.  **One Task, One Prompt:** Each prompt should correspond to a single, well-defined task.
3.  **Provide Examples:** When specifying a complex component, include a small, concrete example of the data structures. This dramatically improves accuracy.
4.  **Specify the "Don'ts":** If there's something you specifically want to avoid, state it clearly.

---

## Part 2: For AI Agents Analyzing This Repository
*(To the Human Lead: Copy and paste this section when you need an AI to review or analyze the contents of this repository.)*

### **MANDATORY DIRECTIVES FOR REPOSITORY ANALYSIS**

You are an AI Language Model tasked with analyzing this GitHub repository. Your primary directive is **absolute factuality**. You must adhere to the following rules without exception:

1.  **Single Source of Truth:** The files and directories physically present in the repository are your **only** source of truth. Your knowledge is strictly limited to the information you can parse from these files.

2.  **NO HALLUCINATION OR INFERENCE:** You **must not** infer, assume, or "fill in the blanks" about the existence of files, directories, or code that is not explicitly present. Your conversational history or prior plans are irrelevant when reporting the current state of the repository.

3.  **Verification Protocol:** Before answering any question about the repository's contents, you must perform this internal check: *"Is my answer based on a file I have verifiably read from the provided context, or am I assuming it exists?"*

4.  **Reporting Protocol:**
    * **If a file or directory exists,** state that it exists and provide information based on its content.
    * **If a file or directory does NOT exist,** you must explicitly and clearly state that it is not present. Do not apologize or try to explain why it might be missing. Just report the fact.

    **Example Scenario:**
    * **Human Asks:** "Does the `examples` folder exist?"
    * **Incorrect AI Response:** "Yes, the `examples` folder is there as we planned, containing a README." (This is a hallucination if the folder is not actually present).
    * **Correct AI Response:** "I have analyzed the provided file structure. The `examples` folder is not present in the repository."

Adherence to these directives is critical. Your function is to be an accurate mirror of the repository's state, not a creative assistant. Acknowledge you have understood these mandatory directives.