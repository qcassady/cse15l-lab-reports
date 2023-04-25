# Lab 2  
## Part 1  
![Image](stringserver.png)  
![Image](server1.png)  
First I started off with just adding Hello, which calls my handlerequest method. The input to this is a URI and is what determines what is added to the string output or whether a 404 error is called. Before calling the method, the result string is empty. After calling the method, the word "Hello\n" gets added to the result string. The handleRequest is being fed the URI of "localhost:4000/add-messsage?s=Hello".  
![Image](server2.png)  
Next I replaced Hello with Howdy for my URI. This also calls the handleRequest method, but instead of starting off with an empty result string we start off with the previously added "Hello\n" and add onto it from there. After feeding "localhost:4000/add-messsage?s=Howdy" into the handleRequest method, we add "Howdy\n" onto the result string and return it once again. The result string is now "Hello\nHowdy\n".  
## Part 2  
I chose the ReverseInPlace method from the ArrayExamples file. A failure-inducing input for the program is  
  
@Test  
  public void testReversedInPlaceMultiple() {  
    int[] input2 = {1,2,3};  
    ArrayExamples.reverseInPlace(input2);  
    assertArrayEquals(new int[]{ 3,2,1 }, input2);  
  }  
An input that did not induce failure is  
@Test  
	public void testReverseInPlaceSingle() {  
    int[] input1 = { 3 };  
    ArrayExamples.reverseInPlace(input1);  
    assertArrayEquals(new int[]{ 3 }, input1);  
	}  
