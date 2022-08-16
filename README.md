# Playing-With-Stacks-and-Queue
<h3>Few C++ functions that make use of the concept of stacks and queue</h3>

Program that uses a stack to check for balancing symbols in the C++ language, where symbols are parentheses ( ), square brackets [ ], and curly brackets { }. The line that included an error, in case an error is detrected, is also mentioned.
```
#include <iostream>
#include <stack>
#include <vector>
#include <fstream>

using namespace std;

int main() {
    stack<char, vector<char>> parser;
    ifstream myfile;
    string filename;
    int lineN = 0;
    cout << "Which file to check: ";
    cin >> filename;
    myfile.open(filename);
    if(!myfile) exit(1);
    char buffer;
    while((buffer=myfile.get())!=-1) {
        if(buffer == '\n') lineN++;
        if(buffer == '(' or buffer == '[' or buffer == '{') parser.push(buffer);
        else if(buffer == ')') {
            if(parser.empty()) { cout << "Error at line " << lineN << " expected " << (char)(buffer - 1); exit(1); }
            else if(parser.top() == (int)buffer - 1 ) parser.pop();
            else { cout << "Error at line " << lineN << ": " << parser.top() << " not closed"; exit(1); }
        }
        else if(buffer == ']' or buffer == '}') {
            if(parser.empty()) { cout << "Error at line " << lineN << " expected " << (char)(buffer - 2); exit(1); }
            else if(parser.top() == (int)buffer - 2) parser.pop();
            else { cout << "Error at line " << lineN << ": " << parser.top() << " not closed"; exit(1); }
        }
    }
    if(!parser.empty()) { cout << "Error " << parser.top() << " not closed"; }
 
    return 0;
}
```

Program that reads a postfix mathmatical expression from the user, stores all terms into a stack, computes its value, and returns it to the user. Assume the expression will contain only integers and the following binary arithmetic operators: + (addition), - (subtraction), * (multiplication) and / (division).
```
#include <iostream>
#include <stack>
#include <string>
#include <string.h>
#define _CRT_SECURE_NO_WARNINGS

using namespace std;

int main() {
    stack<int> operation;
    int str_size = 100;
    //char str[100] = {"3 2 + 4 * 5 1 - /"};
    char str[100];
    char* p;
    cout << "Enter the statement to undergo the postfix mathematical expressions, separeted by spaces: ";
    cin.getline(str, 100);
    p = strtok(str, " ");
    while (p != NULL) {
        //cout<<p<<endl;
        if (isdigit(p[0])) {
            int x = atoi(p);
            operation.push(x);
        }
        else if (p[0] == '+') {
            int z = operation.top();
            operation.pop();
            int y = operation.top();
            operation.pop();
            operation.push(z + y);
        }
        else if (p[0] == '*') {
            int z = operation.top();
            operation.pop();
            int y = operation.top();
            operation.pop();
            operation.push(z * y);
        }
        else if (p[0] == '-') {
            int z = operation.top();
            operation.pop();
            int y = operation.top();
            operation.pop();
            operation.push(y - z);
        }
        else if (p[0] == '/') {
            int z = operation.top();
            operation.pop();
            int y = operation.top();
            operation.pop();
            operation.push(y / z);
        }
        else {
            cout << "Error: character undetectable";
        }
        //cout << "tops is "<<operation.top()<<endl;
        p = strtok(NULL, " ");
    }
    cout << operation.top();
 
    return 0;
}
```
