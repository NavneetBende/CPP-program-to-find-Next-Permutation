Next Permutation in C++
 

Here, in this page we will discuss the program to find next permutation in C++ . We are Given with a word, and need to find the lexicographically greater permutation of it. For example, lexicographically next permutation of “acb” is “bac”.

Here, we will do this program by using the inbuilt next_permutaion() function present in STL library and also discuss program without using that inbuilt function.

Next Permutation in C++
Method Discussed :
Method 1 : Using Inbuilt function
Method 2 : without using inbuilt function
Method 1:
Take the input string from the user and store it in variable say s.
Now, call next_permutation(s.begin(), s.end()). It returns ‘true’ if the function could rearrange the object as a lexicographically greater permutation. Otherwise, the function returns ‘false’.
Run
#include <bits/stdc++.h>
using namespace std;
int main()
{
  string s = "abc" ;

  bool val= next_permutation(s.begin(), s.end());

  if (val == false)
   cout << "No Word Possible" << endl;
  else
   cout << s << endl;

  return 0;
}
Output :
bac
Method 2 :
Take the input string from the user and store it in variable say s.
For a sequence which is not sorted in descending order for example “abedc”, we can follow below steps
a) Traverse from right and find the first item that is not following the descending order. For example in “abedc”, the character ‘b’ does not follow the descending order.
b) Swap the found character with closest greater (or smallest greater) element on right side of it. In case of “abedc”, we have ‘c’ as the closest greater element. After swapping ‘b’ and ‘c’, string becomes “acedb”.
c) After swapping, sort the string after the position of character found in step a. After sorting the substring “edb” of “acedb”, we get “acbde” which is the required next permutation.

Optimizations in step b) and c)
a) Since the sequence is sorted in decreasing order, we can use binary search to find the closest greater element.
c) Since the sequence is already sorted in decreasing order (even after swapping as we swapped with the closest greater), we can get the sequence sorted (in increasing order) after reversing it.

Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Minimum no. of Jumps to reach the end of an array 

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Run

#include <bits/stdc++.h>
using namespace std;
void rev(string& s, int l, int r)
{
  while (l < r)
    swap(s[l++], s[r--]);
}

int bsearch(string& s, int l, int r, int key)
{
    int index = -1;
    while (l <= r) {
       int mid = l + (r - l) / 2;
         if (s[mid] <= key) 
             r = mid - 1;
         else {
             l = mid + 1;
             if (index == -1 || s[index] >= s[mid])
                index = mid;
         }
    }
    return index;
}

bool nextpermutation(string& s)
{
    int len = s.length(), i = len - 2;
    while (i >= 0 && s[i] >= s[i + 1])
      --i;
      if (i < 0)
         return false;
      else {
         int index = bsearch(s, i + 1, len - 1, s[i]);
         swap(s[i], s[index]);
         rev(s, i + 1, len - 1);
         return true;
       }
}

// Driver code
int main()
{
   string s ="abc";
 
    bool val = nextpermutation(s);
    if (val == false)
        cout << "No Word Possible" << endl;
    else
        cout << s << endl;
    return 0;
}
Output :
bac
