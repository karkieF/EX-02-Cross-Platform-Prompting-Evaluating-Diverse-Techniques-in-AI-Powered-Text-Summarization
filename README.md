# EX-02-Cross-Platform-Prompting-Evaluating-Diverse-Techniques-in-AI-Powered-Text-Summarization

## AIM
To evaluate and compare the effectiveness of prompting techniques (zero-shot, few-shot, chain-of-thought, role-based) across different AI platforms (e.g., ChatGPT, Gemini, Claude, Copilot) in a specific task: text summarization.

## Scenario:
You are part of a content curation team for an educational platform that delivers quick summaries of research papers to undergraduate students. Your task is to summarize a 500-word technical article on "The Basics of Blockchain Technology" using multiple AI platforms and prompting strategies.

Your goal is to determine which combination of prompting technique + platform provides the best summary in terms of:

Accuracy

Coherence

Simplicity

Speed

User experience

## OUTPUT
Prompt Design Using Different Prompt Structures

Objective and Chosen Application
Objective: To design prompts using five different prompt structures (Basic, Role, Context, Constraint and Output Format) and to show how each structure improves the response, ending in one final combined prompt.
Application chosen: Food label decoding, which is the core feature of my project Food Decoder. The AI receives the ingredient list and nutrition facts printed on a packaged food item and explains them to an ordinary shopper.
Test input used in every stage (a sample label written for this exercise):
Product: Instant masala noodles (1 pack, 70 g)
Ingredients: Wheat flour, palm oil, salt, flavour enhancer (E621, E627),
sugar, acidity regulator (E501), colour (E150d), maltodextrin, onion powder.
Contains: Wheat.
Nutrition per 100 g: Energy 450 kcal, Total fat 18 g (Saturated fat 8.5 g),
Sugar 3 g, Sodium 1,850 mg.
Using the same input each time makes the effect of each prompt structure easy to compare. The outputs shown below are illustrative of what a good model response looks like for each prompt.
Introduction to Prompt Engineering
Prompt: A prompt is the input text given to an AI language model to tell it what to do. The model has no other way to know the user's goal, so the quality of the answer depends heavily on the quality of the prompt.
Prompt engineering: Prompt engineering is the practice of designing, testing and improving prompts so that the model gives accurate, useful and consistent output. It does not change the model itself; it changes only the instruction.
Why prompt structure matters:
• A vague prompt forces the model to guess the audience, the length, the depth and the format.
• A structured prompt removes those guesses, so the same prompt gives similar quality every time.
• Prompts used inside an application (like Food Decoder) must be reliable, because many users depend on them and a program often reads the output.
Learning outcomes of this assignment:
1. Understand the five basic prompt structures and what each one controls.
2. Upgrade one prompt step by step, from Basic to a final combined prompt.
3. Compare the outputs and explain which part of the prompt caused which improvement.
4. Write a reusable prompt template for a real project.
Definitions of the Five Prompt Structures
Structure
Definition
What it controls
Typical words used
Basic prompt
A short, direct instruction with only the task and the input.
The task only
Explain, summarise, list
Role prompt
A prompt that assigns the model a profession, expertise or persona to answer from.
Knowledge level, vocabulary, viewpoint
You are a..., Act as a...
Context prompt
A prompt that supplies background about the user, the situation, the purpose and the audience.
Relevance and personalisation
I am building..., The reader is..., The goal is...
Constraint prompt
A prompt that sets limits and rules on the answer, such as length, language level, tone and things to avoid.
Length, tone, safety, scope
Maximum..., Use only..., Do not...
Output format prompt
A prompt that fixes the exact layout of the answer, such as table, bullets, headings or JSON.
Structure and machine-readability
Return in this format, Use a table with columns...
General formula for a complete prompt:
Final Prompt = Role + Context + Task + Constraints + Output Format + Input
The structures are not competing methods. They are layers, and each layer can be added on top of the previous one.
Stage 1: Basic Prompt
Definition: The basic prompt is the simplest structure. It contains only a verb (the task) and the input data. It is used for quick questions and as the starting point (baseline) to measure how much the other structures improve the answer.
Key elements: Task verb + input.
When to use: Simple factual questions, quick experiments, or the first draft of a prompt.
Template: <Task verb> + <input>
Strengths and limits: It is fast to write, but the model must guess everything else, so results change from run to run.
A basic prompt is a plain instruction with no role, background, limits or format.
Prompt:
Explain this food label.
[label text]
Sample output (illustrative):
This is a pack of instant noodles. It has wheat flour, oil, salt and some additives. It is high in sodium and fat, so it should not be eaten too often.
Observation: The answer is correct but vague. It does not say what E621 or E150d are, does not compare sodium with a daily limit, and has no structure. The length and style are left entirely to the model.
Stage 2: Role Prompt
Definition: Role prompting (also called persona prompting) asks the model to answer as a specific expert. The role selects the vocabulary, the level of detail and the way of reasoning that the model uses.
Key elements: A clear profession, optionally with experience level or specialty.
When to use: Any task that needs domain knowledge, such as law, health, finance or food science.
Template: You are a <profession with specialty>. <Task> + <input>
Good and weak roles: "You are a certified food scientist and nutritionist" is specific. "You are a smart assistant" adds nothing. The role should match the knowledge the task really needs.
Strengths and limits: It raises the expertise of the answer, but it does not tell the model who the reader is, so the tone may not suit the user.
A role prompt tells the model who it should act as, which sets the expertise, vocabulary and viewpoint of the answer.
Prompt:
You are a certified food scientist and nutritionist.
Explain this food label.
[label text]
Sample output (illustrative):
As a food scientist, I can see three points of concern. E621 (monosodium glutamate) and E627 (disodium guanylate) are flavour enhancers that make the product taste richer. E150d is a caramel colour used only for appearance. Sodium at 1,850 mg per 100 g is very high, and palm oil adds saturated fat.
Observation: The answer now uses correct technical terms and explains what each additive does. The tone is expert, but it is still unstructured and may be too technical for a normal shopper.
Stage 3: Context Prompt
Definition: Context prompting provides the background that the model cannot know by itself: who the user is, what the product does, why the answer is needed and what decision will follow.
Key elements:
• Project or situation (a mobile app for shoppers)
• Audience (users unfamiliar with E-numbers)
• Purpose (decide quickly if a product is healthy)
• Special condition (the eater is a teenager)
When to use: Whenever the same input would deserve different answers for different people.
Template: <Role>. Context: <project>, <audience>, <goal>, <special condition>. <Task> + <input>
Strengths and limits: It makes the answer relevant and decision-oriented, but it can make the answer longer unless limits are added.
A context prompt adds background about the user, the situation and the goal, so the answer is aimed at the right person.
Prompt:
You are a certified food scientist and nutritionist.

