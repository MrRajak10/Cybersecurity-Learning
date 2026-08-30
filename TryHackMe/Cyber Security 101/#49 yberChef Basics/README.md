# CyberChef Basics — TryHackMe Learning Repository

CyberChef is a web-based toolkit for performing a wide range of data transformation, encoding, decoding, encryption, decryption, extraction, and formatting operations. It is often described as a **“Swiss Army knife for data”** because many security-related transformations can be performed quickly without writing custom scripts.

This repository documents the key concepts, workflow, exercises, mistakes, and lessons learned while completing the **CyberChef Basics** room in TryHackMe.

The goal is not simply to record answers. Instead, these notes focus on understanding **what CyberChef does, why a particular operation is appropriate, and how to develop the reasoning needed to use it effectively during security investigations.**

---

## Learning Objectives

By completing this room, you should be able to:

* Understand what CyberChef is and why security professionals use it.
* Navigate the CyberChef interface.
* Understand the relationship between **Operations, Recipes, Input, and Output**.
* Recognize common encoding and decoding formats.
* Work with operations such as:

  * Base64
  * Base58
  * Base85
  * URL encoding/decoding
  * Binary and decimal conversion
  * ROT13
  * Unix timestamps
  * IP, URL, domain, and email extraction
  * URL and IP defanging
* Build multi-step CyberChef recipes.
* Develop a logical workflow for analyzing unknown data.
* Understand why identifying the input format is often more important than randomly trying operations.
* Use CyberChef as a practical defensive-security investigation tool.

---

## What Is CyberChef?

CyberChef is a browser-based application developed by **GCHQ** that provides numerous operations for manipulating and analyzing data.

Instead of manually writing scripts for every small transformation, an analyst can use CyberChef to quickly perform tasks such as:

* Decode Base64 data.
* Encode or decode URLs.
* Convert between binary and decimal representations.
* Decode character encodings.
* Extract IP addresses from large text.
* Extract URLs, domains, or email addresses.
* Convert Unix timestamps.
* Apply common cryptographic transformations.
* Defang potentially dangerous URLs and IP addresses.
* Chain multiple transformations together.

CyberChef can also be downloaded and run locally, which can be useful when working with sensitive information or environments where sending data to an online service is undesirable.

---

## The CyberChef Interface

CyberChef can be understood through four major areas.

### 1. Operations

The **Operations** panel contains the available transformations that CyberChef can perform.

Operations are grouped into categories, making it easier to locate the appropriate functionality.

The search capability is particularly useful because CyberChef contains a large number of operations.

Examples include:

* `From Base64`
* `To Base64`
* `URL Decode`
* `URL Encode`
* `From Unix Timestamp`
* `Extract IP addresses`
* `Extract URLs`
* `Extract email addresses`
* `Defang URL`
* `Defang IP addresses`
* `ROT13`

A useful habit is to search for the operation rather than manually browsing the entire operation list.

---

### 2. Recipe

The **Recipe** panel is the heart of CyberChef.

A recipe is a sequence of operations that are executed in order.

For example:

```text
Operation 1 → Operation 2 → Operation 3 → Output
```

Suppose a piece of data requires:

1. Decimal-to-binary conversion.
2. Another transformation.
3. Final decoding.

Those operations can be placed in the recipe in exactly that order.

The order matters because CyberChef processes the data sequentially.

A recipe can therefore be thought of as a small data-processing pipeline.

---

### 3. Input

The **Input** panel contains the data that CyberChef will process.

Input can come from:

* Manually typed text.
* Pasted text.
* Imported files.
* Additional input tabs.

For investigation work, this makes CyberChef useful for both small strings and larger pieces of captured data.

---

### 4. Output

The **Output** panel displays the result of the recipe.

Depending on the operation, the result might be:

* Plain text.
* Encoded data.
* Decoded data.
* Extracted indicators.
* Converted numbers.
* Transformed URLs.
* Binary data.

CyberChef can also save the output or replace the current input with the generated output.

---

## The Correct CyberChef Mindset

One of the most important lessons from this room is that CyberChef is not primarily about randomly trying operations until something looks readable.

A better workflow is:

```text
Understand the Objective
        ↓
Examine the Input
        ↓
Identify the Likely Data Format
        ↓
Choose an Appropriate Operation
        ↓
Build the Recipe
        ↓
Inspect the Output
        ↓
Verify the Result
```

### Step 1 — Define the Objective

Before touching CyberChef, determine what you are trying to accomplish.

