# String 

#### substr:

```C++
string str="We think in generalities, but we live in details.";
                                           // (quoting Alfred N. Whitehead)

string str2 = str.substr (3,5);     // "think"

size_t pos = str.find("live");      // position of "live" in str

string str3 = str.substr (pos);     // get from "live" to the end

cout << str2 << ' ' << str3 << '\n';
// think live in details.
```

## Palindromic String

*  Longest Palindromic Substring [5]

```C++
string longestPalindrome(string s) {
	if (s.length()<2)
		return s;
	int max_length = 0;
	int start_idx = 0;
	int i = 0;
	while (i < s.length()) {
		// Two pointers
		int right = i;
		int left = i;
		// Remove Duplicates!!
		while (right<s.length()-1 && s[right] == s[right+1]) right++;
		i = right + 1;
		// Expanding
		while (right<s.length()-1 && left > 0 && s[right+1] == s[left-1]) {
			right ++; left --;
		}
		int new_length = right - left + 1;
		if (new_length > max_length) {
			max_length = new_length;
			start_idx = left;
		}
	}
	return s.substr(start_idx, max_length);
}
```

## Finding Longest String Without Repeating

* Longest Substring Without Repeating Characters[3]

```C++
int lengthOfLongestSubstring(string s) {
	unordered_map<char, int> char2index;
	int max_length = 0, start = 0, iterator = 0;
	while (iterator< s.length()) {
		auto it = char2index.find(s[iterator]);
		if (it != char2index.end())
			start = max(start, it->second+1);
		char2index[s[iterator]] = iterator;
		max_length = max(max_length, iterator-start+1);
		iterator++;
	}
	return max_length;
}
```

#### isdigit() 

```C++
#include <cctype>
#include <iostream>
#include <cstring>

using namespace std;

int main() {
    char str[] = "hj;pq910js4";

    cout << "The digit in the string are:" << endl;
    for (int i=0; i<strlen(str); i++) {
        if (isdigit(str[i]))
            cout << str[i] << " ";
    }
    return 0;
}
```