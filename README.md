# Hospital Management & Smart Ambulance System

Hey there! I’m excited to share my dual-module Java project that I’ve been working on. It’s actually two complementary systems in one repo:

1. **Hospital Management System** – a JavaFX desktop app to register patients, handle appointments, manage waiting lists and billing.
2. **Smart Ambulance Dispatch & Routing** – a console-based simulation of optimal ambulance dispatch and hospital selection using graph algorithms from the IEEE Access 2022 paper, “A Novel Smart Ambulance System.”

---

## Why I Built This

I wanted to simulate two critical parts of emergency healthcare:

- **Inside the hospital**: from patient intake to billing and reporting.
- **In the field**: dispatching ambulances in real time, routing them to the best hospital based on current traffic and bed availability.

Combining these taught me a ton about JavaFX UIs, data structures, Dijkstra’s algorithm, and end-to-end system design.

---

## What’s Inside

### 1. Hospital Management System

- **Patient Registration**  
  I store patient details (ID, name, age, contact, history) in a self-balanced BST for O(log n) lookups.

- **Appointments & Waiting List**  
  Appointments go into a simple queue; urgent requests land in a custom min-heap priority queue sorted by date/time.

- **Billing Module**  
  Each patient has a billing record. I serialize their payment history to JSON for storage, update it via JDBC calls, and can adjust their billing on the fly.

- **Reporting**  
  A `ReportGenerator` runs QuickSort on lists of patients, appointments, or bills to generate neatly formatted textual reports.

- **UI**  
  Built with JavaFX + FXML (Scene2 for management, Scene6 for billing). I keep input fields and output labels separate, and weave in back-and-forth navigation.

### 2. Smart Ambulance Dispatch & Routing

- **Graph Representation**  
  A directed weighted graph models our city map, with asymmetric forward/backward travel times. Dijkstra’s algorithm finds shortest paths.

- **Ambulance Model**  
  Tracks each ambulance’s location, readiness time, and availability.

- **Hospital Model**  
  Monitors bed capacity, emergency facilities, and dynamically computes drop-off delays.

- **Emergency Orchestrator**  
  - **Algorithm 1 (Dispatch)**: Dequeue patient requests, pick the ambulance with the minimal `(readiness + travelTime)`.  
  - **Algorithm 2 (Hospital Selection)**: For that ambulance, evaluate each hospital’s `(travelTime + dynamicResponseTime)` and pick the minimum.  

- **Demo Harness**  
  A `Main.java` sets up a sample graph, three hospitals, three ambulances, and three patient calls—then runs the full dispatch & routing simulation in your console.

---

## How to Run

### Hospital Management (JavaFX)

1. Clone the repo  
2. Open the `HospitalManagement` folder in IntelliJ/your IDE  
3. Add the JavaFX SDK (17+) to your module path:  
--module-path /path/to/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml

4. Run `MainApplication` (it launches Scene2 by default)

### Smart Ambulance System (Console)

1. Navigate to `SmartAmbulanceSystem/Backend`  
2. Compile all classes:  
```bash
javac *.java

