# CooL SDK Project
##Problem Statement

AI-powered applications can produce decisions, actions, and outputs that
are difficult to verify or trust. Simply displaying an AI-generated
result does not provide enough evidence to determine whether the
underlying execution or information has been changed.

CooL explores a verifiable evidence workflow for AI executions by
creating evidence records that can be checked later while representing
sensitive payloads through cryptographic commitments.

##What I Built

CooL SDK Project is a browser-based prototype of a verifiable
evidence console for AI executions.

The prototype allows users to:

Record an AI execution or application event.

Enter software/model identity, event type, target, actor, and action
information.

Provide a private payload.

Generate a SHA-256 cryptographic commitment.

Create a structured JSON evidence receipt.

View evidence records created in the browser.

Verify evidence against its stored commitment.

Detect changes to recorded information.

Explore future signature, transparency-log, and TEE integrations
through prototype adapters.

The prototype includes five main areas:

Evidence Overview -- View evidence records, commitments,
verification status, and detected alterations.

Record Execution -- Create a new AI execution evidence record.

Evidence Records -- Inspect records created during the current
browser session.

Verify Receipt -- Check whether a receipt matches its SHA-256
commitment.

Tamper Check -- Modify a recorded field and observe how the
commitment changes.

##How CooL SDK Is Used

CooL provides the conceptual foundation for recording and verifying
evidence generated during an AI application execution.

#The workflow is:

AI Application
      │
      ▼
Execution / Event Data
      │
      ▼
CooL Evidence Record
      │
      ▼
SHA-256 Cryptographic Commitment
      │
      ▼
JSON Evidence Receipt
      │
      ▼
Verification / Tamper Check

The current prototype is lightweight and browser-based. SHA-256
commitments are generated using the browser's Web Crypto API.

#The receipt structure also includes prototype adapters for:

Ed25519 signatures

ML-DSA-65 signatures

RFC 6962-style transparency-log inclusion

TEE attestation using dstack / Intel TDX metadata

These adapters represent planned integration points and are not
production cryptographic or infrastructure services.

#Why CooL Is Important

AI systems are increasingly used to make decisions, perform actions, and
generate important information. Users and organizations need better ways
to understand and verify what happened during these executions.

CooL demonstrates how evidence can help answer questions such as:

What execution produced a result?

Which model, software, or actor was involved?

What action was performed?

Has the recorded information changed?

Can the evidence be checked later?

The project focuses on making verifiable evidence part of the AI
application workflow, rather than treating logging as an afterthought.

##Features

1. AI Execution Recording

Users can record:

Software/model identity

Event type

Tool or target

Actor

Action metadata

Private payload

2. SHA-256 Commitment

The prototype generates a SHA-256 commitment from the recorded execution
information.

This commitment can be recalculated later to check whether the recorded
information has changed.

3. JSON Evidence Receipt

Each evidence record can include:

Event ID

Timestamp

Software/model identity

Event type

Target

Actor

Action

SHA-256 commitment

Signature adapter information

Transparency adapter information

TEE attestation adapter information

4. Receipt Verification

Users can load or paste a receipt into the verification interface.

The prototype compares the calculated commitment with the stored
commitment and reports whether the values match.

5. Tamper Detection

The Tamper Check feature deliberately changes a recorded field, such as
the action metadata.

The prototype then generates a new commitment and compares it with the
original. A mismatch demonstrates that the recorded information has
changed.

##How to Run the Project

Prerequisites

You need:

A modern web browser such as Google Chrome, Microsoft Edge, or
Firefox.

The CooL prototype HTML file.

Git only if you want to clone the repository.

No backend server or database is required for the current prototype.

Option 1: Clone the Repository

git clone https://github.com/bogavilliharika/cool-sdk-project.git
cd cool-sdk-project

Open the prototype HTML file in a modern browser.

Option 2: Open the HTML File Directly

Download the project files.

Locate the CooL prototype HTML file.

Open it in a modern web browser.

The CooL Evidence Console will load locally.

Testing the Prototype

Open Record Execution.

Enter the execution information.

Create an evidence receipt.

Open Evidence Records to inspect the record.

Open Verify Receipt and load the receipt.

Run the verification process.

Open Tamper Check.

Modify the recorded action.

Run the tamper check.

Confirm that the modified commitment differs from the original.

##Architecture / Workflow

┌──────────────────────────────┐
│       AI Application         │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Execution / Event Data  │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       CooL Evidence Flow     │
├──────────────────────────────┤
│ SHA-256 Commitment           │
│ Signature Adapter            │
│ Transparency Log Adapter     │
│ TEE Attestation Adapter      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      JSON Evidence Receipt   │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    Verification / Tamper     │
│           Check              │
└──────────────────────────────┘

Workflow Steps

Represent an AI execution
An AI-related action or application event is recorded.

Capture evidence information
The user enters execution metadata and a private payload.

Generate a commitment
CooL creates a SHA-256 commitment from the recorded information.

Create an evidence receipt
The commitment and relevant metadata are placed into a structured
JSON receipt.

Inspect or export evidence
Users can view, copy, import, or export receipts.

Verify the evidence
The commitment is recalculated and compared with the stored value.

Check for tampering
A modified field produces a different commitment, demonstrating
detectable alteration.

#Technical Decisions

Lightweight HTML, CSS, and JavaScript

The prototype is implemented as a self-contained browser application.

This makes it easy to:

Run locally

Demonstrate the concept

Inspect the implementation

Share the prototype

Avoid backend setup

Browser-Based Cryptography

The prototype uses the browser's Web Crypto API to generate SHA-256
commitments.

This provides a real hashing mechanism without requiring an external
cryptography service.

Cryptographic Commitments

The project uses commitments to represent the integrity of recorded
information instead of relying only on displaying raw payload data.

Adapter-Based Design

Signature, transparency-log, and TEE capabilities are represented
through explicit prototype adapters. This keeps the current
implementation simple while providing clear extension points for future
integrations.

Browser Storage

Evidence records are maintained using browser storage for the prototype.
This avoids requiring a database during demonstrations.

##Limitations

The current implementation is browser-based and uses local storage.

Signature, transparency-log, and TEE features are represented by
prototype adapters.

There is no production backend, authentication system, or deployed
evidence infrastructure.

The prototype demonstrates evidence integrity and tamper detection;
it does not prove that an AI output is correct, safe, or fair.

##Future Improvements

Future versions could include:

Real Ed25519 and ML-DSA-65 signing.

Integration with a transparency log.

Live TEE attestation and verification.

Secure backend evidence storage.

Authentication and role-based access control.

Improved key management.

Automated testing.

Richer evidence and verification reports.

Monitoring and audit capabilities.

Deployment as an online service.

Integration with the production CooL SDK.

Project Status

Status: Prototype / Proof of Concept

The current project demonstrates the CooL evidence workflow, SHA-256
commitment generation, JSON evidence receipts, verification, and tamper
detection in a browser-based environment.

Repository

GitHub repository:

https://github.com/bogavilliharika/cool-sdk-project
