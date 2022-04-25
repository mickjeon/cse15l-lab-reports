# Lab Report 2, Week 4
[Back to index page](https://mickjeon.github.io/cse15l-lab-reports/)

## Code changes to fix bugs in Markdown Parser

### 1. First Failure-Inducing Input
* Screenshot of the code change:
![Code Cahnge 1](error_1.png)
* [Link](https://github.com/mickjeon/markdown-parser/blob/main/my-file.md?plain=1) to failure-inducing input file.
* Symptom: 
```
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
        at java.base/java.util.Arrays.copyOf(Arrays.java:3512)
        at java.base/java.util.Arrays.copyOf(Arrays.java:3481)
        at java.base/java.util.ArrayList.grow(ArrayList.java:237)
        at java.base/java.util.ArrayList.grow(ArrayList.java:244)
        at java.base/java.util.ArrayList.add(ArrayList.java:454)
        at java.base/java.util.ArrayList.add(ArrayList.java:467)
        at MarkdownParse.getLinks(MarkdownParse.java:19)
        at MarkdownParse.main(MarkdownParse.java:29)
```
* The symptom of this first failure inducing input is that the while loop inside the getLinks() method falls into an infinite loop. The failure inducing input has a new line at the end of the first line and triggers the infinite loop. The bug is that the terminating condition is not met inside the while loop and I fixed it by adding a condition to break the while loop.

### 2. Second Failure-Inducing Input
* Screenshot of the code change:
![Code Change 2](error_2.png)
* [Link](https://github.com/mickjeon/markdown-parser/blob/main/image.md?plain=1) to failure-inducing input file.
* Symptom: 
```
 Output: [image.png]
 // The output should be [] to not include the image link.
```
* The symptom of this second failure inducing input is that MarkdownParse.java outputs the an image link while it's not supposed to. The failure inducing input has an image link in the .md file. In order to fix a bug where it prints out an image link, I added a condition to disregard an image link using "!" detection.

### 3. Third Failure-Inducing Input
* Screenshot of the code change:
![Code Change 3](error_3.png)
* [Link](https://github.com/mickjeon/markdown-parser/blob/main/far-away.md?plain=1) to failure-inducing input file.
* Symptom: 
```
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: begin 0, end -1, length 18
        at java.base/java.lang.String.checkBoundsBeginEnd(String.java:4601)
        at java.base/java.lang.String.substring(String.java:2704)
        at MarkdownParse.getLinks(MarkdownParse.java:26)
        at MarkdownParse.main(MarkdownParse.java:39)
```
* The symptom of this third failure inducing input is that an error occurs when an .md file does not contains any link. The failure inducing input only has a Heading and a bold text. In order to fix this bug, I added a condition in which "[", "]", "(", ")" are not included in the .md file, I terminate the while loop as soon as it is entered.
