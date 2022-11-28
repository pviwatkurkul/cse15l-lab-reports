## Lab Report 5 ##

~~~
{
    CPATH=".;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar"

rm -rf student-submission
git clone $1 student-submission
cp TestListExamples.java student-submission
cp lib/hamcrest-core-1.3.jar student-submission
cp lib/junit-4.13.2.jar student-submission
cd student-submission
points=0
file="ListExamples.java"
if [ -e $file ]
then  
    echo "the file exists"
else 
    echo "the file doesnt exist"
    exit 1
fi
javac -cp $CPATH *.java

if [ $? -ne 0 ]
then
    echo "Compiler Error"
    exit 1
fi
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > output.txt

if [ $(grep -c "testFilter" output.txt) -ne 0 ]
then
    echo "[FAILED 0/1] testFilter Tests"
else
    echo "[PASSED 1/1] testFilter Tests"
    let "points+=1"

fi

if [ $(grep -c "testMerge" output.txt) -ne 0 ]
then
    echo "[FAILED 0/1] testMerge Tests"
else
    echo "[PASSED 1/1] testMerge Tests"
    let "points+=1"

fi
if [ $points -eq 0 ]
then
    echo "Score: 0/2"
    echo "Both methods failed."
    exit 1
fi

if [ $points -eq 1 ]
then
    echo "Score: 0/1"
    echo "One method passed."
    exit 1
fi

if [ $points -eq 2 ]
then  
    echo "Score: 2/2"
    echo "Both methods passed."
    exit 1
fi
}
~~~

![Image]()