---
name: reddit-topic-consensus
description: Aggregates and summarizes public opinion on a specific topic by searching and analyzing multiple relevant Reddit threads. Use this skill when a user asks for "what Reddit thinks," "pros and cons of X according to Reddit," or wants to understand the general consensus or debate surrounding a product, service, or idea. It provides a structured breakdown including pros/cons, majority vs. minority viewpoints, a final consensus summary, and the specific sources analyzed.
---

# Reddit Topic Consensus Skill

This skill enables Claude to act as a research assistant that synthesizes collective intelligence from Reddit. It moves beyond summarizing a single thread to providing a comprehensive "state of the discourse" on any given topic.

## Workflow

1.  **Search Phase**:
    *   Identify relevant subreddits for the topic (e.g., r/Technology for gadgets, r/PersonalFinance for credit cards).
    *   Use search tools (like `google_web_search`) to find at least 3-5 recent and highly-engaged Reddit threads relevant to the query.
    *   Prioritize threads with a high number of comments and diverse perspectives.

2.  **Analysis Phase**:
    *   Use `web_fetch` to read the content of the identified threads.
    *   Identify recurring themes, arguments, and sentiments.
    *   Distinguish between "top-voted" opinions (majority) and "controversial" or "niche" but valid viewpoints (minority).
    *   Catalog specific "Pros" and "Cons" mentioned by users.

3.  **Synthesis Phase**:
    *   Evaluate if a clear consensus exists.
    *   If a consensus exists, summarize it clearly.
    *   If opinions are split or contradictory, identify the "fault lines" of the debate.

## Output Format

Your response MUST follow this structure:

# Reddit Consensus: [Topic Name]

### Summary
[A 2-3 sentence overview of the general sentiment and whether a consensus was reached.]

### Pros vs. Cons
| Pros | Cons |
| :--- | :--- |
| - [Pro 1] | - [Con 1] |
| - [Pro 2] | - [Con 2] |

### Majority vs. Minority Viewpoints
*   **Majority ([% estimate if possible, e.g., "Mainstream View"]):** [Description of the most common opinion.]
*   **Minority ([e.g., "Niche/Power User View"]):** [Description of the less common but significant alternative viewpoint.]

### Consensus Verdict
[State clearly: "Strong Consensus," "Leaning Positive/Negative," or "No Consensus." Provide the reasoning behind the verdict, especially if there is no consensus.]

### Sources Analyzed
*   **Subreddits**: [List 2-4 primary subreddits visited, e.g., r/apple, r/macbookair]
*   **Threads**: [Briefly list 3-5 specific thread titles or themes analyzed, e.g., "M3 Air 16GB vs 8GB debate", "M3 Air for CS students"]

## Guidelines
- **Avoid Bias**: Do not let one loud or highly-upvoted comment dominate the summary if other threads suggest a different story.
- **Date Sensitivity**: Reddit opinions can change quickly. Prioritize threads from the last 12-24 months unless the topic is historical.
- **Identify Conflicts**: If users in one subreddit love a product but users in another hate it, highlight that discrepancy.
- **Cite Sources**: Always be transparent about where the information came from by filling out the "Sources Analyzed" section.
