# The Neo-Alexandria Vision

Neo-Alexandria is an open, decentralized protocol for asking experts what to read and commissioning them to write new work. Anyone on the network can ask a human or AI expert for a recommendation in their field, or name a price for a document they want that expert to write.

The name comes from the Library of Alexandria. In Neo-Alexandria, the collection and the people and agents who know it are spread across the network. A question can lead someone to a book they might otherwise overlook. It can also lead to a new work that others can find and recommend.

## Recommendations and commissions

Suppose you want to understand why an irrigation technique that works in trials falls short on small farms. An expert might recommend one field study and tell you which section speaks to your question. If the evidence is scattered, you might offer to pay that expert for a short review that brings the studies together. The expert can accept, propose different terms, or decline. When the parties agree to share the result, it can become a reference for the next person who asks.

The protocol is token-free and carries no protocol fees. A commission records what the requester wants, the price they offer, and the terms the parties agree to. The parties choose how to settle payment for the expert's work.

## Participation like email

Anyone can run their own client or use a service that operates one for them. Independently operated systems can discover and communicate with one another through a shared public specification. Participants can join without registering with a central authority. As with email, recipients decide which messages to accept and whom to engage.

Experts can make their areas of expertise discoverable. Requesters can use a participant's published work, citations, or recommendations from people they trust to decide whom to ask. Different communities can make those judgments for themselves while still exchanging requests over the same protocol.

## A specification for generating secure clients

Someone should be able to give the public specification to a coding agent and generate a complete client they can verify and run. The specification must define the rules peers agree on, including how they discover one another and exchange messages. It must also state the threat model and the security requirements for clients, including how to protect local keys, verify who agreed to a commission, and handle documents from untrusted peers. A public conformance suite should cover successful exchanges and inputs a client must reject.

Coding agents can make it practical for more people to build and maintain their own implementations. The specification should define required behavior and leave implementers room to choose their languages, libraries, and internal designs. When the network runs genuinely independent implementations, a flaw specific to one can affect its users while other clients keep working. The shared specification and common dependencies deserve scrutiny because flaws there can affect several clients at once.

## Building on Ken and Ongo

Ken gives people and agents a portable catalog for publications, notes, and relationships such as citations. Ongo takes research requests, records findings in Ken, and can publish work publicly or with restricted access. Together they provide a way to keep a research record and turn a question into work someone can read. [Ken](https://github.com/zomglings/ken#readme) · [Ongo](https://github.com/zomglings/ongo#readme)

Neo-Alexandria extends that workflow across independent operators. An expert using Ongo should be able to answer a requester using a client written by somebody else. Each participant can choose how they keep their references and carry out their research.

## First demonstration

Two people independently generate clients from the published specification and run them on separate systems. One discovers the other, asks for a reading recommendation, and receives a reference with a short explanation. They then agree on the scope and price of a small commission, and the expert delivers the finished document. That would show that someone can build a client from the public specification and use it to take part in the network.
