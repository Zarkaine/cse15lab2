## This is lab report #2

# Part 1:StringServer
First I had to create the server. I did this with the method given before for numberServer. I created an int called port, and called Server.start(port, new StringServerHandler()); StringServerHandler implements URLHandler. It has 3 instance variables, 2 arrayLists and one String. StringServerHandler has a single method, handleRequest. This method returns a String, and takes a URI as the argument. If the user adds "/add-message?s=<string>" to the url, it will then display the string, as shown below.
 
![Image](https://github.com/Zarkaine/labreport2/blob/main/images/firstAdd.png)
 
I have an if statment checking if /add-message is in the url, then adds the string following the s to the arrayList. Then it copies it to the string, and returns the string. 

![Image](https://github.com/Zarkaine/labreport2/blob/main/images/secondAdd.png)
 
 This is the second message. After using /add-message a second time, it displays it & the previous messages. I originally had an issue where it would re-add previous add-messages to the string. So if you called "first", "second", and "third", it would display "first first second first second third". I resolved this by adding an if statment, so the each item from the arraylist would only be added once. There may have been a simpler/better way to do this, but I have a migraine & Im definitely out of time.
  
  
The relevant arguments for this methods were
  
  
No values got changed because each time add-message was called, if parameter[0] was "s", then parameter[1] was added to the arrayList. Then to the string, and the string was returned. The only value that would've been changed is the string that comes after /add-messsage?s=<string>.

  
#Part 2: Bugs from lab3
  
When I tried running testReserve, it failed and gave return "arrays first differed at element [0]; expected:[4] but was:[0]"
![Image](https://github.com/Zarkaine/labreport2/blob/main/images/reverseTestFail.png)
  

Because the code was
  `
  static int[] reversed(int[] arr) {
  
        int[] newArray = new int[arr.length];
  
        for (int i = 0; i < arr.length; i += 1) {
                                         
            arr[i] = newArray[arr.length - i - 1];
                                         
        }
                                         
        return arr;
                                         
    }
                                       
                                       
This code was failing because it was trying to copy the elements of newArray to arr. But all elements of newArray are 0. It was also returning arr when it was supposed to return newArray. To fix this, I simply swapped arr and newArray in the for loop, and returned newArray.
       `                                 
  int[] newArray = new int[arr.length];
                                        
    for (int i = 0; i < arr.length; i++) {
  
      newArray[i] = arr[arr.length - i - 1];
  
    }
  
    return newArray;`
  
  
So now, the elements in arr were being copied into newArray (in reverse order), and newArray was being returned.
  
#Part 3: I learned a lot this week. For one, I learned how to make a server in java and use the URI methods. I also learned how to use Junit tests which I can only imageine would be very helpful. 
