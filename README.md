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
# Prompt Design Using Different Prompt Structures


## 1. Objective

To design prompts using five different prompt structures (Basic, Role, Context, Constraint and Output Format) and to show how each structure improves the response, ending in one final combined prompt.

**Application chosen:** Food label decoding, the core feature of my project *Food Decoder*. The AI receives the ingredient list and nutrition facts printed on a packaged food item and explains them to an ordinary shopper.

**Test input used in every stage** (a sample label written for this exercise):

```
Product: Instant masala noodles (1 pack, 70 g)
Ingredients: Wheat flour, palm oil, salt, flavour enhancer (E621, E627),
sugar, acidity regulator (E501), colour (E150d), maltodextrin, onion powder.
Contains: Wheat.
Nutrition per 100 g: Energy 450 kcal, Total fat 18 g (Saturated fat 8.5 g),
Sugar 3 g, Sodium 1,850 mg.
```

---

## 2. Introduction to Prompt Engineering

**Prompt:** A prompt is the input text given to an AI language model to tell it what to do. The quality of the answer depends heavily on the quality of the prompt.

**Prompt engineering:** The practice of designing, testing and improving prompts so that the model gives accurate, useful and consistent output. It changes only the instruction, not the model.

**Why prompt structure matters:**

- A vague prompt forces the model to guess the audience, length, depth and format.
- A structured prompt removes those guesses, so quality stays similar every time.
- Prompts used inside an application must be reliable, because many users depend on them.

---

## 3. Definitions of the Five Prompt Structures

| Structure | Definition | What it controls |
| --- | --- | --- |
| Basic | A short, direct instruction with only the task and input | The task only |
| Role | Assigns the model a profession or persona to answer from | Expertise, vocabulary, viewpoint |
| Context | Gives background about the user, situation, purpose and audience | Relevance and personalisation |
| Constraint | Sets limits and rules such as length, language level, tone and things to avoid | Length, tone, safety, scope |
| Output Format | Fixes the exact layout of the answer (table, bullets, JSON) | Structure and machine-readability |

**General formula:**

```
Final Prompt = Role + Context + Task + Constraints + Output Format + Input
```

---

## 4. Stage 1: Basic Prompt

**Prompt:**

```
Explain this food label.
[label text]
```

**Sample output (illustrative):**

> This is a pack of instant noodles. It has wheat flour, oil, salt and some additives. It is high in sodium and fat, so it should not be eaten too often.

**Observation:** Correct but vague. It does not explain E621 or E150d, does not compare sodium with a daily limit, and has no structure.

---

## 5. Stage 2: Role Prompt

**Prompt:**

```
You are a certified food scientist and nutritionist.
Explain this food label.
[label text]
```

**Sample output (illustrative):**

> As a food scientist, I can see three points of concern. E621 (monosodium glutamate) and E627 (disodium guanylate) are flavour enhancers that make the product taste richer. E150d is a caramel colour used only for appearance. Sodium at 1,850 mg per 100 g is very high, and palm oil adds saturated fat.

**Observation:** Uses correct technical terms and explains what each additive does, but it is unstructured and may be too technical for a normal shopper.

---

## 6. Stage 3: Context Prompt

**Prompt:**

```
You are a certified food scientist and nutritionist.

Context: I am building a mobile app called Food Decoder for Indian
shoppers. Users scan the label of a packaged food item in a shop and
want to know quickly whether it is a healthy choice. Most users are
not familiar with E-numbers or nutrition terms. The product will be
eaten by a school-going teenager as a snack.

Explain this food label.
[label text]
```

**Sample output (illustrative):**

> For a teenager's snack, this pack is not a good everyday choice. One pack has about 1,300 mg of sodium, which is more than half of the daily limit usually advised for adults. The flavour enhancers (E621, E627) are permitted but are a sign of a highly processed product. The wheat in it is an allergen to note if the teenager is sensitive to gluten.

**Observation:** Personalised to the audience and situation, and gives a decision instead of only a description. It is still long and uncontrolled.

---

## 7. Stage 4: Constraint Prompt

**Prompt:**

```
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
```

**Sample output (illustrative):**

