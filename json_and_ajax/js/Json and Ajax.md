##Json = Object + Array
###Java Script Object Notation 
javascript 的Object
```javascript
var mycat = {
    "name": "kitty",
    "species": "cat",
    "favFood": "fish"
} 
```
javascript 的Array
```javascript
var myFavColors = ["yello", 'blue', 'red'];
```
javascript 的Json = Object + Array
```javascript
var thePets = [
    {
        "name": "kitty",
        "species": "cat",
        "favFood": "fish"
    },
    {
        "name": "Barky",
        "species": "dog",
        "favFood": "carrots"
    }
]
```
----------
##Ajax
###Asynchronous JavaScript And XML
```javascript
var ourRequest = new XMLHttpRequest();
ourRequest.open('GET', 'https://learnwebcode.github.io/json-example/animals-1.json');
ourRequest.onload = function() {
    var ourDate = JSON.parse(ourRequest.responseText)
    console.log(ourDate[0]);
};
ourRequest.send();
```
-------------
##Ajax请求Json数据并渲染网页
```javascript
var animalContainer = document.getElementById("animal-info");
var btn = document.getElementById("btn");

btn.addEventListener("click", function() {
    var ourRequest = new XMLHttpRequest();
    ourRequest.open('GET', 'https://learnwebcode.github.io/json-example/animals-1.json');
    ourRequest.onload = function() {
        var ourDate = JSON.parse(ourRequest.responseText)
        renderHTML(ourDate)
    };
    ourRequest.send();
});


function renderHTML(data) {
    var htmlString = '';

    for (i=0; i<data.length; i++) {
        htmlString += '<p>' + data[i].name + 'is a ' + data[i].species + '.</p>'
    };

    animalContainer.insertAdjacentHTML('beforeend', htmlString);
};
```

------
##循环数据，处理异常
```javascript
var pageCounter = 1
var animalContainer = document.getElementById("animal-info");
var btn = document.getElementById("btn");

btn.addEventListener("click", function() {
    var ourRequest = new XMLHttpRequest();

    ourRequest.open('GET', 'https://learnwebcode.github.io/json-example/animals-' + pageCounter + '.json');
    
    ourRequest.onload = function() {
        if (ourRequest.status >= 200 && ourRequest.status<400) {
            var ourDate = JSON.parse(ourRequest.responseText);
            renderHTML(ourDate);    
        }else{
            console.log("We try to connect the server, but is return an error ");
        }        
    };

    ourRequest.onerror = function() {
        console.log("Connection error")
    };

    ourRequest.send();

    pageCounter++;

    if (pageCounter > 3) {
        btn.classList.add("hide-me")
    }
});


function renderHTML(data) {
    var htmlString = '';

    for (i=0; i<data.length; i++) {
        htmlString += '<p>' + data[i].name + 'is a ' + data[i].species + ' that likes eat ' 

        for (ii=0; ii<data[i].foods.likes.length; ii++) {       
            if (ii==0) {
                htmlString += data[i].foods.likes[ii];
            }else{
                htmlString += ' and ' + data[i].foods.likes[ii];
            };
        }

        htmlString += '  and dislikes '

        for (ii=0; ii<data[i].foods.dislikes.length; ii++) {        
            if (ii==0) {
                htmlString += data[i].foods.dislikes[ii];
            }else{
                htmlString += ' and ' + data[i].foods.dislikes[ii];
            };
        }
    };

    htmlString += '.</p>'

    animalContainer.insertAdjacentHTML('beforeend', htmlString);
};
```

