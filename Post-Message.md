# Post Message
It is a way for web applications to overcome SOP restriction and communicate with different domain.

# How Post Message Works
- It uses javascript to send message and listen for incomming message 
- Main window opens a child window and both can comminicate with each other

### Parent Window Example Code
```javascript
var emial = "rahim@test.com"
var child_url = "https://paymentreciever.com"
function getpayment(){
var ref=window.open(child_url,"pop","width=450,height=350,resizeable=1");
ref.postMessage(email,"paymentreciever.com");
}
```

### CHild Window Example Code
```javascript
window.addEventListner('message',msgHandler);
fuction msgHandler(event){
if(event.origin == "parentdomain.com"){
document.write("You Email is "+ event.data);
document.write("Proceed to payment");
}
```

## Bugs
- Child Window Dosen't verity origin 
Attacker can open that window and send message / payload

- Attacker can get data from child window / credentials. if parent origin is not verified
```javascript
function sendMessage(){
var pass = "Secret123"
window.opener.postMessage(credentials,"parentdomain.com")
window.close()
}
```

