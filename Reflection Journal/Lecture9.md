# Lecture 9: Textual Versus Graphical Representations, Headless Architectures, and JavaFX Application Patterns

**Date:** 3 August 2026
**Course:** CSC360: Computer Graphics and Interaction

---

### Textual Versus Graphical Paradigms: ASCII Trees and Headless Systems

The ninth lecture centered on the architectural division between text-based interfaces and graphical rendering pipelines through a review of group project specifications. We opened with an analysis of Group 4's assignment, which involves representing hierarchical tree structures through two distinct modalities: printing an ASCII tree via standard output versus drawing a graphical tree on a rendering canvas.

Printing an ASCII tree relies purely on character streams and terminal formatting, using monospaced glyphs and line-drawing Unicode characters (such as vertical bars, horizontal tees, and corner connectors) arranged with precise indentation. This format mirrors standard command-line directory trees like the Unix `tree` utility, where the root directory appears at the top level and nested child files or subdirectories are indented beneath. In contrast, drawing a graphical tree requires spatial layout algorithms, node bounding-box calculations, vector stroke rendering, and explicit pixel coordinate transformations.

Evaluating the trade-offs between these two paradigms highlighted why text remains fundamental in computer science:
* **Computational Overhead:** ASCII text rendering requires minimal memory, zero graphical context initialization, and negligible CPU cycles, whereas graphical rendering demands window context creation, scene graph traversal, rasterization pipelines, and continuous event loops.
* **Remote Accessibility and Headless Execution:** A headless system operates entirely without a graphical user interface or physical display presentation layer. Text is the primary and most direct mechanism for communicating with the operating system kernel and CPU. When connecting to remote servers where GUI tools like AnyDesk are unavailable or introduce excessive bandwidth overhead, secure cryptographic protocols like SSH enable rapid, full-featured administration through raw character streams.
* **Command Line Superiority:** While graphical user interfaces provide intuitive discoverability for end users, command-line interfaces (CLI) offer far greater composability, scriptability, and administrative power through Unix pipelines, standard input/output redirection, and automation scripts.

---

### Visualizing Relational Data: Group 5 and Dynamic Arrow Mapping

The session transitioned to Group 5's project, which requires developing a Java program that renders directed arrows connecting matching elements across two separate lists of strings. This topic illustrated the primary value proposition of computer graphics over pure text: human cognitive bandwidth and visual pattern recognition.

When comparing two independent collections of text data in a terminal, identifying intersections or many-to-many relationships requires exhaustive manual scanning. By rendering the two string collections as vertically aligned visual lists separated by an open canvas space, the application can draw dynamic vector arrows or cubic Bézier spline paths between identical strings. This graphical mapping transforms an abstract set-intersection problem into an immediate visual relationship, demonstrating how vector graphics facilitate rapid data analysis and relationship comprehension.

---

### JavaFX Architecture and Decoupled UI: Group 6's Custom Splash Screen

We examined Group 6's assignment, which involves designing a modular splash screen in JavaFX using FXML. Building modern desktop user interfaces requires clean architectural separation between presentation layout and procedural business logic. FXML achieves this separation by providing an XML-based declarative markup language for defining scene graph components, styling, and visual structure, while delegating dynamic event handling to an associated Java controller class.

To construct an effective splash screen, we broke down the engineering requirements into modular components:
* **Visual Identity Assets:** Rendering the primary application brand name, vector or raster logo graphics, version metadata, and custom background canvases.
* **Non-Blocking Asset Preloading:** Displaying an indeterminate progress indicator or dynamic loading bar while application resources, configuration files, and database connections initialize asynchronously on a background worker thread.
* **Stage Transitions:** Automatically transitioning the primary JavaFX Stage from the temporary, undecorated splash window into the main application dashboard once startup tasks finish execution.

---

### Hierarchical Object Management and Serialization: Group 7's Tree Property Editor

Group 7's project introduced advanced JavaFX component hierarchies and object persistence through a master-detail tree editing interface. The application layout consists of a dual-pane workspace:
* **Navigation View (Left Panel):** A hierarchical `TreeView` component displaying nested domain objects and folder structures. Expanding or selecting a node exposes its child elements and triggers event handlers that notify the surrounding workspace.
* **Property Inspector View (Right Panel):** A dynamic form panel that inspects the object currently selected in the tree, exposing its internal fields and properties through editable controls like text inputs, toggle switches, and numeric steppers.

A key software engineering requirement discussed for this assignment is object serialization. When a user modifies an object's properties in the right-hand panel and triggers a save action, the application must serialize the in-memory object graph into a durable storage format, such as structured JSON or Java native binary object streams (`ObjectOutputStream`). Upon launching the application in future sessions, the deserialization pipeline reconstructs the persisted object hierarchy, restoring the state of the tree view and the properties of each individual node.

---

### Multi-Job Concurrency and Worker Threading: Group 8's Composite Progress Bar

The final project review addressed Group 8's assignment: constructing a composite progress bar system capable of tracking multiple asynchronous background jobs with support for real-time task cancellation. This assignment directly reinforced the concurrency principles explored in Lecture 6 regarding UI thread safety.

Because the JavaFX Application Thread manages the scene graph and UI event dispatching, running heavy background workloads on the main thread would freeze the entire interface. Group 8's architecture must implement robust thread management using modern Java concurrency constructs, such as `ExecutorService` thread pools and the JavaFX `Task<V>` framework. Each individual workload executes on a background worker thread, calculating its progress and reporting completion percentages back to the UI thread using thread-safe properties like `task.progressProperty()`.

The composite progress tracker aggregates these individual worker metrics into an overall completion percentage while allowing users to invoke cancellation triggers on specific jobs. Handling task cancellation safely requires background tasks to periodically check their interrupt status (`Thread.currentThread().isInterrupted()`), release allocated resources cleanly, terminate execution gracefully, and transition the corresponding UI progress indicator into a cancelled state without destabilizing the rest of the application.

---

### Curated Resources and Further Reading

#### Terminal Systems, Text Streams, and Headless Architectures
* The Linux Documentation Project: Text Terminal HOWTO and Standard Streams (Fundamental guide on terminal emulators, stdin, stdout, and character devices).
* OpenSSH Official Documentation: SSH Architecture, Key Authentication, and Headless Server Administration (Detailed guide on remote server management without display managers).
* GNU Coreutils: Tree and Indentation Formatting in Command Line Environments (Reference on hierarchical directory visualization using monospaced text streams).

#### JavaFX Scene Graph, FXML, and Component Layouts
* OpenJFX Official Documentation: Getting Started with JavaFX and FXML (Architectural guide on separating presentation markup from controller implementations).
* Oracle JavaFX Tutorials: Working with JavaFX TreeView (Implementation reference for building dynamic master-detail node hierarchies).
* Jakob Jenkov: JavaFX FXML Tutorial and Scene Graph Hierarchy (Practical guide to declarative UI construction and stage management).

#### Concurrency, Worker Tasks, and Asynchronous UI Updates
* Oracle Documentation: Worker Threads and the JavaFX Task Framework (Essential patterns for coordinating long-running background jobs with the JavaFX Application Thread).
* Brian Goetz: Java Concurrency in Practice (The definitive industry textbook covering thread pools, cancellation mechanics, and thread-safe shared state).
* Baeldung: Guide to Java Object Serialization (Step-by-step tutorial on serializing complex object graphs to disk using JSON and native Java streams).
