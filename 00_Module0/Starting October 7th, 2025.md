
## 1️ What is *Continued Pre-Training* (CPT)?

### Pre-training (original)

* Model is trained on **massive, generic data**
* Happens once (or rarely)
* Extremely expensive (GPUs, time, scale)

This is how:

* GPT
* Claude
* LLaMA
* Nova
  are originally created.

---

### Continued Pre-Training (CPT)

CPT means:

> **Taking an already pre-trained foundation model and further training it on additional data**.

Key characteristics:

* Training still happens on **model weights**
* Not just prompting
* Not just embeddings
* Not just instruction tuning

Think of CPT as:

> “Extending the model’s *core knowledge* with new data”

Examples:

* Adding domain-specific language
* Teaching the model a company’s terminology
* Improving reasoning in a niche domain

 CPT is **deep, heavy, and risky** compared to lighter techniques.

---

## 2️ What AWS Is Saying (Very Precisely)

> **Starting October 7th, 2025, you will no longer be able to access Continued pre-training in Bedrock.**

This means:

* Bedrock will **no longer support CPT**
* The feature is being **removed**, not deprecated lightly
* This is a **deliberate architectural decision**

But…

> **You can continue to use continued pre-training for Amazon Nova models on Amazon SageMaker.**

So CPT is **not going away**.
It’s being **relocated**.

---

## 3️ Why AWS Is Doing This (Critical Insight)

This is where your **cloud + GenAI maturity** helps.

### Bedrock philosophy

Bedrock is designed for:

* API-based consumption
* Serverless usage
* Fast experimentation
* Enterprise safety
* Governance & guardrails

Bedrock is **NOT** designed for:

* Long-running training jobs
* Heavy GPU orchestration
* Low-level training control
* Custom training pipelines

 CPT **does not fit** Bedrock’s abstraction level.

---

### SageMaker philosophy

SageMaker is designed for:

* Full ML lifecycle
* Training jobs
* Fine-tuning
* Data pipelines
* Experiment tracking
* Custom hyperparameters
* GPU/accelerator control

 CPT fits **perfectly** in SageMaker.

So AWS is doing the **right architectural separation**.

---

## 4️ The Clean Mental Model (Lock This In)

Think like this:

| Capability             | Bedrock            | SageMaker |
| ---------------------- | ------------------ | --------- |
| Prompting              |   YES                | YES         |
| Inference              | YES                   |YES          |
| Model selection        | YES                   | NO         |
| Serverless GenAI apps  | YES                   | NO         |
| Guardrails             | YES                   | NO         |
| Fine-tuning (light)    | YES  (limited)        | YES         |
| Continued pre-training | NO (after Oct 2025) | YES         |
| Full training control  | NO                  | YES         |

 **Bedrock = consumption layer**
 **SageMaker = training & customization layer**

---

## 5️ Why Only Amazon Nova Models?

Notice something subtle:

> CPT is supported **only for Amazon Nova models** on SageMaker.

Why?

Because:

* AWS owns Nova
* AWS controls the training pipeline
* AWS can safely expose weight-level training
* Third-party models (Claude, LLaMA) have IP restrictions

So CPT:

* Is **not allowed** for external models
* Is **safe only where AWS owns the model**

This is both **legal** and **technical reality**.

---

## 6️ What This Means for You (As a Learner)

Very important takeaway:

* **Do NOT associate Bedrock with model training**
* **Do NOT think Bedrock = SageMaker**
* Bedrock is about **using models**
* SageMaker is about **changing models**

If your goal is:

* Chatbots
* RAG
* Agents
* Copilots
* Enterprise apps
  → **Bedrock**

If your goal is:

* Model customization at weight level
* Domain-specific learning
* Training pipelines
  → **SageMaker**

---

## 7️ One-Line Summary (Your Notes Version)

> AWS is removing Continued Pre-Training from Bedrock because Bedrock is an inference-first, serverless GenAI platform, while heavy model customization like CPT belongs to SageMaker’s full ML training ecosystem.

This is **architecture maturity**, not feature removal.

---


