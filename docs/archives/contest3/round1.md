# Contest 3 Round 3

---

## Problem 1: Secret Base

**Problem Statement**

You are given a secret message that you must decode to enter a secret base. The message contains only letters. Each letter has been cyclically shifted 5 characters to the right and is replaced by the letter that is 4 places after it on the alphabet (looping back to the beginning if necessary). I.e. ‘A’ would be replaced by ‘E’, ‘X’ would be replaced by ‘B’, etc. Given the message, what was the original secret message?


**Input Specifications**

You are given a single string, the message to be decoded.


**Output Specifications**

Output a single string, the decoded message.


**Sample Input**

AsvphLipps


**Sample Output**

HelloWorld


**Explanation**

Reversing the encoding operation, we cyclically shift each character 5 to the left and replace it with the letter 4 places before it in the alphabet, giving us ‘HelloWorld’.
