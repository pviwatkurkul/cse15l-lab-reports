# Lab Report 2 #
## **Creating a Search Engine on a Local/Remote Web Server** ##


* This lab will contain the explanation of integrating a search engine into a local/remote webserver and also the debugging of bugs and how to identify them.

* First, we're going to start with the implementation of a search engine and how it was done with a concise walkthrough of the code.
~~~ 
{
    class Handler implements URLHandler {
        ArrayList<String> word = new ArrayList<String>();
        String searched = new String();
        String substrng = "";
        public String handleRequest(URI url) {
            if (url.getPath().equals("/")) {
                return String.format("No string");
            } else if (url.getPath().equals("/search")) {
                String[] parameters1 = url.getQuery().split("=");
                    if (parameters1[0].equals("s")) {
                        substrng = parameters1[1];
                    for (int i = 0; i< word.size(); i++){
                            if (word.get(i).contains(substrng)){
                                searched += (word.get(i) + " ");
                        }
                    }
                    return String.format(searched);
                }
                return "404 Not Found";
            } else {
                System.out.println("Path: " + url.getPath());
                if (url.getPath().contains("/add")) {
                    String[] parameters = url.getQuery().split("=");
                    if (parameters[0].equals("s")) {
                        word.add(parameters[1]);
                        return String.format("String added");
                    }
                }
                return "404 Not Found!";
            }
    }
}         
~~~


**Add String** 

* Adding a String to the list is fundamental in being able to search/test the code so with the picture down below, it is shown that adding through the url is successful.
![Image](addused.png)

* To break down what is exactly happening we can break down the code by parts.

~~~
{
    System.out.println("Path: " + url.getPath());
        if (url.getPath().contains("/add")) {
}
~~~

* The url.getPath() method is called from the URLClasshandler which will obtain the path from the link and check for /add which prompts that adding a string is about to happen.

~~~
{
    String[] parameters = url.getQuery().split("=");
        if (parameters[0].equals("s")) {
            word.add(parameters[1]);
            return String.format("String added");
        }
    }
    return "404 Not Found!";
}
~~~

* What's happening next is that getQuery() is gonna obtain the next piece of the url such as when ? is apart of the code. 

* By using getQuery().split("="), the left side of = and right side will be split into an array where it can be accessed through indexing of an array. To prompt the adding of a string, it checks for an "s" on the left side of = and a string on the right side.

* Next the string on the right side of = will be added to **word** which is a String ArrayList that will store the strings that are added into the webserver.

* If the url does not contain an /add, s, or a string. A string error will be outputted such as "404 Not Found!";

**Search for String**

![Image](searchused.png)

* We're now gonna be focusing on the search part of the search engine.

~~~
{
       public String handleRequest(URI url) {
            if (url.getPath().equals("/")) {
                return String.format("No string");
}
~~~
* This code is gonna utilize the .getPath() method to obtain the url from the passed in parameter.
* url.getPath() is gonna check if the url contains a "/" and if it does it's gonna return a string statement as "No string" as its default.

![Image](default.png)

~~~
{
    else if (url.getPath().equals("/search")) {
                String[] parameters1 = url.getQuery().split("=");
                    if (parameters1[0].equals("s")) {
                        substrng = parameters1[1];
                    for (int i = 0; i< word.size(); i++){
                            if (word.get(i).contains(substrng)){
                                searched += (word.get(i) + " ");
                        }
                    }
                    return String.format(searched);
                }
}
~~~

* Going down the list of code for the search method block, we can see that url.getPath() is gonna continue to look through the URL to check for the prompt to search.

* As you can see it's gonna look for the string "/search", which shows that the user is going to search something.

* Once that substring is located, the rest of the code will run. String[] parameters1 is a string list that will contain a string as a element on the left side of a "=".

* In this case we want to use "s=(whattosearch)" to indicate that we want to look for a set of strings that contain that search word. 

* Therefore, parameters[0] will store "s" and parameters[1] will store the substring we want to search for.

* Next using a for loop we're going to loop through the **word** ArrayList that will contain the strings that are added and see if the substring is contained within the list of strings.

* If a string is found that matches the conditional, it will be added to the String list, **search**, which will be returned after all the strings are found and added.

* String.format() will return the string list, displaying to the user what has been found with their search.

## No Query Found ## 

![Image](wrongquery.png)

* We always want to consider the chance that something shouldn't be inputted or when a bug occurs. That's we want to prompt the user that something went wrong with the code or their input is invalid.

* For this case, we use ? to indicate that a query is contained with the URL. 
 
~~~ 
{
      for (int i = 0; i< word.size(); i++){
                            if (word.get(i).contains(substrng)){
                                searched += (word.get(i) + " ");
                        }
                    }
                    return String.format(searched);
                }
                return "404 Not Found";
}
~~~

~~~
{
      if (parameters[0].equals("s")) {
                        word.add(parameters[1]);
                        return String.format("String added");
                    }
                }
                return "404 Not Found!";
            }
}
~~~

* As you can see with the implementation of add and search, we always make sure to have an else statement incase there's a chance that the input is not what we want.

* With the picture above there is a ? but nothing to follow the indication of a query. That's where we want to throw an error statement because that's not what we want or looking for. 

* For the implementation using an else statement to complement the if statement is useful in that if the statement returns false it will immediately return the erorr message.

**This concludes the implementation of a search engine within a web server**