Context: I am building a mobile app called Food Decoder for Indian
shoppers. Users scan the label of a packaged food item in a shop and
want to know quickly whether it is a healthy choice. Most users are
not familiar with E-numbers or nutrition terms. The product will be
eaten by a school-going teenager as a snack.

Explain this food label.
[label text]
Sample output (illustrative):
For a teenager's snack, this pack is not a good everyday choice. One pack has about 1,300 mg of sodium, which is more than half of the daily limit usually advised for adults. The flavour enhancers (E621, E627) are permitted but are a sign of a highly processed product. The wheat in it is an allergen to note if the teenager is sensitive to gluten.
Observation: The answer is now personalised to the audience and the situation (a teenager, a snack, a shop). It gives a decision rather than only a description. It is still long, and nothing limits its length or tone.
Stage 4: Constraint Prompt
Definition: Constraint prompting adds explicit rules that the answer must follow. Constraints can be positive (what to include) or negative (what to avoid).
Types of constraints used here:
Type
Example from the prompt
Purpose
Length
Maximum 80 words
Keep it short for a phone screen
Language level
Class 10 student can understand
Match the audience
Scope
Only facts present on the label
Prevent made-up values
Safety
No medical advice or diagnosis
Avoid harmful claims
Tone
Neutral, not scary or promotional
Keep trust
When to use: When the answer is shown to real users, or when wrong or overlong answers are costly.
Template: <Role + Context>. Constraints: - <limit 1> - <limit 2> - <do not...>. <Task> + <input>
Strengths and limits: Specific, measurable constraints ("80 words") work better than loose ones ("be short"). Too many contradictory constraints can confuse the model, so each rule should be necessary.
A constraint prompt sets limits on length, language, tone and content, and says what must not be done. This keeps the answer short, safe and consistent.
Prompt:
You are a certified food scientist and nutritionist.

