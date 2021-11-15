---
layout: post
title: Challenges
---
## Table of Contents
- [Reverse A String](#reverse-a-string)
- [Factorialize A Number](#factorialize-a-number)
- [Check for Palindrome](#check-for-palindrome)
- [Find the Longest word in a string](#find-the-longest-word-in-a-string)
- [Title Case a Sentence](#title-case-a-sentence)
- [Return Largest Numbers in Arrays](#return-largest-numbers-in-arrays)
- [Confirm the Ending](#confirm-the-ending)
- [Repeat a String Repeat a String](#repeat-a-string-repeat-a-string)
- [Truncate a String](#truncate-a-string)
- [Chunky Monkey](#chunky-monkey)
- [Slasher Flick](#slasher-flick)
- [Mutations](#mutations)
- [Falsy Bouncer](#falsy-bouncer)
- [Seek and Destroy](#seek-and-destroy)
- [Where do I Belong](#where-do-i-belong)
- [Caesars Chiper](#caesars-chiper)
- [Sum All The Numbers In Range](#sum-all-the-numbers-in-range)
- [Diff Two Arrays](#diff-two-arrays)
- [Roman Numeral Converter](#roman-numeral-converter)

## Reverse A String <a name="reverse-a-string"></a>

```
function reverseString(str) {
  const strArr = str.split('');
  const reverseStrArr = strArr.reverse();
  const reversedString = reverseStrArr.join('');
  return reversedString;
}

const result = reverseString('hello');
console.log(result);
// olleh


function reverseString(str) {
  let final = '';
  for (let i = str.length - 1; i >= 0; i--) {
    final += str[i];
  }
  return final;
}

const result = reverseString('hello');
console.log(result);
// olleh
```

## Factorialize A Number <a name="factorialize-a-number"></a>

```
function factorialize(num) {
  let result = 1;
  for (let i = 1; i <= num; i++) {
    result *= i;
  }
  return result;
}

const result = factorialize(5);
console.log(result);
// 120

function factorialize(num) {
  if (num === 1) return 1;
  return num * factorialize(num - 1);
}

const result = factorialize(2);
console.log(result);
// 2
```

## Check for Palindrome <a name="check-for-palindrome"></a>

```
function palindrome(str) {
  const reg = /[\W_]/g;
  const smallStr = str.toLowerCase().replace(reg, '');
  const reversed = smallStr.split('').reverse().join('');
  if (reversed === smallStr) return true;

  return false;
}

const result = palindrome('eye');
console.log(result);
// true
```

## Find the Longest word in a string <a name="find-the-longest-word-in-a-string"></a>

```
function findLongestWord(str) {
  const words = str.split(' ');
  let longest = '';
  for (const word of words) {
    if (word.length > longest.length) longest = word;
  }
  return longest.length;
}

const result = findLongestWord('The quick brown fox jumped over the lazy dog');
console.log(result);
// 6

function findLongestWord(str) {
  return str.split(' ').sort((a, b) => b.length - a.length)[0].length;
}

const result = findLongestWord('The quick brown fox jumped over the lazy dog');
console.log(result);
// 6
```

## Title Case a Sentence <a name="title-case-a-sentence"></a>

```
function titleCase(str) {
  const words = str.toLowerCase().split(' ');
  for (let i = 0; i < words.length; i++) {
    words[i] = words[i][0].toUpperCase() + words[i].slice(1);
  }
  return words.join(' ');
}

const result = titleCase("I'm a litte tea pot");
console.log(result);
// I'm A Litte Tea Pot

function titleCase(str) {
  const titled = str
    .toLowerCase()
    .split(' ')
    .map((elem) => elem[0].toUpperCase() + elem.slice(1));
  return titled.join(' ');
}

const result = titleCase("I'm a litte tea pot");
console.log(result);
// I'm A Litte Tea Pot

```

## Return Largest Numbers in Arrays <a name="return-largest-numbers-in-arrays"></a>

```
function largestOfFour(arr) {
  let maxes = [];
  for (let i = 0; i < arr.length; i++) {
    let tempMax = arr[i][0];
    for (let j = 0; j < arr[i].length; j++) {
      if (tempMax < arr[i][j]) tempMax = arr[i][j];
    }
    maxes.push(tempMax);
  }
  return maxes;
}

const result = largestOfFour([
  [4, 5, 1, 3],
  [13, 27, 18, 26],
  [32, 35, 37, 39],
  [1000, 1001, 857, 1],
]);
console.log(result);
// [ 5, 27, 39, 1001 ]


function largestOfFour(arr) {
  let maxes = [0, 0, 0, 0];
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr[i].length; j++) {
      if (maxes[i] < arr[i][j]) maxes[i] = arr[i][j];
    }
  }
  return maxes;
}

const result = largestOfFour([
  [4, 5, 1, 3],
  [13, 27, 18, 26],
  [32, 35, 37, 39],
  [1000, 1001, 857, 1],
]);
console.log(result);
// [ 5, 27, 39, 1001 ]


```

## Confirm the Ending <a name="confirm-the-ending"></a>

```
function confirmEnding(str, target) {
  return str.endsWith(target);
}

const result = confirmEnding('Bastian', 'n');
console.log(result);
// true

function confirmEnding(str, target) {
  return str.substr(-target.length) === target;
}

const result = confirmEnding('Bastian', 'n');
console.log(result);
// true
```

## Repeat a String Repeat a String <a name="repeat-a-string-repeat-a-string"></a>

```
function repeatStringNumTimes(str, num) {
  if (num < 0) return '';

  return str.repeat(num);
}

const result = repeatStringNumTimes('abc', 3);
console.log(result);
// abcabcabc

function repeatStringNumTimes(str, num) {
  if (num < 0) return '';
  let final = '';
  for (let i = 0; i < num; i++) {
    final += str;
  }
  return final;
}

const result = repeatStringNumTimes('abc', 3);
console.log(result);
// abcabcabc

function repeatStringNumTimes(str, num) {
  if (num < 1) return '';
  return str + repeatStringNumTimes(str, num - 1);
}

const result = repeatStringNumTimes('abc', 3);
console.log(result);
// abcabcabc
```

## Truncate a String <a name="truncate-a-string"></a>

```
function truncateString(str, num) {
  if (num >= str.length) return str;
  if (num <= 3) return str.slice(0, num) + '...';
  return str.slice(0, num - 3) + '...';
}

const result = truncateString(
  'A-tisket a-tasket A green and yellow basket',
  11
);
console.log(result);
// A-tisket...
```

## Chunky Monkey <a name="chunky-monkey"></a>

```
function chunkArrayInGroups(arr, size) {
  let groups = [];

  while (arr.length > 0) {
    groups.push(arr.slice(0, size));
    arr = arr.slice(size);
  }

  return groups;
}

const result = chunkArrayInGroups(['a', 'b', 'c', 'd', 'e', 'f'], 2);
console.log(result);
// [ [ 'a', 'b' ], [ 'c', 'd' ], [ 'e', 'f' ] ]


function chunkArrayInGroups(arr, size) {
  let groups = [];

  while (arr.length > 0) {
    groups.push(arr.splice(0, size));
  }

  return groups;
}

const result = chunkArrayInGroups(['a', 'b', 'c', 'd', 'e', 'f'], 2);
console.log(result);
// [ [ 'a', 'b' ], [ 'c', 'd' ], [ 'e', 'f' ] ]

```

## Slasher Flick <a name="slasher-flick"></a>

```
function slasher(arr, howMany) {
  arr.splice(0, howMany);
  return arr;
}

const result = slasher([1, 2, 3], 2);
console.log(result);
// [ 3 ]

```

## Mutations <a name="mutations"></a>

```
function mutation(arr) {
  const firstWord = arr[0].toLowerCase();
  const secondWord = arr[1].toLowerCase();

  for (let i = 0; i < secondWord.length; i++) {
    if (firstWord.indexOf(secondWord[i]) === -1) return false;
  }

  return true;
}

const result = mutation(['hello', 'hey']);
console.log(result);
// false

function mutation(arr) {
  const firstWord = arr[0].toLowerCase();
  const secondWord = arr[1].toLowerCase();

  for (let i = 0; i < secondWord.length; i++) {
    if (!firstWord.includes(secondWord[i])) return false;
  }

  return true;
}

const result = mutation(['hello', 'hey']);
console.log(result);
// false

```

## Falsy Bouncer <a name="falsy-bouncer"></a>

```
function bouncer(arr) {
  let truthies = [];
  for (let elem of arr) {
    if (elem) truthies.push(elem);
  }
  return truthies;
}

const result = bouncer([7, 'ate', '', false, 9]);
console.log(result);
// [ 7, 'ate', 9 ]


function bouncer(arr) {
  return arr.filter((elem) => elem);
}

const result = bouncer([7, 'ate', '', false, 9]);
console.log(result);
// [ 7, 'ate', 9 ]

```

## Seek and Destroy <a name="seek-and-destroy"></a>

```
function destroyer(arr) {
  let args = Array.from(arguments);
  args.splice(0, 1);
  const targets = args;
  let result = [];
  for (let num of arr) {
    if (targets.indexOf(num) === -1) result.push(num);
  }

  return result;
}

const result = destroyer([1, 2, 3, 1, 2, 3], 2, 3);
console.log(result);
// [ 1, 1 ]


function destroyer(arr) {
  let args = Array.from(arguments);
  args.splice(0, 1);
  const targets = args;

  return arr.filter((num) => args.indexOf(num) === -1);
}

const result = destroyer([1, 2, 3, 1, 2, 3], 2, 3);
console.log(result);
// [ 1, 1 ]

```

## Where do I Belong <a name="where-do-i-belong"></a>

```
function getIndexToIns(arr, num) {
  arr.sort((a, b) => a - b);
  for (let i = 0; i < arr.length; i++) {
    if (num <= arr[i]) {
      return i;
    }
  }
  return arr.length;
}

const result = getIndexToIns([40, 60], 50);
console.log(result);
// 1
```

## Caesars Chiper <a name="caesars-chiper"></a>

```
function rot13(str) {
  let solved = '';
  for (let i = 0; i < str.length; i++) {
    let asciiNum = str[i].charCodeAt();
    if (asciiNum >= 65 && asciiNum <= 77) {
      solved += String.fromCharCode(asciiNum + 13);
    } else if (asciiNum >= 78 && asciiNum <= 90) {
      solved += String.fromCharCode(asciiNum - 13);
    } else {
      solved += str[i];
    }
  }
  return solved;
}

const result = rot13('AB YZ');
console.log(result);
// NO LM

```

## Sum All The Numbers In Range <a name="sum-all-the-numbers-in-range"></a>

```
function sumAll(arr) {
  const start = Math.min(arr[0], arr[1]);
  const end = Math.max(arr[0], arr[1]);
  let total = 0;

  for (let i = start; i <= end; i++) {
    total += i;
  }
  return total;
}

const result = sumAll([1, 4]);
console.log(result);
// 10

```

## Diff Two Arrays <a name="diff-two-arrays"></a>

```
function diffArray(arr1, arr2) {
  let result = [];
  for (let i = 0; i < arr1.length; i++) {
    if (arr2.indexOf(arr1[i]) === -1) result.push(arr1[1]);
  }

  for (let j = 0; j < arr2.length; j++) {
    if (arr1.indexOf(arr2[j]) === -1) result.push(arr2[j]);
  }

  return result;
}

const result = diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]);
console.log(result);
// [ 4 ]

function diffArray(arr1, arr2) {
  let combo = arr1.concat(arr2);
  return combo.filter((num) => {
    if (arr1.indexOf(num) === -1 || arr2.indexOf(num) === -1) {
      return num;
    }
  });
}

const result = diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]);
console.log(result);
// [ 4 ]

```

## Roman Numeral Converter <a name="roman-numeral-converter"></a>

```
function convertToRoman(num) {
  const romanToNum = {
    M: 1000,
    CM: 900,
    D: 500,
    CD: 400,
    C: 100,
    XC: 90,
    L: 50,
    XL: 40,
    X: 10,
    IX: 9,
    V: 5,
    IV: 4,
    I: 1,
  };

  let roman = '';

  for (let key in romanToNum) {
    while (num >= romanToNum[key]) {
      roman += key;
      num -= romanToNum[key];
    }
  }
  return roman;
}

const result = convertToRoman(8);
console.log(result);
// VIII

```
