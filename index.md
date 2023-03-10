## This is lab report #2 (update 8)

# Part 1: StringServer
First I had to create the server. I did this with the method given before for numberServer. I created an int called port, and called Server.start(port, new StringServerHandler()); StringServerHandler implements URLHandler. It has 3 instance variables, 2 arrayLists and one String. StringServerHandler has a single method, handleRequest. This method returns a String, and takes a URI as the argument. If the user adds "/add-message?s=<string>" to the url, it will then display the string, as shown below.
 
![Imgur1](https://imgur.com/ZcMZImS.png)
 
I have an if statment checking if /add-message is in the url, then adds the string following the s to the arrayList. Then it copies it to the string, and returns the string. 

![Imgur2](https://imgur.com/1BpXJcK.png)
 
 This is the second message. After using /add-message a second time, it displays it & the previous messages. I originally had an issue where it would re-add previous add-messages to the string. So if you called "first", "second", and "third", it would display "first first second first second third". I resolved this by adding an if statment, so the each item from the arraylist would only be added once. There may have been a simpler/better way to do this, but I have a migraine & Im definitely out of time.
  
  
The relevant arguments for the method handleRequest was a URI
  
  
No values got changed because each time add-message was called, if parameter[0] was "s", then parameter[1] was added to the arrayList. Then to the string, and the string was returned. The only value that would've been changed is the string that comes after /add-messsage?s=<string>.

  
# Part 2: Bugs from lab3
  
I tested reversed(int[] arr) with the default testReverse()
 
 <pre><code>
 @Test
  public void testReversed() {
    int[] input1 = { 1, 2, 3, 4 };
    assertArrayEquals(new int[] { 4, 3, 2, 1 }, ArrayExamples.reversed(input1));
  }
</code></pre>
 
But as shown below, it failed and gave return "arrays first differed at element [0]; expected:[4] but was:[0]"
![Imgur3](https://imgur.com/NY6AC99.png)

 But if you changed the input to just 0s, it would pass
  <pre><code>
  @Test
  public void ogtestReversed() {
    int[] input1 = { 0, 0, 0, 0 };
    assertArrayEquals(new int[] { 0, 0, 0, 0 }, ogArrayExamples.reversed(input1));
  }
  </code></pre>
  
Before any changes, it looked like this:
  
 <pre><code> 
  static int[] reversed(int[] arr) {
  
        int[] newArray = new int[arr.length];
  
        for (int i = 0; i < arr.length; i += 1) {
                                         
            arr[i] = newArray[arr.length - i - 1];
                                         
        }
                                         
        return arr;                                 
    }
   </code></pre>
         
There were two bugs in this. The first bug for this code was copying from newArray to arr instead of arr to newArray. The symptom that resulted was having the incorrect values, in this case null.  The second bug was returning the wrong array. After creating a new array that is the reverse of the first, we wanted to return the new array, but instead the original array is returned. The symptom of this is simply incorrect output, even if the first bug is fixed.
                                       
To fix the first bug, I simply swapped arr & newArray in the for loop. To fix the second bug, I changed the return statment to return the newArray. These changes are shown in the code below:
                                       
  <pre><code>                             
  int[] newArray = new int[arr.length];
                                        
    for (int i = 0; i < arr.length; i++) {
  
      newArray[i] = arr[arr.length - i - 1];
  
    }
    return newArray;`
 </code></pre>
  
So now, the method fufills the intended purpose of creating & returning a new array that is the reverse of the original. This is because it copies the elements of arr into newArray properly, and returns newArray as intended.
  
# Part 3: What I learned
I learned a lot this week. For one, I learned how to make a server in java and use the URI methods. I also learned how to use Junit tests which seems to be very helpful. The types of errors that I can catch using Junit tests are what usually send me to the cse basement for tutors, which usually have a long wait. So now I can solve more issues on my own, and reduce the amount of time I stare at Gradescope in frustration.
