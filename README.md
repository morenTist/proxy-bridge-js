# proxy-bridge-js
*** make your site (host) a proxy ** 

```js
const proxy = require('express-http-proxy');
const app = require('express')();
const port = process.env.PORT || 3000;

// for test make the root of the site on get request 
// will return the succuss msg
// it's optional
app.get("/",(req,res)=>res.send(" the route page "));

 // the route that you wnat tobe the proxy
// by default is the /proxy 
const proxyRoute = "/proxy";

// proxy Handler
app.use(`${proxyRoute}*`, (req,res,next)=>{
  //removeing extra pass
	const url = (req)=>req.originalUrl.replace( new RegExp(`/\/?${proxyRoute}\/?/`,"i"),"");
	// send through the proxy
  return proxy(url(req) ,{proxyReqPathResolver:url })(req,res,next);
});

// your code here
// ... 

app.listen(port);


```