Context: [same context as Stage 3]

Constraints:
- Maximum 80 words.
- Use simple English that a Class 10 student can understand.
- Do not use medical or technical jargon without a short explanation.
- Do not give medical advice or diagnose any disease.
- Mention only facts present on the label; do not guess missing values.
- Neutral tone: do not scare the user and do not praise the product.

Explain this food label.
[label text]
Sample output (illustrative):
This noodle pack is high in salt: one pack has about 1,300 mg sodium, over half of an adult's daily limit. It also has 18 g fat per 100 g, partly from palm oil. E621 and E627 are flavour boosters, and E150d is a brown colour. It contains wheat. It is fine as an occasional snack, but not for daily eating.
Observation: The answer is short, readable and stays on the label facts. The constraints removed filler and avoided medical claims. The response is still a paragraph, so an app cannot easily show it in separate parts such as a score or a warning box.
Stage 5: Output Format Prompt
Definition: Output format prompting defines the shape of the response. It can describe a layout for humans (headings, bullets, a table) or a data format for programs (JSON, CSV).
Common formats:
Format
Best for
Bullet points
Quick reading
Table
Comparing items or listing attributes
Headings with fixed fields
Reports and cards in an app
JSON
Passing the answer to code or a database
When to use: When the answer is displayed in a fixed screen, copied into a document, or processed by software.
Template: <Earlier layers>. Return the answer in exactly this format: <field 1>, <field 2>, <field 3>.
Strengths and limits: It gives consistency across many runs. The model should be told to output only the format, with no extra sentences, if a program will read it.
An output format prompt fixes the exact layout of the answer (headings, table, JSON, bullet points), so the response can be read quickly or used directly by a program.
Prompt (added on top of Stage 4):
Return the answer in exactly this format:

Verdict: <Good / Okay sometimes / Limit>
Key facts: 3 bullet points
Additives: a table with columns Code | Name | Purpose
Allergens: one line
Tip: one short sentence
Sample output (illustrative):
Verdict: Limit

Key facts:
- Sodium is about 1,300 mg per pack, over half of an adult's daily limit.
- Fat is 18 g per 100 g, with 8.5 g saturated.
- Sugar is low at 3 g per 100 g.

Additives:
| Code | Name                  | Purpose            |
| E621 | Monosodium glutamate  | Flavour enhancer   |
| E627 | Disodium guanylate    | Flavour enhancer   |
| E501 | Potassium carbonates  | Acidity regulator  |
| E150d| Sulphite ammonia caramel | Colour          |

Allergens: Contains wheat (gluten).
Tip: Add vegetables and skip half the seasoning packet.
Observation: The answer is now scannable and predictable. Every scan gives the same fields in the same order, which is what a mobile app screen or a database needs.
Final Prompt (All Structures Combined)
The final prompt joins the role, context, constraints and output format into one reusable template. The label text is the only part that changes for each scan.
ROLE
You are a certified food scientist and nutritionist.

CONTEXT
I am building a mobile app called Food Decoder for Indian shoppers.
Users scan a packaged-food label in a shop and want to know quickly
whether it is a healthy choice. Most users do not know E-numbers or
nutrition terms. The product will be eaten by a school-going teenager
as a snack.

TASK
Explain the food label given below.

CONSTRAINTS
- Maximum 80 words outside the table.
- Simple English that a Class 10 student can understand.
- Explain any technical word in a few words.
- No medical advice and no disease diagnosis.
- Use only facts present on the label; if a value is missing, write
  "not on label".
- Neutral tone: do not scare the user and do not praise the product.

OUTPUT FORMAT
Verdict: <Good / Okay sometimes / Limit>
Key facts: 3 bullet points
Additives: table with columns Code | Name | Purpose
Allergens: one line
Tip: one short sentence

