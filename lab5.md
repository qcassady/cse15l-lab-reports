# Lab 5  
## Original Post  
I am using my personal laptop, running Windows 10, and using VisualStudioCode to do my programming.  
My `grade.sh` file is supposed to `echo` "Full Score!" when you pass all the tests, but instead of doing so it says "1/1" instead. The x/1 is meant to be reserved for the repositories that fail one or more tests, but I can't seem to figure out what to change to get this to work properly.  
It runs fine with any of the repositories that fail a test, such as `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3` where it says `0/1` like it should, but for a correct repository such as `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected` it will say `1/1` instead of `Full Score!`. Any help would be greatly appreciated!  
![lab5sc1](https://github.com/qcassady/cse15l-lab-reports/assets/130010365/f3f9665f-3250-44f4-899c-0af00740460f)  
## TA Response  
Have you checked your `score.txt` file to what it contains in the case of a perfect score?  
## Student Response  
Thank you very much! I realized that there was still a line in the file even thought it was empty, so the length would still be nonzero. I fixed this by swapping from `temp.length` to the much better `-s score.txt`, which properly checks to see if the file is empty for my purposes. Thanks for the advice!  
![Screenshot 2023-06-05 174203](https://github.com/qcassady/cse15l-lab-reports/assets/130010365/fd51929c-465e-4f97-95f1-2fc4c9349c18)  
## Setup Information  
You need the file structure of:  
![image](https://github.com/qcassady/cse15l-lab-reports/assets/130010365/1dd19468-58df-4c03-9a66-7d55321980ff)  
Before any edits, the code of the relevant file (`grade.sh`) was:  
~~~
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

if [[ -f student-submission/ListExamples.java ]]
then
    cp -r student-submission/ListExamples.java grading-area
    cp -r lib grading-area
    cp -r TestListExamples.java grading-area
else 
    echo "File not found!"
    exit 1
fi

cd grading-area
javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java
java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore TestListExamples > results.txt
grep 'Tests run:' results.txt > score.txt
temp=$(cat "score.txt")
num=${temp:11:1}
if [[ temp.length == 0 ]]
then 
    echo "Full Score!"
else
    echo $((1-num))"/1"
fi
# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
~~~  
To trigger the bug I ran `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected`.  
To fix the problem I changed this snippet of code:  
~~~
if [[ temp.length == 0 ]]
then 
    echo "Full Score!"
else
    echo $((1-num))"/1"
fi
~~~
to this snippet of code:  
~~~
if [[ -s score.txt ]]
then 
    echo $((1-num))"/1"
else
    echo "Full Score!"
fi
~~~
## Reflection  
During this second half of the quarter, I think the most valuable thing I learned was how to use `vim`. It makes it very easy to remotely edit files, as well as enables you to do everything from the terminal. It is also really interesting to me that they have a built in tutorial on how to use it (`vimtutor`), something that I have not seen for any of the other commands. It is a little weird to get used to at first, but eventually you learn how to use it pretty well and it becomes much easier to use quickly!
