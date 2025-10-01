# Smart Office Facility Manager

## 🎯 Overview
This project implements a **console-based application** for managing a smart office facility, including conference room bookings, occupancy detection, and automated controls.  

It directly addresses the requirements of the coding exercise by focusing strictly on **logic, code quality, design patterns, and SOLID principles**.  

The application is built in **Java (Maven-based)** and is designed for **high maintainability and extensibility**.

---

## ✨ Design Philosophy: The Six Design Patterns
This solution integrates six core design patterns to demonstrate **two behavioral, two creational, and two structural patterns**.

| Pattern Type | Pattern                   | Component / Use Case             | Rationale / Requirement Met |
|--------------|--------------------------|----------------------------------|------------------------------|
| Creational   | **Singleton**             | SmartOfficeHub & Logger          | Ensures only one instance manages global state and logging. |
|              | **Factory Method**        | RoomDeviceFactory                | Creates and wires LightController and ACController to rooms, adhering to OCP. |
| Behavioral   | **Command**               | ICommand & Concrete Commands     | Encapsulates user requests (Booking, Config, Stats) for flexible, traceable operation. |
|              | **Strategy**              | FiveMinuteTimeoutStrategy        | Encapsulates the 5-minute booking auto-release rule (Req. 4), promoting flexibility. |
| Structural   | **Observer**              | MeetingRoom (Subject) & Controllers | Automates lights/AC based on occupancy status (Req. 5). |
|              | **Proxy**                 | AuthenticatedCommandProxy        | Controls access to secured commands (Config, Block, Cancel), demonstrating authentication (Optional Req. 2). |

---

## ⚙️ Project Structure
The project follows **best practices with logical separation of concerns** enforced by Java packages:

| Package     | Content Focus |
|-------------|---------------|
| **core**    | Central state (SmartOfficeHub), main entities (MeetingRoom, Session). |
| **commands**| User actions (BookRoomCommand, ConfigRoomCountCommand). |
| **controllers** | Devices and observers (IController, ACController, NotificationService). |
| **strategies**  | Business rule policies (IBookingReleaseStrategy, FiveMinuteTimeoutStrategy). |
| **adapters**    | Translates console input string into executable ICommand objects. |
| **proxies**     | Implementation of authentication proxy (AuthenticatedCommandProxy). |
| **services**    | Background tasks and helpers (BookingMonitorService, UserAuthenticator). |
| **utilities**   | Logger (Singleton) and custom exceptions. |

---

## 🔑 Gold Standards & Key Implementations

### ✅ Logging & Exception Handling
- **Logger (Singleton):** Tracks successes and errors.  
- **Custom Exceptions:** (e.g., `BookingConflictException`) ensure **user-friendly error output** while logging technical details internally.

### ✅ Transient Error Handling / Performance
- **BookingMonitorService** runs asynchronously using `ScheduledExecutorService` to manage time-dependent **auto-release (5 minutes)**.  
- Ensures main console remains responsive.

### ✅ Security (Proxy Pattern)
- **AuthenticatedCommandProxy** restricts access to secured commands.  
- Only **admin users** can execute configuration and booking operations.

---
