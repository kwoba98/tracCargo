# tracCargo
tracCargo – A Power Apps solution for tracking cargo and empty-container movements at ICDs, capturing operational events in real time and supporting automated reporting, visibility, and cargo traceability.

# tracCargo
### Cargo & Empty-Container Tracking System

**tracCargo** is a Power Apps-based solution designed to improve visibility and traceability of cargo and empty-container movements at Inland Container Depots (ICDs). It captures operational events in a centralized SharePoint list, providing a foundation for tracking cargo progress, retrieving movement histories, and transforming operational records into structured reports.

## 1. The Problem

Traditional ICD tracking and reporting often depend on manual data entry, spreadsheets, and separate operational records. This can make it difficult to establish the latest status of a container, trace its movement history, identify outstanding activities, and compile reliable operational reports.

tracCargo aims to simplify this process by capturing movement events as they occur and maintaining a structured record of each activity.

## 2. Project Objectives

- **Improve traceability:** Maintain a chronological record of cargo and empty-container events.
- **Standardize data capture:** Use structured fields and predefined event types to improve consistency.
- **Centralize operational records:** Store submitted events in a SharePoint list.
- **Support faster reporting:** Use captured event timestamps to build operational reports and calculate turnaround times.
- **Improve visibility:** Make it easier to retrieve the recorded history of a container or operational reference.
- **Establish a scalable foundation:** Begin with a pilot ICD before considering expansion to other stations.

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| Microsoft Power Apps | Mobile-friendly operational data capture |
| Microsoft SharePoint Lists | Centralized storage of tracking events |
| Microsoft Power Query | Data transformation and report preparation |
| Microsoft Excel | Analysis and operational reporting |
| QR/barcode scanning | Planned or configurable identification workflow for operational references |

## 4. How tracCargo Works

tracCargo follows an **event-based tracking model**. Each operational activity is recorded as a separate event rather than overwriting the previous status.

<escape>
Operational Event → Power Apps → SharePoint Event Log → Power Query → Operational Reports
</escape>

Each event can record information such as:

- FFID or operational reference
- Cargo or empty-container classification
- Transaction type: import, export, or transit
- Event type
- Container number and size
- Cargo description, where applicable
- Truck registration
- Station
- Cross-stuffing container reference, where applicable
- Event timestamp
- Remarks
- User information and synchronization status, where implemented

This structure provides a history of recorded activities and supports reconstruction of a container's operational timeline.

## 5. Operational Workflows

### Empty-Container Tracking

The initial workflow supports the following event types:

1. **Received** – Records the receipt of an empty container.
2. **From Cross Stuffing** – Records an empty container associated with a cross-stuffing activity.
3. **Backloaded** – Records a backloading activity.

### Cargo Tracking

The initial workflow supports the following event types:

1. **Received** – Records cargo receipt.
2. **Cross Stuffed** – Records a cross-stuffing activity.
3. **Loaded** – Records a loading activity.
4. **Released** – Records cargo release.

The available event types depend on whether the operation is classified as **Empty** or **Cargo**.

*These event definitions can be refined as the pilot workflow is validated against actual ICD procedures.*

## 6. Data Model

The central SharePoint list is named `ICD_Event_Log`.

| Field | Purpose |
|---|---|
| `FFID` | Links events to an operational reference |
| `Empty_Cargo` | Identifies the operation category |
| `TRANS_IMP_EXP` | Records the transaction type |
| `EventType` | Identifies the activity being recorded |
| `ContainerNo` | Identifies the container |
| `ContainerSize` | Records container size or configuration |
| `CargoName` | Records the cargo description, where applicable |
| `TruckNo` | Records the associated truck registration |
| `Station` | Identifies the operational station |
| `CrossStuffContainer` | Records the related container, where applicable |
| `Timestamp` | Records the event date and time |
| `Remarks` | Captures additional operational information |
| `Sync_Status` | Tracks synchronization state, if synchronization handling is implemented |
| `UserEmail` | Identifies the user associated with the event |

Each row represents an individual event. Multiple events can share the same FFID and container number, allowing the event log to preserve the sequence of activities.

## 7. Reporting and Analytics

The event log can be transformed into a report-friendly dataset using Microsoft Power Query.

Potential reporting capabilities include:

- Reconstructing container timelines by FFID and container number.
- Pivoting event types into milestone columns with their corresponding timestamps.
- Identifying missing milestones and outstanding activities.
- Calculating elapsed time between operational milestones.
- Supporting container dwell-time and turnaround-time analysis.
- Producing station-level operational summaries.

**Important:** Repeated event types require explicit business rules. For example, a report must define whether to use the first recorded receipt, the latest loading event, or another timestamp when an activity occurs more than once. The reporting logic should also account for incomplete journeys and multiple operational cycles.

## 8. Application Screens

The planned application structure includes:

1. **Home / Cargo Tracking** – Entry point for tracking activities.
2. **Scan Cargo** – Captures or retrieves an operational reference.
3. **Update Status** – Records a new operational event.
4. **Confirmation** – Displays the outcome of a submission.
5. **Pending Sync** – Intended for displaying records awaiting synchronization, if offline support is implemented.
6. **History / Lookup** – Retrieves previously recorded information.
7. **Error Screen** – Communicates validation or submission errors.

The exact screen behavior will evolve as the pilot is tested with operational users.

## 9. Current Implementation and Development Priorities

The application has been connected to the SharePoint list, and basic event submission has been tested.

The next development priorities are:

- Validate the event-capture process against real operational scenarios.
- Implement reliable container history and lookup.
- Develop and reconcile the Power Query reporting logic.
- Introduce input validation and duplicate-event handling.
- Test repeated milestones, incomplete records, and separate operational cycles.
- Evaluate offline capture and synchronization before relying on them operationally.
- Pilot the application at one ICD before expanding to additional stations.

## 10. Future Enhancements

Potential future enhancements include:

- QR/barcode-based retrieval of container and operational references.
- Offline event capture with reliable synchronization.
- Duplicate detection and validation rules.
- Automated exception and overdue-activity reporting.
- Dashboards for station performance and turnaround times.
- Multi-station support and role-based access.
- Integration with additional operational data sources.

These are development opportunities rather than claims that every feature is already available.

## 11. Expected Outcome

tracCargo aims to provide a more consistent way to capture and trace cargo and empty-container movements, reduce reliance on fragmented manual records, and create a dependable data foundation for operational reporting.

The long-term objective is to connect **operational event capture, container traceability, and reporting** in one practical workflow.

---

**Project:** tracCargo  
**Platform:** Microsoft Power Apps  
**Data Storage:** Microsoft SharePoint Lists  
**Reporting:** Microsoft Power Query and Excel  
**Initial Scope:** Cargo and empty-container tracking at a pilot ICD