> This noodle pack is high in salt: one pack has about 1,300 mg sodium, over half of an adult's daily limit. It also has 18 g fat per 100 g, partly from palm oil. E621 and E627 are flavour boosters, and E150d is a brown colour. It contains wheat. It is fine as an occasional snack, but not for daily eating.

**Observation:** Short, readable and limited to label facts. It is still a paragraph, so an app cannot easily show it in separate parts.

---

## 8. Stage 5: Output Format Prompt

**Prompt (added on top of Stage 4):**

```
Return the answer in exactly this format:

Verdict: <Good / Okay sometimes / Limit>
Key facts: 3 bullet points
Additives: a table with columns Code | Name | Purpose
Allergens: one line
Tip: one short sentence
```

**Sample output (illustrative):**

```
Verdict: Limit

Key facts:
- Sodium is about 1,300 mg per pack, over half of an adult's daily limit.
- Fat is 18 g per 100 g, with 8.5 g saturated.
- Sugar is low at 3 g per 100 g.

Additives:
| Code  | Name                     | Purpose           |
| E621  | Monosodium glutamate     | Flavour enhancer  |
| E627  | Disodium guanylate       | Flavour enhancer  |
| E501  | Potassium carbonates     | Acidity regulator |
| E150d | Sulphite ammonia caramel | Colour            |

Allergens: Contains wheat (gluten).
Tip: Add vegetables and skip half the seasoning packet.
```

**Observation:** Scannable and predictable. Every scan gives the same fields in the same order, which suits a mobile app screen or a database.

---

## 9. Final Prompt (All Structures Combined)

```
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
```

---

## 10. Comparison of All Stages

| Stage | Structure | What it adds | Weakness left |
| --- | --- | --- | --- |
| 1 | Basic | A simple answer | Vague, no depth |
| 2 | Role | Expert vocabulary and additive knowledge | Too technical, no structure |
| 3 | Context | Fits the audience and situation | Long, uncontrolled style |
| 4 | Constraint | Short, simple, safe, label-only facts | Free-text paragraph |
| 5 | Output Format | Fixed, scannable, app-ready layout | None for this use case |

---

## 11. Second Application: Text Summarization

| Stage | Prompt |
| --- | --- |
| 1. Basic | Summarize this article. |
| 2. Role | You are a professional news editor. Summarize this article. |
| 3. Context | You are a professional news editor. The summary will be read by college students who have two minutes between classes and want to know what happened and why it matters. Summarize this article. |
| 4. Constraint | (Stage 3) Maximum 60 words. Use simple English. Do not add information that is not in the article. Do not give your opinion. |
| 5. Output Format | (Stage 4) Return: Headline (max 10 words), 3 bullet points, and one line titled "Why it matters". |

---

## 12. Best Practices

1. Be specific: replace "short" with "maximum 80 words".
2. Put the instruction first and the input last, clearly marked.
3. Use labelled sections such as ROLE, CONTEXT, CONSTRAINTS and OUTPUT FORMAT.
4. Say what to do, not only what to avoid.
5. Give an example of the output when the format is complex.
6. Test with several inputs, not just one.
7. Improve one layer at a time.
8. Always verify important facts, such as allergen warnings, against the original label.

---

## 13. Result

Five prompt structures, namely Basic, Role, Context, Constraint and Output Format, were designed and tested on a sample food label for the Food Decoder application. The Basic prompt gave a short and vague answer, while the Role prompt improved it by adding expert terms such as E621 and E150d. The Context prompt made the answer suit a teenager buying a snack, and the Constraint prompt kept it short, simple and limited to facts on the label. The Output Format prompt produced a fixed layout with a verdict, key facts, an additive table, an allergen line and a tip, which an app can display directly. Hence, the final prompt that combines role, context, constraints and output format gave the most accurate, consistent and reusable result.

## 14. Conclusion

A basic prompt leaves the model to guess the expertise, the reader, the limits and the layout. Adding a role, context, constraints and an output format one by one turned a vague two-line answer into a short, reliable, structured response that suits the Food Decoder app. A good prompt is built in layers, and each layer should be tested against the same input to see what it really improves.

