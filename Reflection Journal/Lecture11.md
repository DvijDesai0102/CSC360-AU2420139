# Lecture 11: Hands-on Group Project Planning, Workspace UI Layout Architecture, and Rapid Prototyping

**Date:** 15 September 2026  
**Course:** CSC360: Computer Graphics and Interaction

---

### Architectural Scoping and UI Layout Design for Master-Detail Object Editors

The eleventh lecture shifted from conceptual theory into an intensive, hands-on team research and planning lab centered on our collaborative group project. Our assignment entails constructing a JavaFX application that renders a dynamic tree hierarchy of domain objects with full support for inspecting and mutating each object's properties in real time. This session allowed us to translate the abstract architectural discussions from earlier lectures into concrete design blueprints, UI wireframes, and functional prototyping workflows.

We initiated the lab by decomposing the project requirements into modular visual components. To ensure an intuitive user experience, we established a classic master-detail workspace layout. The left sidebar functions as a primary navigation panel housing a JavaFX `TreeView` control that models a hierarchical file directory structure. Selecting an individual folder or file node inside this tree triggers an event callback that dynamically populates the main canvas area on the right with the detailed properties, editable inputs, and content views associated with that specific item. Spending dedicated time upfront mapping out this structural separation allowed us to align our team's mental models, establish clear API boundaries between UI components, and avoid the friction that arises when writing code without a unified layout strategy.

---

### Interface Inspiration Analysis: Google Docs Outline vs. VS Code Workspace Navigation

To ground our architectural choices in proven human-computer interaction (HCI) paradigms, we conducted a comparative visual audit of professional desktop and web interfaces that solve similar hierarchical navigation problems, specifically analyzing Google Docs and Visual Studio Code.

Our evaluation focused on how each application balances deep nesting with spatial usability:
* **Google Docs Outline and Document Tabs:** Google Docs utilizes a linear, document-centric navigation model. Its outline panel displays structural headings and table-of-contents markers optimized for vertical document flow. While clean and simple for shallow hierarchies, it lacks native support for complex, deeply nested multi-folder directory structures.
* **VS Code Explorer Sidebar:** Visual Studio Code employs a true file-system tree view engineered for deeply nested folder structures, multi-file selection states, contextual action menus, and dynamic node expansion. The explorer view couples directly with an adjacent editor pane, making it the ideal architectural template for our object editor.

Comparing these designs side by side provided actionable insights into spatial partitioning, tree node visual affordances, and split-pane divider behaviors. Rather than attempting to invent a novel interface layout from scratch, leveraging established workspace patterns ensures that our application remains intuitive for end users.

---

### Rapid Prototyping in Antigravity via LLM-Assisted JavaFX Layout Scaffolding

After finalizing our visual layout blueprints, we transitioned to practical environment setup and rapid UI prototyping. Using the Antigravity development workspace alongside Claude, we generated an initial baseline prototype of the JavaFX layout using standard, out-of-the-box OpenJFX dependencies and layout panes (`SplitPane`, `TreeView`, and `VBox`).

Focusing on lightweight structural scaffolding rather than premature aesthetic customization allowed us to quickly evaluate window resizing behaviors, panel divider constraints, and event listener bindings between the left navigation tree and the right detail view. This iterative prototyping approach bridged the gap between theoretical user interface design and executable JavaFX code, setting a solid foundation for implementing object serialization, custom property fields, and persistent node state management in upcoming project sprints.

---

### Curated Resources and Further Reading

#### JavaFX Layout and Master-Detail Navigation Design
* OpenJFX Official Documentation: JavaFX SplitPane and TreeView API Reference (Detailed technical guide on configuring responsive workspace panels and dynamic tree nodes).
* Oracle JavaFX Tutorials: Building Master-Detail Views in JavaFX (Best practices for linking selection models in tree controls to dynamic form inputs).
* Jakob Jenkov: JavaFX Layout Panes Overview (Comprehensive reference on combining BorderPane, SplitPane, and VBox containers for desktop application layouts).

#### Interface Design and Usability Research
* Nielsen Norman Group: Tree Controls in User Interfaces (Empirical research on node expansion affordances, visual hierarchy, and navigation deep-linking).
* Visual Studio Code User Interface Anatomy: The Explorer View (Architectural breakdown of panel splitters, file trees, and editor tab integration).
* Human Interface Guidelines: Split Views and Sidebar Navigation (Design standards for multi-pane desktop interfaces and content management workflows).
