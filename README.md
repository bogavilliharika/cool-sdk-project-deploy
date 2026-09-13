# CooL SDK Project

## Problem Statement

AI-powered applications can produce decisions, actions, and outputs that users may find difficult to verify or trust. Simply displaying an AI-generated result does not provide enough evidence to determine whether the underlying information or execution has been changed.

This project explores a verifiable evidence workflow for AI executions. The goal is to create evidence records that allow important execution information to be checked later while keeping sensitive payload information represented through a cryptographic commitment rather than directly exposing it as the evidence record.

---

## What I Built

**CooL SDK Project** is a browser-based prototype that demonstrates a verifiable evidence console for AI executions.

The prototype allows users to:

* Record an AI execution or application event.
* Enter software/model identity, event type, target, actor, and action information.
* Provide a private payload.
* Generate a **SHA-256 cryptographic commitment** for the recorded information.
* Create an evidence receipt containing the execution metadata and commitment.
* View evidence records created during the browser session.
* Verify a receipt independently against its stored commitment.
* Detect tampering when a recorded field is changed.
* Demonstrate signature, transparency-log, and TEE components through explicit prototype adapters.

The prototype provides five main areas:

1. **Evidence Overview** – View evidence records, verification status, commitments, and detected alterations.
2. **Record Execution** – Create a new AI execution evidence receipt.
3. **Evidence Records** – View recorded evidence from the current browser session.
4. **Verify Receipt** – Check whether a receipt matches its SHA-256 commitment.
5. **Tamper Check** – Modify a recorded field and demonstrate that the resulting commitment no longer matches.

---

## How CooL SDK Is Used

CooL is used as the conceptual foundation for the evidence and verification workflow demonstrated by this prototype.

The prototype models the CooL evidence workflow around an AI application execution:

**AI Application → Evidence Record → Cryptographic Commitment → Verification / Evidence Adapters → Independent Verification**

The current prototype implementation is intentionally lightweight and browser-based. The SHA-256 commitment is generated using the browser's Web Crypto API.

The prototype also contains explicit adapters representing:

* **Ed25519 signatures**
* **ML-DSA-65 signatures**
* **RFC 6962-style transparency-log inclusion**
* **TEE attestation using dstack / Intel TDX metadata**

These components are represented as prototype adapters rather than production cryptographic or infrastructure integrations. This makes the prototype useful for demonstrating the intended CooL evidence workflow while keeping the implementation simple and easy to run.

---

## Why CooL Is Important

Trust is important for applications that use AI to make decisions, perform actions, or generate information.

A normal application can show an AI result, but users may still have difficulty determining:

* What execution produced the result.
* Whether important execution information was changed.
* Whether the evidence corresponds to the original data.
* Whether the recorded evidence can be independently verified.

CooL is important to this solution because it provides the foundation for treating **verifiable evidence as part of the product workflow** rather than simply displaying information.

In this prototype, the evidence workflow demonstrates how an execution can be represented by a cryptographic commitment and later checked for integrity. This provides a clearer path toward transparent and independently verifiable AI application behavior.

---

## Features

### 1. AI Execution Recording

Users can record an execution by providing:

* Software / model identity
* Event type
* Tool / target
* Actor
* Action metadata
* Private payload

### 2. SHA-256 Commitment

The prototype creates a SHA-256 commitment from the recorded execution information.

The commitment allows the integrity of the recorded fields to be checked without requiring the evidence interface to expose the payload as ordinary evidence data.

### 3. Evidence Receipt

A structured JSON evidence receipt is generated containing information such as:

* Event ID
* Timestamp
* Software / model
* Event type
* Target
* Actor
* Action
* SHA-256 payload commitment
* Signature adapter information
* Transparency adapter information
* TEE attestation adapter information

### 4. Independent Verification

A receipt can be pasted into the verification interface and checked against its stored SHA-256 commitment.

If the recorded fields reproduce the expected commitment, the receipt is reported as verified.

If a field has been changed, the commitment no longer matches and the receipt is reported as tampered or invalid.

### 5. Tamper Detection

The Tamper Check feature allows a recorded action to be changed deliberately.

The prototype calculates a new SHA-256 commitment and compares it with the original commitment. A mismatch demonstrates how an alteration can be detected.

---

## How to Run the Project

### Prerequisites

You only need:

* A modern web browser such as Google Chrome, Microsoft Edge, or Firefox.
* Git, if you want to clone the repository.

No backend server or database is required for the current prototype.

### Option 1: Clone and Open Directly

Clone the repository:

```bash
git clone https://github.com/bogavilliharika/cool-sdk-project.git
```

Move into the project directory:

```bash
cd cool-sdk-project
```

Open the prototype HTML file in a modern web browser.

### Option 2: Download the Repository

