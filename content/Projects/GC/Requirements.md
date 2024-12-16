##  1 ) Connection initiation gateway

#### Objective
- Upon first time of launching the web app and navigating to desired sporting event an connection will be initiated with sever along with initial client details and selected sport.
#### Data Sent
- ``` {"id":"collage id", "eventId":"some Id"} ```
#### Result
- The initial one way request is sent and the server acknowledge the sent request and will sent the updates of request event on that channel.
- This can also help in gathering statics in real time as how many people are live on this particular event.
## 2 ) Score
#### Objective
- To send the difference of changes in scores of the requested event.
- This will also depend on various sport events as all have a different condition for updating score or more precisely sending data. For example in cricket update is sent upon every ball, in chess upon every move and moreover the data sent is also vastly different.
- The frontend has to decode the received data.
#### Data Received
- Depend upon sport.
- Example Cricket :- ``` {"ball 12":"13/1","comment" : "Bumrah has drwan the first blood","batsman" : {"name" : "rohit","runs":"100",balls : "96"},"bowler":{"name":"yuvi","overs":"3.6","runs":"10","maiden":"1","wickets":"2"}}```
#### Result
- User will get live updates 
## 3 ) Reaction 
#### Objective
- To allow the viewers to react live and become more engaging.
#### Data Sent
- ``` {"id":"userId","emoji":":)","comment":"lesssgoooo"}```
#### Result
- Game will become more engaging.
## 4 ) Heartbeat or Ping Pong
#### Objective
- To check if the user is still connected and active or not.
#### Data Sent
- https://github.com/joewalnes/reconnecting-websocket 
- https://stackoverflow.com/questions/26971026/handling-connection-loss-with-websockets
- Using above two article we can implement a constant message ping action in a loop from frontend and server needs to check if for some designated time that is not received then client has probably dropped off and connection can be closed if not closed by client.
#### Result
- Wasting of resources will be prevented.