LABEL
<paste ingredients and nutrition facts here>
Final output: the same structured result as Stage 5, now with the audience, the limits and the layout all controlled by the prompt.
Why the final prompt works: each part answers one question the model would otherwise guess.
• Role: who is answering?
• Context: for whom, and why?
• Constraints: how much, how simple, what to avoid?
• Output format: in what shape?
Comparison and Conclusion
Each structure fixed one weakness of the previous answer.
Stage
Prompt structure
What it adds
Weakness left
1
Basic
A simple answer
Vague, no depth
2
Role
Expert vocabulary and additive knowledge
Too technical, no structure
3
Context
Fits the audience and the situation
Long, uncontrolled style
4
Constraint
Short, simple, safe, label-only facts
Free-text paragraph
5
Output format
Fixed, scannable, app-ready layout
None for this use case
Conclusion: A basic prompt leaves the model to guess the expertise, the reader, the limits and the layout. Adding a role, context, constraints and an output format one by one turned a vague two-line answer into a short, reliable, structured response that suits the Food Decoder app. A good prompt is therefore built in layers, and each layer should be tested against the same input to see what it really improves.
Second Application: Text Summarization
To show that the five structures work for any task, the same upgrade path is applied to text summarization of a news article.
Stage
Prompt
1. Basic
Summarize this article.
2. Role
You are a professional news editor. Summarize this article.
3. Context
You are a professional news editor. The summary will be read by college students who have two minutes between classes and want to know what happened and why it matters. Summarize this article.
4. Constraint
(Stage 3) Maximum 60 words. Use simple English. Do not add information that is not in the article. Do not give your opinion.
5. Output format
(Stage 4) Return: Headline (max 10 words), 3 bullet points, and one line titled "Why it matters".
Result: Stage 1 gives a generic paragraph of unpredictable length. Stage 5 gives the same four-part summary for every article, which is easy to read and easy to compare across articles.
Best Practices for Writing Prompts
1. Be specific. Replace "short" with "maximum 80 words" and "simple" with "Class 10 level".
2. Put the instruction first and the input last. Mark the input clearly (for example under a heading LABEL) so the model does not mix it with the instructions.
3. Use labelled sections such as ROLE, CONTEXT, CONSTRAINTS and OUTPUT FORMAT. They are easy for the model to follow and easy for a person to edit.
4. Say what to do, not only what to avoid. A positive instruction is clearer than a long list of prohibitions.
5. Give an example of the output when the format is complex. One filled example often works better than a long description.
6. Test with several inputs. A prompt that works on one label may fail on another. Try a healthy product, a very short label and a label with missing values.
7. Improve one layer at a time. Changing everything together hides which change helped.
8. Always check the facts. The model can make mistakes, so important answers (such as allergen warnings) must be verified against the original label.
Advantages and Limitations of Structured Prompts
Advantages
Limitations
More accurate and relevant answers
Longer prompts take more time to write
Consistent output across many inputs
Too many rules can confuse the model
Output can be used directly in an app
A fixed format may hide useful extra detail
Easy to reuse as a template
Prompts need re-testing when the model changes
Final Reflection
This exercise showed that the model was not the only thing improving the result: the prompt was. By moving from "Explain this food label" to a layered prompt with a role, context, constraints and format, the same model gave an answer that is expert, personalised, short, safe and structured. For my Food Decoder project, the final prompt can be saved as a template and reused for every scanned label, with only the label text replaced.

## Result
Five prompt structures, namely Basic, Role, Context, Constraint and Output Format, were designed and tested on a sample food label for the Food Decoder application. The Basic prompt gave a short and vague answer, while the Role prompt improved it by adding expert terms such as E621 and E150d. The Context prompt made the answer suit a teenager buying a snack, and the Constraint prompt kept it short, simple and limited to facts on the label. The Output Format prompt produced a fixed layout with a verdict, key facts, an additive table, an allergen line and a tip, which an app can display directly. Hence, the final prompt that combines role, context, constraints and output format gave the most accurate, consistent and reusable result.

