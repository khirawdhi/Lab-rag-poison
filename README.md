# RAG Data Poisoning Lab

A hands-on lab demonstrating how **Retrieval-Augmented Generation (RAG)** systems can be manipulated through **knowledge base poisoning**, and how trust-based retrieval controls mitigate the attack.

---

## What You'll Learn

- How RAG retrieves external documents
- How poisoned knowledge bases influence LLM responses
- Why retrieval is a critical trust boundary
- How trust filtering reduces data poisoning risks

---

## Scenario

An internal AI assistant retrieves documents from a knowledge base before answering employee questions.

A malicious document is added during ingestion, causing the assistant to recommend insecure actions (for example, bypassing MFA).

The language model itself is never compromised—the retrieved context is.

![RAG Data Poisoning Pipeline](room/img/RAG.png)

---

## What the Lab Demonstrates

1. Clean retrieval
2. Poisoned retrieval
3. Mitigated retrieval using trusted sources

The same prompt produces different answers based solely on the retrieved context.

---

## Mitigations

- Source allowlists
- Document provenance
- Segregated vector indexes
- Retrieval-time authorization
- Trust-based filtering

---

## Run the Lab

```bash
# Build a clean index
cd app
python3 ingest.py --kb ../kb --index ../index_clean.json

# Query
python3 query.py --index ../index_clean.json --q "How do I access VPN if MFA is failing?"

# Create a poisoned index
python3 ingest.py --kb ../kb --inject ../injected --index ../index_poisoned.json

# Query the poisoned index
python3 query.py --index ../index_poisoned.json --q "How do I access VPN if MFA is failing?"

# Query using trusted sources only
python3 query.py --index ../index_poisoned.json --q "How do I access VPN if MFA is failing?" --trusted-only
```

---

## Key Takeaways

- Retrieval is a security boundary.
- AI systems inherit the trustworthiness of their data.
- Data integrity is as important as model security.

---

## Disclaimer

This project is intended for educational and defensive security research only.

## License

MIT
