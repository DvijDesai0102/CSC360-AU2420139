# Lecture 13: Feature Refinement, JSON Data Persistence, Repository Governance, and Technical Presentation Strategy

**Date:** 29 september 2026  
**Course:** CSC360: Computer Graphics and Interaction

---

### Implementation Progression: Extended Tree Hierarchies and Bug Resolution

The thirteenth lecture focused on active software implementation and feature integration for our collaborative group project. Moving past initial UI scaffolding and structural research, our team directed development efforts toward expanding the core functional capabilities of our JavaFX master-detail application. We expanded the file directory tree view to support deep, multi-level nesting of domain objects, ensuring that node selection, dynamic expansion, and parent-child parentage relationships remain computationally stable across large object graphs.

In parallel with feature expansion, we conducted an intensive debugging cycle to resolve lingering UI state anomalies and event dispatch errors. Specifically, we addressed edge cases surrounding event listener fires during node selection switches, ensuring that editing properties in the right-hand panel accurately mutates the underlying target model without corrupting adjacent node states. Resolving these technical bugs stabilized the core rendering loop, paving the way for persistent storage integration.

---

### Persistence Architecture: JSON Import and Export Operations

A primary technical milestone achieved during this session was the complete implementation of JSON import and export functionality for state persistence. Earlier theoretical discussions on object serialization highlighted that interactive desktop software cannot exist solely in transient heap memory; application states must survive process restarts and be transferable across host environments.

To realize this, we implemented data access mechanisms that translate in-memory JavaFX object trees into structured, human-readable JSON payloads:
* **Export Pipeline:** Navigating the dynamic `TreeView` structure, extracting internal object properties, and serializing the complete object graph into a standardized JSON file format using structured mapping libraries.
* **Import and Reconstitution Pipeline:** Reading external JSON documents from disk, parsing node hierarchies, deserializing property fields back into typed domain models, and dynamically re-populating the JavaFX `TreeView` and detail forms.

Implementing this persistence layer bridges runtime user interactions with durable file system storage, ensuring our application functions as a fully realized, production-grade desktop utility.

---

### Repository Documentation Conventions: README vs. GitHub Wiki Organization

As our codebase grew in feature density, team discussions highlighted potential confusion regarding documentation governance, specifically defining clear operational boundaries between the repository `README.md` file and the GitHub Wiki.

To resolve this ambiguity, we established strict documentation conventions:
* **Primary README.md File:** Acts as the executive entrance to the repository, containing essential setup instructions, build execution flags via Maven, environment prerequisites, high-level feature overviews, and the definitive directory layout of the codebase.
* **GitHub Wiki Workspace:** Functions as a comprehensive technical knowledge base, hosting in-depth architectural guides, class diagrams, API references, detailed user manuals, and individual feature specifications.

Following this decision, we refactored the project file structure and updated the main `README.md` file to reflect our current package hierarchy and JSON schemas. Aligning repository documentation directly with executable code prevents technical debt, simplifies peer reviews, and provides graders with a clear roadmap of the application architecture.

---

### Technical Communication Strategy: Feature-Driven Presentation Planning

The session concluded with a strategic planning phase for our upcoming final project presentation. Communicating complex technical achievements effectively requires a structured, narrative-driven presentation framework.

We finalized a presentation roadmap structured around feature screenshots ordered chronologically by technical complexity:
1. **Foundational Layout:** Demonstrating the baseline JavaFX layout, showing the primary split-pane, left-hand navigation tree, and empty workspace area.
2. **Interactive Node Editing:** Highlighting dynamic tree expansion, node selection listeners, and live property mutations in the right-hand inspection form.
3. **Advanced Persistence and File Operations:** Showcasing complete JSON import/export workflows, file dialog integrations, and state restoration across application restarts.

Structuring the presentation to mirror our actual engineering timeline demonstrates logical problem decomposition, illustrating how simple graphical primitives and layout containers incrementally evolved into an interactive data management platform.

---

### Curated Resources and Further Reading

#### Data Serialization and JSON Processing in Java
* Jackson Project Documentation: Java Object Serialization to JSON (Comprehensive guide on mapping nested object graphs into JSON documents).
* Google Gson User Guide: Dynamic Tree Deserialization (In-depth reference on parsing heterogeneous object hierarchies and custom type adapters).
* Oracle Java Tutorials: File I/O and Native Stream Operations (Best practices for managing local file system streams, character encodings, and error handling).

#### Open-Source Documentation and Repository Management
* GitHub Docs: Master Guidelines for README Files vs. GitHub Wikis (Official standards for structuring project entry points and technical wiki documentation).
* Write the Docs Community: Technical Documentation Architecture for Engineering Teams (Industry guidelines on maintaining documentation synchronicity alongside active codebases).
* Martin Fowler: Code Smells and Documentation Decay (Architectural essay on managing technical debt through clear software structure and clear docs).