For example:

> “I found an encoded-looking string and need to determine what information it contains.”

This is much more useful than simply thinking:

> “I have some gibberish. Let me try everything.”

---

### Step 2 — Examine the Input

Look for characteristics that reveal what type of data you are dealing with.

Examples:

* Characters consisting primarily of `0` and `1` → potentially binary.
* A string resembling Base64 → investigate Base64.
* `%` followed by hexadecimal values → potentially URL encoding.
* A long decimal number representing a timestamp → potentially Unix time.
* A string containing email-like patterns → use an email extractor.
* Text containing IPv4 addresses → use an IP extractor.
* A suspicious URL → consider URL extraction or defanging.

Recognizing these patterns reduces unnecessary experimentation.

---

### Step 3 — Choose the Operation

Once the likely format is known, select the relevant operation.

For example:

```text
Base64-looking data → From Base64
URL with percent encoding → URL Decode
Unix timestamp → From Unix Timestamp
Binary number → From Binary
Text containing IP addresses → Extract IP addresses
```

---

### Step 4 — Verify the Output

Do not assume an output is correct simply because CyberChef produced something readable.

Ask:

* Does this match the objective?
* Does the output make contextual sense?
* Is the resulting format what I expected?
* Does another transformation need to be performed?

This verification step is important during real investigations.

---

## Important CyberChef Operations

### Base64

Base64 is an encoding mechanism commonly encountered in cybersecurity.

CyberChef can perform both directions:

```text
To Base64
From Base64
```

This makes it convenient to move between plaintext and Base64 representations.

Remember:

**Base64 is encoding, not encryption.**

It does not provide confidentiality.

---

### Base58 and Base85

CyberChef supports several other encoding formats, including Base58 and Base85.

These formats may appear in different applications and data-processing environments.

The important skill is recognizing that not every encoded-looking value is Base64.

---

### URL Encoding

URL encoding represents special characters using percent-encoded values.

For example:

```text
:
/
?
=
```

may appear as encoded hexadecimal representations.

CyberChef can reverse these transformations with:

```text
URL Decode
```

and create them with:

```text
URL Encode
```

This is especially useful while investigating web traffic and HTTP-related data.

---

### Binary and Decimal Conversion

CyberChef can convert between representations such as binary and decimal.

This is useful for understanding how data can be represented numerically rather than as normal text.

A key lesson is that the same underlying information can appear in completely different representations.

For example:

```text
Character
   ↓
Decimal
   ↓
Binary
```

CyberChef removes much of the tedious manual conversion work.

---

### ROT13

ROT13 is a Caesar-style substitution cipher that rotates alphabetic characters by 13 positions.

For example:

```text
A → N
B → O
C → P
```

Because the transformation is symmetric, applying ROT13 again reverses it.

ROT13 should not be considered secure encryption. It is a simple substitution mechanism frequently encountered in challenges, puzzles, and legacy contexts.

---

### Unix Timestamp

A Unix timestamp represents time as the number of seconds elapsed since:

```text
January 1, 1970 00:00:00 UTC
```

CyberChef can convert between Unix timestamps and human-readable date/time representations.

Useful operations include:

```text
From Unix Timestamp
To Unix Timestamp
```

This is particularly useful when investigating logs, forensic data, or application-generated timestamps.

---

## Extraction Operations

CyberChef is not limited to encoding and decoding.

Its extraction operations can identify useful indicators from larger text.

Examples include:

### Extract IP Addresses

Useful for quickly identifying IPv4 or IPv6 addresses inside logs, reports, or captured text.

### Extract Email Addresses

Useful for locating email indicators during investigations.

### Extract URLs

Useful for identifying web destinations embedded inside large datasets.

### Extract Domains

Useful when the investigation requires identifying domain names rather than complete URLs.

These operations can save significant time compared with manually searching through large amounts of text.

---

## Defanging

Cybersecurity reports frequently contain potentially dangerous indicators such as:

```text
IP addresses
URLs
Domains
```

Publishing these indicators in their normal form can make them accidentally clickable.

CyberChef provides operations such as:

```text
Defang URL
Defang IP Address
```

Defanging modifies indicators so they are less likely to be accidentally accessed.

For example, a URL may be represented using forms such as:

```text
hxxps://example[.]com
```

The exact output depends on the selected defanging options.

This is particularly relevant when writing:

* Incident reports
* Threat intelligence reports
* SOC documentation
* Malware analysis reports
* Security advisories

