# M5 — Failed regression and incident-reopening workflow

**Classification:** Mixed — **actual failed negative control test** documented in M3, followed by a **simulated ticket reopening workflow**. There is no evidence that a previously closed real incident ticket was reopened in a support system.

## Evidence-supported regression failure

| Test | Intended outcome | Actual JV2 sandbox observation | Result |
|---|---|---|---|
| REG-BLOCK-01, order-header block 04, order 1056 | F2 billing should be prevented while applicable billing block 04 remains active (test expectation) | Invoice 90000304 and FI posting 9400000058 were completed; order header still displayed block 04 | **Failed expected control**, EV-036–EV-037 / EV-051 |
| REG-BLOCK-02, delivery-header block 04, delivery 80000787 | F2 billing should be prevented by the tested delivery header block (test expectation) | F2 invoice 90000305 was created; evidence includes block selection and user confirmation of saved value | **Failed expected control**, EV-038–EV-039 / EV-052; saved-state screenshot absent |

**Interpretation:** These are **actual negative-test failures**, but the cause and correctness of the expectation still require JV2-specific configuration review. No previous verified permanent fix for this block existed, so they are **not proof of regression following a successfully deployed change**.

## Reopening a ticket — documented simulation, not actual ticket history

1. **Illustrative state:** A support analyst hypothetically closes a billing-block incident after assuming block 04 prevents billing. **Not an actual closure.**
2. **Retest:** Actual JV2 evidence above shows billing proceeded when the blocking check was expected to prevent it.
3. **Simulated decision:** Reopen the *hypothetical* incident because closure criteria were not achieved. Mark validation **Failed**, assign investigation to billing configuration owner and link [PRB-SD-001](Problem-Record-PRB-SD-001.md).
4. **Appropriate real status:** **Open / awaiting JV2 CBC review**. Do not represent a hypothetical reopening as an executed support-tool action.
5. **Future closure evidence:** Authorized JV2 customizing review, defect or accepted-design decision, negative/positive regression results and business acceptance.

## What was and was not achieved

- **Achieved in SAP:** Two billing-block negative/control tests with actual invoice outcomes; T41 04/F2 assignment inspected independently but not applicable as JV2 proof.
- **Achieved as documentation:** Professional reopen/escalate/problem-link workflow, explicit failed-test classification.
- **Not achieved:** Actual service-desk ticket reopening, approved configuration change, successful fixed-control retest, and real business sign-off.
