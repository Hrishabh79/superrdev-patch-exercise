# Patch Notes

## 1. Incorrect task filtering
- File: backend/src/main/java/com/internal/tasktracker/TaskRepository.java
- Layer: Repository
- Discovery: Code inspection and status/search testing
- Root cause: AND/OR conditions in the SQL query were not grouped correctly.
- Fix: Grouped title and description search conditions with parentheses.
- Why: Ensures archived and status filters apply correctly to all search results.

## 2. Artificial API delay
- File: backend/src/main/java/com/internal/tasktracker/TaskController.java
- Layer: Controller
- Discovery: Code inspection
- Root cause: Every request called Thread.sleep() based on query length.
- Fix: Removed the artificial delay and complexity calculation.
- Why: Prevents unnecessary latency and blocked server threads.

## 3. Pagination not reset after filtering
- File: frontend/src/App.jsx
- Layer: Frontend
- Discovery: Code inspection and UI testing
- Root cause: Search and status changes kept the previous page number.
- Fix: Reset the page to 1 when search or status changes.
- Why: Prevents empty or incorrect results when the new filter has fewer pages.

## 4. Loading state stuck after API failure
- File: frontend/src/hooks/useTasks.js
- Layer: Frontend
- Discovery: Code inspection
- Root cause: The error handler did not reset the loading state.
- Fix: Clear previous errors on new requests and set loading to false on failure.
- Why: Keeps the UI responsive when an API request fails.
