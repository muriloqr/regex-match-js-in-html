# regex-match-js-in-html
A regex to match/avoid JS in HTML. (May not be fully guaranteed)

#### Regex
##### JS
~~~js
/(<script[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>)|(((?<=\<))?((on.+?)([ ]+)?=([ ]+)?["']?((?:.(?!["']?\s+(?:\S+)=|[>"']))+.)["']?)((?=\>))?)|(on.+?)\w+/gi
~~~
##### Java
~~~java
(<script[^<]*(?:(?!<\\/script>)<[^<]*)*<\\/script>)|(((?<=\\<))?((on.+?)([ ]+)?=([ ]+)?[\"']?((?:.(?![\"']?\\s+(?:\\S+)=|[>\"']))+.)[\"']?)((?=\\>))?)|(on.+?)\\w+|(action)|(method)
~~~

### Usage for Javascript
#### Example
~~~js
let maliciousHtml = `
  <div onmouseover="window.location.reload()">
    <h1> Hello, there is a html!<h1>
    
    <script>
      // Malicious code
      let pwd = prompt("Write your password here:");
      
      // EXAMPLE: REQUEST TO A WEBSERVER
    </script>
  </div>
`
let safeHtml = maliciousHtml.replace(/(<script[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>)|(((?<=\<))?((on.+?)([ ]+)?=([ ]+)?["']?((?:.(?!["']?\s+(?:\S+)=|[>"']))+.)["']?)((?=\>))?)|(on.+?)\w+/gi, "")
// safeHtml now is:
//  <div >
//    <h1> Hello, there is a html!<h1>
//    
//    
//  </div>

~~~

### Usage for Java
#### Example
~~~java
String maliciousHtml = "<div onmouseover=\"window.location.reload()\"><h1> Hello, there is a html!<h1><script>let pwd = prompt(\"Write your password here:\"); </script>  </div>";

String safeHtml = maliciousHtml.replaceAll("(<script[^<]*(?:(?!<\\/script>)<[^<]*)*<\\/script>)|(((?<=\\<))?((on.+?)([ ]+)?=([ ]+)?[\"']?((?:.(?![\"']?\\s+(?:\\S+)=|[>\"']))+.)[\"']?)((?=\\>))?)|(on.+?)\\w+|(action)|(method)", "");

// safeHtml now is: <div ><h1> Hello, there is a html!<h1>  </div>

~~~
