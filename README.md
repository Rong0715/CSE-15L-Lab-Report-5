# A Review on Lab Report 2: StringServer
Lab Report 2 is by far the most interesting lab report for me. It offers a simple and thought-provoking perspective on how much we can do with the knowledges that we currently know -- I used to think after taking several Java programmimg courses all I can do was writing bunch of for loops and making sure my code output matches the sample output on the assignment instruction. But after this report and its corresponding lab, I understand, for the first time operating one myself, how powerful servers are as tools for us to store data, interact with other people, and develop interesting functions with fairly high potential.
### What did I do in Lab Report 2?
In this report, I wrote a web server called `StringServer` that keeps track of a single string that gets added to by incoming requests using path like this:
`/add-message?s=<string>`.
The code I wrote to in order to perform as purpose is below:
``` Java
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {

    String dialogue = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("It's an empty path.");
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    dialogue += "\n" + parameters[1];
                    return dialogue;
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

The `Handler` class contains operations to process the given URL. It firstly gets the path part of the URL, and check if it's equal to `"/"`, which means the path is empty. If so, the message `"It's an empty path."` will be printed on the screen. If the path contains further information, the program moves on to check if the path contains the sub string `"/add-message"` which is used by the user to prompt the program to perform add-message task.