1. Download or clone the repository from GitHub.
2. Locate the prototype HTML file.
3. Open the HTML file in a modern web browser.
4. The CooL Evidence Console will load locally.

### Testing the Prototype

After opening the application:

1. Go to **Record Execution**.
2. Enter or modify the execution information.
3. Click **Create Evidence Receipt**.
4. A SHA-256 commitment and evidence receipt will be generated.
5. Open **Verify Receipt**.
6. Load or paste the generated receipt.
7. Click **Verify Receipt**.
8. The verification result should show whether the commitment matches.
9. Open **Tamper Check**.
10. Change the recorded action.
11. Run the tamper check.
12. The prototype should report **TAMPERING DETECTED** because the modified information produces a different SHA-256 commitment.

---

## Architecture / Workflow

The prototype follows a lightweight evidence-generation and verification architecture.

### High-Level Workflow

```text
AI Application
      │
      ▼
Execution / Event Data
      │
      ▼
CooL Evidence Workflow
      │
      ├── SHA-256 Commitment
      │
      ├── Signature Adapter
      │
      ├── Transparency Log Adapter
      │
      └── TEE Attestation Adapter
      │
      ▼
Evidence Receipt
      │
      ▼
Independent Verification
      │
      ▼
Verified / Tampered
```

### Workflow Steps

1. **AI Application / Execution**

   * An AI-related execution or application event is represented.

2. **Evidence Recording**

   * Execution metadata and a private payload are entered into the prototype.

3. **Cryptographic Commitment**

   * The prototype generates a SHA-256 commitment from the execution information.

4. **Evidence Receipt**

   * The commitment and relevant metadata are stored in a structured evidence receipt.

5. **Evidence Adapters**

   * Signature, transparency-log, and TEE components are represented through prototype adapters.

6. **Independent Verification**

   * The receipt can be checked later to determine whether the recorded fields reproduce the original commitment.

7. **Tamper Detection**

   * If the recorded information is modified, the newly calculated commitment differs from the original commitment.

---

## Technical Decisions

### Lightweight HTML-Based Implementation

The prototype is implemented as a lightweight HTML, CSS, and JavaScript application.

This was chosen so that the product can be demonstrated easily without requiring a backend service or complex installation process.

### Browser-Based Cryptography

The prototype uses the browser's Web Crypto API to generate SHA-256 commitments.

This provides a real cryptographic commitment mechanism while keeping the prototype simple and self-contained.

### Evidence Instead of Plaintext Payload Storage

The prototype uses a cryptographic commitment to represent the integrity of the private payload instead of relying only on displaying the payload as evidence.

This demonstrates the concept of verifying that information has not changed without making the payload itself the primary evidence artifact.

### Adapter-Based Architecture

The signature, transparency-log, and TEE components are represented as explicit prototype adapters.

This keeps the prototype focused on validating the product workflow while leaving room for integration with real cryptographic and infrastructure services in a future implementation.

### Browser Session Storage

Evidence records are maintained using browser local storage for the prototype.

This avoids requiring a database while allowing multiple evidence records to be created and inspected during the demonstration.

---

## Limitations

The current project is a **prototype** and is not intended to be a production-ready evidence infrastructure.

Current limitations include:

* The application is browser-based and uses local browser storage.
* The SHA-256 commitment is implemented using the browser's Web Crypto API.
* Ed25519 signatures are represented through a prototype adapter rather than a production signing service.
* ML-DSA-65 signatures are represented through a prototype adapter.
* RFC 6962-style transparency-log inclusion is represented through a prototype adapter.
* TEE attestation is represented through prototype metadata rather than a live TEE attestation environment.
* There is no production backend, distributed evidence database, or deployed transparency log.
* The current prototype does not provide production-grade authentication, authorization, key management, or access control.
* The prototype has been designed primarily to demonstrate and validate the product workflow.

---

## Future Improvements

Future versions of the project could include:

* Integrating the production CooL SDK and its supported APIs directly into the application.
* Replacing prototype adapters with real Ed25519 and ML-DSA-65 signing infrastructure.
* Connecting the application to a real transparency log.
* Integrating real TEE attestation and verification.
* Adding secure backend storage for evidence records.
* Adding authentication and role-based access control.
* Improving key management and secure credential handling.
* Adding automated unit, integration, and security testing.
* Improving the user interface and overall user experience.
* Providing richer evidence and verification information.
* Adding monitoring and audit capabilities.
* Deploying the application as an online service.
* Expanding the prototype into a production-ready verifiable evidence platform.

---

## Project Status

**Status: Prototype / Proof of Concept**

The current implementation is designed to demonstrate the CooL-oriented evidence workflow, cryptographic commitment verification, evidence receipts, and tamper detection in a simple browser-based environment.

---

## Repository

GitHub repository:

https://github.com/bogavilliharika/cool-sdk-project
