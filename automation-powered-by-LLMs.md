# Examples of Automation Scripts and Tools Powered by LLMs

## 1. Automated Code Review and Vulnerability Detection

Large Language Models (LLMs) can automate source code reviews by identifying common security vulnerabilities, explaining associated risks, and recommending secure coding practices. Unlike traditional rule-based scanners, LLMs understand the context and intent of the code, enabling more intelligent security analysis.

Common vulnerabilities that LLMs can help identify include:

- SQL Injection (SQLi)
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Command Injection
- Path Traversal
- Server-Side Request Forgery (SSRF)
- Insecure Deserialization
- Hardcoded Credentials
- Weak Cryptography
- Insecure API Usage

---

# Introduction

In this example, a GPT-2 model is used to analyze source code for potential security vulnerabilities.

The workflow consists of the following steps:

1. Accept a source code snippet as input.
2. Tokenize the code using the Hugging Face tokenizer.
3. Process the input through the GPT-2 language model.
4. Analyze the generated output for indicators of insecure coding patterns.
5. Generate security findings and remediation recommendations.

> **Note**
>
> GPT-2 is used here for educational purposes. Modern code-focused LLMs such as GPT-4, Code Llama, StarCoder, DeepSeek-Coder, or fine-tuned security models provide significantly better accuracy for vulnerability detection.

---

# Example 1 – SQL Injection Detection

## Overview

SQL Injection (SQLi) is one of the most common web application vulnerabilities. It occurs when user-controlled input is directly incorporated into SQL queries without proper validation or parameterization, allowing attackers to manipulate database queries.

---

## Example Script

```python
from transformers import GPT2Tokenizer, GPT2LMHeadModel

# Load tokenizer and model
tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
model = GPT2LMHeadModel.from_pretrained("gpt2")

# GPT-2 does not define a padding token by default
tokenizer.pad_token = tokenizer.eos_token


def analyze_code(code):
    """
    Analyze source code for potential security vulnerabilities.

    Args:
        code (str): Source code to analyze.

    Returns:
        str: Model-generated analysis.
    """

    inputs = tokenizer(
        code,
        return_tensors="pt",
        padding=True,
        truncation=True
    )

    outputs = model.generate(
        inputs["input_ids"],
        attention_mask=inputs["attention_mask"],
        max_length=200,
        num_return_sequences=1,
        early_stopping=True
    )

    return tokenizer.decode(outputs[0], skip_special_tokens=True)


code_sample = """
user_id = input()

query = "SELECT * FROM users WHERE id = " + user_id

db.execute(query)
"""

print("SQL Injection Analysis")
print("----------------------")
print(analyze_code(code_sample))
```

---

# How the Script Works

### 1. Model Initialization

The script loads the GPT-2 tokenizer and language model using the Hugging Face Transformers library.

```python
tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
model = GPT2LMHeadModel.from_pretrained("gpt2")
```

---

### 2. Code Tokenization

The input source code is converted into tokens that the language model can understand.

```python
inputs = tokenizer(
    code,
    return_tensors="pt",
    padding=True,
    truncation=True
)
```

---

### 3. Code Analysis

The tokenized code is passed through the language model to generate a security assessment.

```python
outputs = model.generate(...)
```

---

### 4. Output Generation

The generated tokens are converted back into readable text.

```python
tokenizer.decode(outputs[0], skip_special_tokens=True)
```

---

# Vulnerable Code Example

```python
user_id = input()

query = "SELECT * FROM users WHERE id = " + user_id

db.execute(query)
```

### Why It Is Vulnerable

The SQL query is constructed using string concatenation.

An attacker could provide malicious input such as:

```sql
1 OR 1=1
```

which would produce:

```sql
SELECT * FROM users WHERE id = 1 OR 1=1
```

This may allow unauthorized access to database records.

---

# Expected Output

```text
SQL Injection Analysis

Potential SQL Injection vulnerability detected.

The SQL query is constructed using direct string concatenation with
user-controlled input. This may allow attackers to manipulate the query
and execute arbitrary SQL commands.

Recommendation:
• Use parameterized queries.
• Validate user input.
• Apply the principle of least privilege for database accounts.
```

---

# Secure Implementation

Instead of concatenating user input into SQL statements:

```python
query = "SELECT * FROM users WHERE id = " + user_id
```

use parameterized queries:

```python
query = "SELECT * FROM users WHERE id = ?"

cursor.execute(query, (user_id,))
```

For PostgreSQL:

```python
cursor.execute(
    "SELECT * FROM users WHERE id = %s",
    (user_id,)
)
```

---

# Security Recommendations

When SQL Injection is detected, the LLM can recommend:

- Parameterized queries
- Prepared statements
- Input validation
- Stored procedures (where appropriate)
- ORM frameworks
- Database least-privilege access
- Error message sanitization
- Web Application Firewall (WAF) protection

---

# Enterprise Use Cases

This automation can be integrated into various stages of the Secure Software Development Lifecycle (SSDLC), including:

- Pull Request (PR) reviews
- GitHub Actions
- GitLab CI/CD pipelines
- Azure DevOps Pipelines
- Jenkins security gates
- Secure code review workflows
- IDE extensions
- Developer security assistants

Security teams can use LLMs to:

- Detect insecure coding patterns
- Reduce manual code review effort
- Explain vulnerabilities to developers
- Recommend secure code fixes
- Prioritize findings based on risk
- Improve secure coding practices across development teams

---

# Limitations

Although LLMs significantly enhance automated code reviews, they should complement—not replace—traditional application security testing tools.

Best results are achieved by combining LLMs with:

- Static Application Security Testing (SAST)
- Dynamic Application Security Testing (DAST)
- Software Composition Analysis (SCA)
- Infrastructure-as-Code (IaC) scanning
- Secrets scanning
- Manual security reviews
- Penetration testing

This layered approach improves detection accuracy, reduces false positives, and strengthens overall software security.
