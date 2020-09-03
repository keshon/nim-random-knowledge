## How to getPostParams in Prologue if POST params are sent by fetch

Ok the quick answer is to use 'application/x-www-form-urlencoded;charset=UTF-8' as Content-Type and encode payload as query string:

### Front-end side
```
// Read input values (jQuery example)
let payload = {
    'name': $('#name').val(),
    'email': $('#email').val(),
    'message': $('#message').val()
};

//Encode the data
const formData = Object.keys(payload).map((key) => {
    return encodeURIComponent(key) + '=' + encodeURIComponent(payload[key]);
}).join('&');

// Make post request to Prologue's endpoint
fetch('/endpoint', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded;charset=UTF-8'
    },
    body: formData
})
.then((response) => {
    return response.json();
})
```

### Back-end side ###

```
import 
    prologue

let env = loadPrologueEnv(".env")
let settings* = newSettings(
        appName = env.getOrDefault("appName", "Prologue"),
        debug = env.getOrDefault("debug", true),
        port = Port(env.getOrDefault("port", 8787)),
        staticDirs = [env.get("staticDir")],
        secretKey = env.getOrDefault("secretKey", "")
    )
    
var app = newApp(settings = settings, middlewares = @[debugRequestMiddleware(), compileStyles()])

# This is back-end route
proc endpointRouteExample(ctx: Context) {.async.} =

    # Read posted values
    let 
        name = ctx.getPostParams("name")
        email = ctx.getPostParams("email")
        message = ctx.getPostParams("message")

    echo name
    echo email
    echo message
    echo body


app.addRoute("/endpoint", endpointRouteExample,  @[HttpPost])

app.run()

## Why it is important?
Because passing values via `FormData` type or as `multipart/form-data` or as `application/json` just won't work
