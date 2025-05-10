# Cloud_assigmnent
### **How Visibility Timeout and Dead-Letter Queue (DLQ) Improve Reliability**  

#### **1. Visibility Timeout**  
- **Purpose**: Prevents duplicate processing of SQS messages.  
- **How It Helps**:  
  - When a Lambda reads a message, SQS makes it *invisible* to other consumers for a set duration (e.g., 30 seconds).  
  - If Lambda succeeds, the message is deleted.  
  - If Lambda fails (e.g., crashes/timeout), the message reappears for retry.  
- **Benefit**: Ensures each order is processed **exactly once**, even if Lambda fails temporarily.  

#### **2. Dead-Letter Queue (DLQ)**  
- **Purpose**: Cataches messages that repeatedly fail processing.  
- **How It Helps**:  
  - After `MaxReceiveCount` (e.g., 3 retries), failed messages move to the DLQ.  
  - Example: Malformed orders won’t loop indefinitely, allowing manual debugging.  
- **Benefit**: Isolates problematic messages while keeping the main queue flowing.  

#### **Why Both Matter**  
Together, they:  
✔ **Prevent data loss** (DLQ)  
✔ **Avoid infinite retries** (Visibility Timeout)  
✔ **Maintain system stability** during errors.  
