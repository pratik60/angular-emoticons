

Originally forked from  http://github.com/JangoSteve/jQuery-CSSEmoticons

In the HTML file we have declared a html app post . The controller PostController from the javascript file is given an alias post. Include the required javascript, css files.The javascript snippet which could also be included as a file (app.js) is described below. 

The css file required essentially for the special emoticons is image-emoticon-png-gif.css. 

The angular-png-gif-emoticon.js is the filter. This file has to be defined after including the javascript snippet in app.js. The msg variable contains the raw format of the text which has to be emoticonized.

index.html
```HTML
<!DOCTYPE html>
<html ng-app="post">
  <body  ng-controller="PostController as post.min.js"></script>
    <script type="text/javascript" src="app.js"></script>
    <link rel="stylesheet" type="text/css" href="image-emoticon-png-gif.css" />
    <script type="text/javascript" src="angular-png-gif-emoticon.js"></script>
    <div class="message" ng-bind-html="msg | emoticonize:showEmoticons"></div>
  </body>
</html>
```

In the javascript file declare a controller corresponding to a module. Here we have defined the StoreController corresponding to the angular module store and stored inside the variable app. The emoticonizeFilter is the filter required for converting the text to emoticons. The parameters to the function defined within the controller are scope and sce. The scope is used to define the initial value of the bool variable showEmoticons as well as to store the message that needs to be converted.The sce is used to convert the user text into text that can be trusted as HTML. A self call on this function is performed.

app.js
```javascript 
(function() {
  var app=angular.module('post',['emoticonizeFilter']);
  
  app.controller('PostController',function($scope, $sce){
   
   $scope.msg= $sce.trustAsHtml("This is an interesting post   :-) <br/>=D");
   $scope.showEmoticons = true;
  });
}).call(this);
```

  In the angular-png-gif-emoticon.js file we take the user text as the input and try matching it with the pre-defined emoticons using regular expressions. If any such symbol is found it is replaced with the corresponding emoticon.The displayed message contains the emoticons. This works for  two character emoticons, three character emoticons as well as special emoticons.
