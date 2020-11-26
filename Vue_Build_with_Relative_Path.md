vue env: Vue_CLI 3.4.x

## change vue.config.js

in ```vue.config.js```
```
  publicPath: "./",
```
this will use relative path in the **index.html**
```
<link href="css/app.5e9efa5f.css" rel="stylesheet">
<script src="js/app.a5cf622e.js">
```

## avoid using '/' startwith the router path
using as following
```
            thiz.$router.replace(`monitor`);
```

don't use
```
            thiz.$router.replace(`/monitor`);
```
