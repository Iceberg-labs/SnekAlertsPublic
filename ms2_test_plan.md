### **Test Plan for SnekAlerts Registration Normalization and Event Scheduling**

#### **Feature Description**
The feature includes:
1. **Normalization of Registration Data**: Converts an array of registration objects into a dictionary keyed by the `asset` field, ensuring efficient access and processing.
2. **Event Scheduling**: Schedules the `defi_events` coroutine to run every minute, ensuring asynchronous execution within an active event loop.

---

### **Test Cases**

#### **Test Case 1: Normalization of Registration Data**
**Objective**: Verify that the `normalize_registrations` function correctly transforms the input array into the desired dictionary format.

- **Input**:
  ```python
  [
      {'asset': 'abc123', 'discord': 12345, 'telegram': 67890, 'custom_settings': {'min_ada_buy': 25}},
      {'asset': 'def456', 'discord': 54321, 'telegram': 98765, 'custom_settings': {'min_ada_buy': 50}}
  ]
  ```
- **Expected Output**:
  ```python
  {
      'abc123': {'discord': 12345, 'telegram': 67890, 'custom_settings': {'min_ada_buy': 25}},
      'def456': {'discord': 54321, 'telegram': 98765, 'custom_settings': {'min_ada_buy': 50}}
  }
  ```
- **Steps**:
  1. Call `normalize_registrations` with the input array.
  2. Verify the output matches the expected dictionary.

- **Result**: ✅ Passed

---

#### **Test Case 2: Event Scheduling**
**Objective**: Ensure that the `defi_events` coroutine is scheduled to run every minute without runtime errors.

- **Steps**:
  1. Call `schedule_jobs` to schedule the `defi_events` coroutine.
  2. Verify that the job is added to the scheduler.
  3. Simulate the scheduler running and ensure `defi_events` executes without errors.

- **Expected Behavior**:
  - The job is added to the scheduler.
  - `defi_events` executes asynchronously without blocking or runtime errors.

- **Result**: ✅ Passed

---

#### **Test Case 3: Handling of Asynchronous Execution**
**Objective**: Verify that `defi_events` executes properly within an active event loop.

- **Steps**:
  1. Start an asyncio event loop.
  2. Trigger the scheduled job manually.
  3. Ensure `defi_events` executes without raising `RuntimeError` or warnings about unawaited coroutines.

- **Expected Behavior**:
  - No `RuntimeError` for `asyncio.run` in an active event loop.
  - No warnings about unawaited coroutines.

- **Result**: ✅ Passed

---

#### **Test Case 4: Integration with Frigid APIs**
**Objective**: Verify that the `defi_events` function interacts correctly with the existing Frigid APIs and handles responses as expected.

- **Steps**:
  1. Ensure the Frigid API endpoints are accessible.
  2. Trigger the `defi_events` function and observe its interaction with the APIs.
  3. Verify that the responses are processed correctly.

- **Expected Behavior**:
  - Successful responses are processed correctly.
  - Any errors or timeouts are logged without crashing the application.

- **Result**: ✅ Passed

---

#### **Test Case 5: Longevity Testing**
**Objective**: Verify that the system can maintain uptime and functionality over an extended period of 30 days.

- **Steps**:
  1. Deploy the system in a controlled environment.
  2. Ensure the `defi_events` function executes as scheduled every minute.
  3. Monitor the system for any crashes, memory leaks, or performance degradation.

- **Expected Behavior**:
  - The system remains stable and functional for 30 days.
  - No crashes, memory leaks, or significant performance degradation occur.

- **Result**: ✅ Passed

---

### **Test Results Summary**

| **Test Case**                     | **Status** | **Remarks**                                                                 |
|------------------------------------|------------|------------------------------------------------------------------------------|
| Normalization of Registration Data | ✅ Passed  | Function correctly transforms input array into the desired dictionary format. |
| Event Scheduling                   | ✅ Passed  | `defi_events` is scheduled to run every minute without runtime errors.        |
| Handling of Asynchronous Execution | ✅ Passed  | No runtime errors or warnings in an active event loop.                        |
| Integration with Frigid APIs       | ✅ Passed  | Interacts with Frigid APIs as expected, processing responses correctly.       |
| Longevity Testing                  | ✅ Passed  | System maintained uptime and functionality over 30 days without issues.      |

---

### **Conclusion**
The feature has been tested thoroughly and meets the functional requirements. All test cases passed successfully, and the implementation is robust against potential runtime issues and external API failures.
