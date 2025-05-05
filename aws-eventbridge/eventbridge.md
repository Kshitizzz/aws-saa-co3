# AWS EventBridge

## Memory Hook

- “EventBridge = AWS’s Event Router”
- “When X happens, automatically trigger Y.”

---

## ✅ Must-Know Core Concepts

- **EventBridge** is a serverless **event bus** for routing events between services.
- It connects:
  - AWS service events (native)
  - Custom applications (your app emits events)
  - SaaS platforms (Zendesk, Datadog, Shopify, etc.)
- Events are JSON payloads with **source**, **detail-type**, and **details**.

### Core Components

- **Event Bus**: Ingests events (default, partner, or custom)
- **Rule**: Matches incoming event patterns
- **Target**: Destination service (Lambda, SNS, SQS, Step Function, etc.)

---

## ⚙️ How It Works (Flow)

1. **Event generated** (e.g., EC2 stopped)
2. Event lands on an **Event Bus**
3. **Rule** matches the pattern (e.g., `"source": "aws.ec2"`)
4. **Target** is triggered (e.g., a Lambda function runs)

---

## 🚪 Types of Event Buses

| Bus Type      | Description                                |
|---------------|--------------------------------------------|
| **Default**   | Automatically receives AWS service events  |
| **Custom**    | Your app can send events here via API      |
| **Partner**   | For SaaS integrations (e.g., Zendesk)      |

---

## 🎯 Supported Targets (Partial List)

- Lambda
- Step Functions
- SNS
- SQS
- EC2 Run Command
- Kinesis Stream
- ECS Task

---

## ⚠️ Nuances & Edge Cases

- **All AWS services don’t emit events natively** — use CloudTrail or Config for detailed change tracking.
- EventBridge does **not wait for target execution** → async.
- Rules are **region-specific**, and events are processed regionally.
- **Schema Registry** helps you understand event structure — useful for custom events.
- **Event replay** is possible via event archive → new feature!

---

## 📌 Exam Pointers

- “Auto-run Lambda when S3 object created?” → ✅ EventBridge Rule (or S3 trigger)
- “Route SaaS system alert to Lambda?” → ✅ Partner Event Bus
- “Multiple services should act on same EC2 state-change?” → ✅ Fan-out via EventBridge
- “Need serverless workflow based on events?” → ✅ EventBridge + Step Functions

---

## 🔄 Related Services

| Service       | Role                                       |
|---------------|--------------------------------------------|
| CloudTrail    | Logs API calls that **can be used as events** in EventBridge |
| Step Functions | Used as a target to trigger workflows      |
| Lambda        | Used for processing triggered events        |
| SNS/SQS       | Fan-out or buffering of triggered actions   |
