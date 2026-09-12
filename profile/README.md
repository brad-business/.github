# BRAD Business

**BRAD Business** is a business operating system for modeling, operating, accounting for, and auditing real-world businesses.

It is built on a simple premise:

> **Businesses differ in what they sell and how they operate, but the underlying economic activities are remarkably similar.**

A restaurant, farm, retailer, manufacturer, professional-services firm, SACCO, or other organization acquires resources, creates or transforms value, provides goods or services, receives or extends credit, settles obligations, and records the resulting economic activity.

BRAD Business provides a common engine for modeling these activities while allowing each business to compose the capabilities it actually needs.

---

## The Business Operating System

BRAD Business is not designed primarily as an ERP application.

It is being built as a **Business Operating System (BOS)**.

The BOS provides the underlying machinery for:

* Entities
* Commands
* State
* State transitions
* Economic events
* Resources
* Obligations
* Parties
* Transactions
* Settlement
* Accounting
* Audit
* Authorization
* Evidence
* Integrations

Business applications are then composed from these primitives.

Conceptually:

```text
                 BUSINESS OPERATING SYSTEM
                           │
          ┌────────────────┼────────────────┐
          │                │                │
       Commerce        Inventory        Finance
          │                │                │
       Services       Manufacturing     Lending
          │                │                │
          └────────────────┼────────────────┘
                           │
                      Accounting
                           │
                         Audit
```

The same underlying engine can therefore support very different types of organizations without embedding industry-specific assumptions into the core.

---

## The Economic Model

The BOS models business activity as changes in state caused by validated economic events.

At its simplest:

```text
State(t + 1)
    =
State(t)
    +
Validated Economic Event
```

A business operation can therefore be represented as:

```text
Command
   ↓
Validation
   ↓
State Transition
   ↓
Economic Event
   ↓
Consequences
   ├── Operational state
   ├── Accounting
   ├── Audit
   ├── Tax
   └── Integrations
```

For example, a sale may result in:

```text
SaleCompleted
InventoryIssued
RevenueRecognized
ReceivableCreated
PaymentReceived
```

The accounting system does not need to be the business operation itself. It is a consequence of the underlying economic event.

This separation allows the same business operation to drive operational, financial, auditing, reporting, and integration processes consistently.

---

## A Universal Business Vocabulary

The system is designed around a small number of general economic operations:

```text
ACQUIRE
CREATE
TRANSFORM
STORE
MOVE
SELL
RENT
PROVIDE
FINANCE
BROKER
LICENSE
CONSUME
TRANSFER
SETTLE
ADJUST
```

These operations can be composed into more complex business processes.

For example:

```text
Retail
    Acquire → Store → Sell → Settle

Manufacturing
    Acquire → Transform → Store → Sell → Settle

Agriculture
    Acquire → Create → Transform → Store → Sell → Settle

Professional Services
    Acquire → Provide → Bill → Settle

Lending
    Acquire Funds → Finance → Collect → Settle
```

This allows the system to model businesses by **what they do economically**, rather than by an ever-growing list of industries.

---

## State and Event Driven

The BOS is fundamentally a state-transition system.

Business entities have state:

```text
Inventory:
    Available → Reserved → Issued → Consumed

Sale:
    Draft → Confirmed → Fulfilled → Completed

Obligation:
    Created → Outstanding → Partially Settled → Settled

Loan:
    Application → Approved → Disbursed → Repaying → Settled
```

Transitions are performed through commands and produce events.

```text
Command
    ↓
Guard / Validation
    ↓
Transition
    ↓
New State
    ↓
Domain Event
```

This provides a consistent mechanism for enforcing business rules and maintaining a complete history of how the current state was reached.

---

## Accounting

Accounting is a first-class component of the system, but it is downstream from economic activity.

The system is designed to preserve the relationship:

```text
Business Operation
        ↓
Economic Event
        ↓
Accounting Event
        ↓
Journal Entry
        ↓
Ledger
        ↓
Financial Statements
```

This allows operational records and accounting records to remain connected without coupling the business domain directly to a particular accounting implementation.

The accounting engine will support the fundamental accounting structures required by businesses, including:

* Chart of accounts
* Journals
* Double-entry postings
* General ledger
* Accounts receivable
* Accounts payable
* Cash
* Assets
* Liabilities
* Equity
* Revenue
* Expenses
* Accounting periods
* Trial balances
* Financial statements

---

## Audit and Lineage

Auditability is built into the architecture rather than added as an afterthought.

The system should be able to trace a financial result back through its origin:

```text
Financial Statement
        ↓
General Ledger
        ↓
Journal Entry
        ↓
Accounting Event
        ↓
Economic Event
        ↓
Domain Event
        ↓
Command
        ↓
Actor
        ↓
Evidence
```

Important transitions will retain information such as:

* Who performed the operation
* What was requested
* What changed
* When it happened
* Why it happened
* Which entity was affected
* Which authorization permitted it
* What evidence supported it
* Which subsequent events resulted from it

This provides the foundation for operational audit, financial audit, compliance, and investigation.

---

## Installation Model

BRAD Business is designed around **independent installations rather than a shared multi-tenant business database**.

An installation is an independent operational boundary with its own:

* Business data
* Operational state
* Accounting records
* Audit history
* Configuration
* Users and permissions
* Database
* Business processes

The BRAD control plane may manage installations for purposes such as:

* Identity
* Licensing
* Installation registration
* Version management
* Updates
* Feature entitlements
* Health and fleet management

However, the business operating system itself remains independent of the control plane.

Conceptually:

```text
                    BRAD CONTROL PLANE
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
        Installation   Installation   Installation
             A             B             C
             │             │             │
            BOS           BOS           BOS
             │             │             │
          Database      Database      Database
```

This architecture provides strong data isolation and makes the system suitable for organizations where operational or regulatory separation is important.

---

## Infrastructure Agnostic Core

The BOS does not depend on a particular transport or persistence technology.

The same business engine can be exposed through:

* REST
* gRPC
* CLI
* Desktop applications
* Mobile applications
* Background workers
* Direct Rust integrations

Likewise, persistence is provided through replaceable adapters.

```text
                 ┌─────────────┐
REST ───────────►│             │
gRPC ───────────►│     BOS     │
CLI ────────────►│             │
Tauri ──────────►│             │
Worker ─────────►│             │
                 └──────┬──────┘
                        │
                 ┌──────┴──────┐
                 │             │
              PostgreSQL     SQLite
                 │             │
              Memory / Other Adapters
```

The core therefore has no knowledge of HTTP, SQL, PostgreSQL, SQLite, or any particular UI framework.

Those concerns belong to adapters and applications.

---

## Rust

The core of BRAD Business is written in **Rust**.

Rust is particularly well suited to this architecture because the type system allows important business concepts and invariants to be represented explicitly.

Examples include:

* Strongly typed identifiers
* Explicit state machines
* Commands and events
* Domain-specific errors
* Traits for infrastructure boundaries
* Compile-time dependency boundaries
* Explicit ownership of state
* Safe concurrency
* Reliable long-running services

The goal is not simply to use Rust as an implementation language.

The goal is to use Rust's type system to make the business model itself explicit.

---

## Workspace Architecture

The entire project is maintained as a single Cargo workspace.

The initial architecture is:

```text
brad-business/
│
├── crates/
│   ├── bos/
│   ├── domain/
│   ├── economics/
│   ├── accounting/
│   └── audit/
│
├── capabilities/
│   ├── commerce/
```