---

## Building Multi-Step Recipes

One of the most important concepts in CyberChef is that operations can be chained together.

For example:

```text
Input
  ↓
Operation A
  ↓
Operation B
  ↓
Operation C
  ↓
Output
```

A multi-operation recipe might look conceptually like:

```text
From Decimal
      ↓
To Binary
```

The output of the first operation becomes the input of the second.

This is useful when a single transformation is not enough to obtain the desired result.

---

## Common Mistake: Choosing the Wrong Operation

A major challenge when learning CyberChef is knowing what operation to use.

If the input format is unknown, it is tempting to try operations randomly.

This can produce:

* meaningless output
* corrupted-looking data
* unexpected symbols
* apparently random strings

The solution is not necessarily to keep trying operations indefinitely.

Instead, first investigate what the input probably represents.

For example:

```text
Unknown string
     ↓
Identify characteristics
     ↓
Determine likely encoding/format
     ↓
Choose targeted operation
```

This approach is significantly more efficient.

---

## A Practical Investigation Workflow

A beginner-friendly investigation process can be summarized as:

```text
1. Identify the goal.
2. Preserve the original input.
3. Inspect the structure of the data.
4. Form a hypothesis about its format.
5. Select the appropriate CyberChef operation.
6. Check the output.
7. Validate the result.
8. Add another operation only when necessary.
```

This mindset is more important than memorizing the complete CyberChef operation list.

---

## Lessons Learned

### 1. CyberChef reduces repetitive work

Many operations that would otherwise require small scripts or manual calculations can be completed quickly through CyberChef.

### 2. Understanding data formats is essential

CyberChef does not automatically know what your data means.

The analyst still needs to identify whether the input is:

* Encoded
* Encrypted
* Hashed
* Compressed
* Formatted
* Structured
* Plain text

### 3. Encoding is not encryption

Base64, URL encoding, binary representation, and similar techniques should not be confused with secure encryption.

### 4. Recipes are pipelines

A recipe is simply a sequence of transformations applied in a controlled order.

### 5. Context matters

The same string may look meaningless until you understand where it came from and what kind of data it represents.

### 6. Automation does not replace reasoning

CyberChef makes transformations easier, but the analyst still needs to decide:

> “What am I looking at, and what should I do with it?”

---

## Beginner Practice Exercises

### Exercise 1 — Identify the Format

Take several strings represented in:

* Base64
* Binary
* URL encoding
* ROT13

Before using CyberChef, predict which operation should be used.

Then verify your prediction.

---

### Exercise 2 — Extract Indicators

Create a text file containing:

* Several IPv4 addresses.
* Multiple URLs.
* A few email addresses.
* Several ordinary sentences.

Use CyberChef to extract each indicator type.

---

### Exercise 3 — Build a Two-Step Recipe

Create a simple recipe that uses two transformations in sequence.

Before running it, write down what you expect each stage to produce.

Then compare your prediction with CyberChef's output.

---

### Exercise 4 — Timestamp Analysis

Collect several Unix timestamps from sample logs.

Convert them into human-readable timestamps with CyberChef.

Then reverse the process using the appropriate operation.

---

### Exercise 5 — Defanging

Create a small list of fictional malicious-looking URLs and IP addresses.

Use CyberChef to defang them for use in a security report.

Then inspect which parts of the indicator were modified.

---

## Key Takeaways

CyberChef is most valuable when combined with good analytical reasoning.

The important skill is not memorizing hundreds of operations.

It is learning how to answer these questions:

```text
What is my objective?
        ↓
What type of data am I looking at?
        ↓
Which operation matches that data?
        ↓
Do I need one operation or several?
        ↓
Does the final output make sense?
```

Once this thought process becomes familiar, CyberChef becomes a powerful companion for defensive security, threat intelligence, digital forensics, incident response, malware analysis, and general security investigations.

---

## Room Completion Reflection

Completing this room demonstrates an important progression in cybersecurity learning:

At first, a string of unfamiliar characters can appear completely meaningless.

After learning to identify common data representations, the same string becomes something that can be classified, transformed, and investigated.

That shift—from **“I don't know what this is”** to **“I can form a hypothesis and test it”**—is one of the most valuable skills developed through practical cybersecurity training.

---

## Repository Structure

```text
CyberChef-Basics/
├── README.md
└── notes.md
```

This repository is intended to serve as a learning reference while continuing the broader TryHackMe cybersecurity training journey.
