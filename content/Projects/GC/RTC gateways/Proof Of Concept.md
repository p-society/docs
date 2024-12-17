# Real-Time Communication (RTC) Services Gateway Specification

![[Gateways_POC.png]]

[Reference for above diagram](https://youtu.be/exSwQtMxGd4?si=Po0HfmScV2sWFTK2&t=1764) 
## 1) Connection Initiation Gateway

### Objective
The primary goal of this gateway is to establish an initial connection when a user first launches the web application and navigates to a specific sporting event. This connection serves multiple purposes:
- Establish a real-time communication channel
- Send initial client details
- Confirm event selection
- Prepare for subsequent real-time updates

### Data Sent
The initial connection payload is a compact JSON object containing:
- `id`: A unique identifier for the client (potentially a college ID or user identifier)
- `eventId`: Specific identifier for the selected sporting event

```json
{
  "id": "collage id", 
  "eventId": "some Id"
}
```

### Result
- The server acknowledges the connection request
- A dedicated communication channel is opened for the specific event
- Real-time updates for the selected event become available
- Provides analytics on concurrent user engagement
  - Tracks how many users are simultaneously viewing a particular event
- Sets up the foundation for subsequent real-time interactions

## 2) Score Update Mechanism

### Objective
Implement a flexible score update system that:
- Transmits score changes in real-time
- Accommodates diverse sporting event update requirements
- Provides granular, sport-specific data transmission

### Key Considerations
- Update frequency varies by sport:
  - Cricket: Update on every ball
  - Chess: Update on every move
  - Football: Update on goals, fouls, etc.
- Requires adaptive frontend decoding logic

### Data Received
The score update payload will be sport-specific. Example for cricket:

```json
{
  "ball 12": "13/1",
  "comment": "Bumrah has drawn the first blood",
  "batsman": {
    "name": "rohit",
    "runs": "100",
    "balls": "96"
  },
  "bowler": {
    "name": "yuvi",
    "overs": "3.6",
    "runs": "10",
    "maiden": "1",
    "wickets": "2"
  }
}
```

### Result
- Provides live, real-time scoring updates
- Enables rich, detailed event tracking
- Supports immersive user experience

## 3) Reaction Mechanism

### Objective
Enhance user engagement through:
- Live reaction capabilities
- Interactive viewing experience
- Real-time social interaction

### Data Sent
User reaction payload includes:
- `id`: User identifier
- `emoji`: Emotional response
- `comment`: Optional text commentary

```json
{
  "id": "userId",
  "emoji": ":)",
  "comment": "lesssgoooo"
}
```

### Result
- Increases viewer interaction
- Creates a more dynamic, social viewing environment
- Allows instant emotional expression during events

## 4) Heartbeat/Ping-Pong Connection Maintenance

### Objective
Implement a robust connection monitoring mechanism to:
- Verify active user connections
- Prevent unnecessary resource allocation
- Manage connection lifecycle efficiently

### Recommended Implementation Strategies
Drawing insights from:
- [Reconnecting WebSocket Library](https://github.com/joewalnes/reconnecting-websocket)
- [WebSocket Connection Loss Handling](https://stackoverflow.com/questions/26971026/handling-connection-loss-with-websockets)

### Proposed Mechanism
- Frontend: Implement continuous ping messages in a loop
- Server: Monitor ping frequency
- Disconnect protocol:
  - If no ping received within a designated timeframe
  - Assume client connection lost
  - Gracefully close the connection

### Result
- Optimized resource management
- Reduced server load
- Improved connection stability
- Efficient handling of intermittent network conditions
