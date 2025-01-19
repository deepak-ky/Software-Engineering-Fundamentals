

---


```

final String CRLF = "\n\r"; //Carriage Return, Line Feed - ASCII characters 10 and 13  
/*  
* A carriage return, sometimes known as cartridge return and often shortened as CR, <CR> or return is a  
* control character or mechanism used to reset a device's position to the beginning of a line of text.  
*  
* /r/n or /n/r  
* */  
  
String response =  
    "HTTP/1.1 200 OK" // Status Line : HTTP_VERSION RESPONSE_CODE RESPONSE_MESSAGE  
    + CRLF  
    + "Content-Length: " + html.getBytes().length // HEADER  
    + CRLF + CRLF  
    + html  
    + CRLF + CRLF  
    ;
    
```