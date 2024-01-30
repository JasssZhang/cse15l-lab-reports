# Lab Report 2
*Jasmine Zhang A17371205*
## Part 1
ChatServer code
```
import java.io.IOException;
import java.net.URI;

// adds text message in the form <user>: <message>
class Handler implements URLHandler {

    //create new string outside method
    //otherwise it would be renewed everytime we run the method
    String storeString = "";
    public String handleRequest(URI url){
        if (url.getPath().equals("/")){
            return storeString;
        } else{
            if (url.getPath().contains("/add-message")){
                //get url after ? and split by &
                //store in input String array
                String[] input = url.getQuery().split("&");
                //split the two strings seperately
                //store in message and user String array
                String[] message = input[0].split("=");
                String[] user = input[1].split("=");
                //Strings we need are stored in user[1] and message[1]
                String result = String.format(user[1] + ": " + message[1] + "\n");
                
                //store result in String
                //return string
                storeString += result;
                return storeString;
            }
        }
        return "404 not found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length ==0){
            System.out.println("Missing port number. Please try again.");
            return;
        }
        //get port number and typecast into integer
        int portNum = Integer.parseInt(args[0]);
        //start server
        Server.start(portNum, new Handler());
    }
}
```

Screenshot 1

![Image](L2S2.png)

Here, I typed "/add-message?s=hello&user=jasmine" as input arguments in url block. This would call the handleRequest(URL url) method, and would specifically run the "else if" part of my code. This method takes in "/add-message?s=hello&user=jasmine" as an argument. Relevant field to this method is the String storeString, which is created to store the values of <user>: message in each call of the method. From this specific request, the length of the String is incremented by one. The value of the string changed as one element: "jasmine: hello" is added. The storeString is now {"jasmine: hello"}.


Screenshot 2

![Image](L2S3.png)

Here, I entered "/add-message?s=How are you&user=jzhang" as input arguments in the url block. Same as the first screenshot, handelRequest(URI url) method is called. The relevant argument to this method is "/add-message?s=How are you&user=jzhang". String storeString is a relevant field. From this specific request, length of this string is changed to 2, and a new element is added to the string to change its value, which is "jzhang: How+are+you". The storeString is now {"jasmine: hello", "jzhang: How+are+you"}.

## Part 2

Show with ls
![Image](L2S4.png)
Both private and public key are stored in directory .ssh. Private key is stored in id_ed25519 while public key is stored in file id_ed25519.pub

![Image](L2S4a.png)
The path for private key is /home/.ssh/id_ed25519

The path for public key is /home/.ssh/id_ed25519.pub 


Terminal interaction without password

![Image](L2S5.png)

Here, once I've stored my public ssh key within the .ssh directory on my remote account, I was asked to enter my password. When I try to log in after this, I was able to log in directly, without being asked for a password.


## Part 3
In week 2 lab, I've learnt that I can connect my laptop to another computer by using the command *ssh user@ieng6.ucsd.edu*, which I did not know before. By using this command and typing in my student account password upon log in, I was able to connect my laptop to a computer in CSE basement that would act as a server to run any commands that I run on my own laptop. 

I've also learnt that we can write codes to create a webpage, and we can access certain paths and codes with the url bar on our browser. By changing the url and entering certain commands encoded in the code block, we would be able to run the program accordingly and edit the webpage itself.

One thing I've also learnt is that we can clone codes in github repository to our own workspace with this command: "git clone <url>". This is really useful for editing certain code blocks.
