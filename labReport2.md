## Lab Report 2

**Code for ChatServer.Java** 
```
import java.io.IOException;
import java.net.URI;
import java.io.*;
import java.util.*;

class Handler implements URLHandler {
    ArrayList<String> messages = new ArrayList<>();
    
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Please enter a message in the search bar";
        } else if (url.getPath().equals("/add-message")) {

            String[] parameters = url.getQuery().split("&");

            String user = null;
            String message = null;

            for (String pair : parameters) {
                String[] values = pair.split("=");
                if (values.length == 2) {
                    String key = values[0];
                    String value = values[1];

                    if ("s".equals(key)) {
                        message = value;
                    } else if ("user".equals(key)) {
                        user = value;
                    }
                }
               
            }

             if (message != null && user != null) {
                String finalMessage = user + ": " + message;
                messages.add(finalMessage);
                return String.format("%s",String.join("\n", messages));
        
            } else {
                return "Invalid parameters!";
            }
        }

        return "404 Not Found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

**Screenshots of `/add-message` in action!**

ADD SCREENSHOTS

The methods that are called in my code are 
* The main method
* The handleRequest method

The relevant argument for this screenshot is the `"/add-message"` 

