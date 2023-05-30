---
layout: post
title: Coding Questions
date: 2023-04-30 
description: This blog is a part of interview prepration this contain explanation of coding question and concepts related to it.
tags: Interview_prep
categories: Coding
related_posts: false
published: false
---

# 1.Backtracking
To basice idea of backtracking problem is to try all the possible solution and then choose the best one. But this choices can be tricky some times hence when solving a backtracking problem we need to keep in mind the following points:
1. Visualize the state space tree (What are the choice you have at each step)
2. Identify the base case (When to stop)
3. branch pruning (When to stop exploring a branch)

Points specific to python implementation:
1. Python passes list/mutable object by reference hence we need to make a copy of the list before passing it to the recursive function this can be done by simply doing array[:] this creates a new copy of the list.
2. If we wish to use list as it is then we have to pop the element which we have added after the recursive call to the function.

## Problems

### 1.[Word Search](https://leetcode.com/problems/word-search/)
Given an m x n grid of characters board and a string word, return true if word exists in the grid.
<br><br>**Learning**: 
The idea is to use backtracking which we will start from each cell and when we visit a cell we mark with '.' and pass the new board to the recursive function. When we get back from the recursive call we unmark the cell and move to the next cell. We can prune(return) the branch if the cell we are visiting is not equal to the character we are looking for.

### 2.[Letter Case Permutation](https://leetcode.com/problems/letter-case-permutation/)

Given a string s, we can transform every letter individually to be lowercase or uppercase to create all possible strings.
Return a list of all possible strings we could create.
<br><br>**Learning**:
We will use backtracking as the string is alpha numerice when the string is a letter we have 2 choice either to keep it as a lower case or to upper case but if it is a number we can just keep it as it is(No branching). Basically it is conditional branching. Also we have a function swapcase() which can be used to swap the case of the letter.[solution](https://leetcode.com/problems/letter-case-permutation/solutions/379928/python-clear-solution/?orderBy=most_votes&languageTags=python)

### 3.[Subsets](https://leetcode.com/problems/subsets/)

Given an integer array nums of unique elements, return all possible subsets (the power set).
The solution set must not contain duplicate subsets. Return the solution in any order.
<br><br>**Learning**:
The idea is to use backtracking and at each step we have 2 choice either to include the element or not. In both the cases we will remove the number for the list and pass the new list to the recursive function.

### 4.[Subsets II](https://leetcode.com/problems/subsets-ii/)

Given an integer array nums that may contain duplicates, return all possible subsets (the power set).
The solution set must not contain duplicate subsets. Return the solution in any order.
<br><br>**Learning**:
The idea is to use backtracking and at each step we have 2 choice either to include the element or not. But the difference here is that we also have to decide on number of times we want to include the element. So effectully we have k choice which is the number of times we want to include the element this will also include zero time or not to keep the element and we write such recurssion in loop. [solution](https://leetcode.com/problems/subsets-ii/solutions/3464268/backtracking-in-loop/?orderBy=most_votes) This solution prevents us from duplicates because for each element we are only branching ones with a branching factor of k. If we use the stratergy of Subsets I then we will have duplicates because we will be branching for single element multiple times.

### 5.[Permutations](https://leetcode.com/problems/permutations/)

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.
<br><br>**Learning**:
The idea is to use backtracking and at each first step we have n choice which is the number of elements in the list. We will remove the element from the list and pass the new list to the recursive function. We will also add the element back to the list after the recursive call.

### 6.[Permutations II](https://leetcode.com/problems/permutations-ii/)

Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.
<br><br>**Learning**:
The idea is to use backtracking and at each step we have m choice which is no. of unique numbers avaiable in that recursive step. we have to maintain a dictionary to keep track of the number of times we have used a number as it should not exess its count in the input array. [solution](https://leetcode.com/problems/permutations-ii/submissions/941544514/)

### 7.[Combinations](https://leetcode.com/problems/combinations/)

Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].
You may return the answer in any order.
<br><br>**Learning**:
At each step we have n choice which is the number of elements no used till now. We will remove the element from the list and pass the new list to the recursive function. The point to remender is that the list will get smaller and smaller every time we call the recursive function. In my solution i have not used a list but the range function so i have to pass st ever time. [solution](https://leetcode.com/problems/combinations/submissions/941550426/)

### 8.[Combination Sum](https://leetcode.com/problems/combination-sum/)

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.
The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.
<br><br>**Learning**::
At each step we have the choice to use a number from 0 to infinity times but at max we will only use it still its sum is equal to target or less than target. So let say we have array [2,4,5,9] and the target is 18 so we have choices for 2 as [[2] ,[2,2],[2,2,2],...] this is what we will brach for each element and remove that elemnt from the array and pass a temp array with each case and this will be done recursively till the sum is target or greater than targert. If it is equal to target we will add the temp array to the result. [solution](https://leetcode.com/problems/combination-sum/submissions/941567764/)

### 9.[Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target. Each number in candidates may only be used once in the combination.
Note: The solution set must not contain duplicate combinations.
<br><br>**Learning**:
Here we do not have infinite choice for each element we only have choice equal to the number of times the element is present in the array. So we will have to maintain a dictionary to keep track of the number of times we have used a number as it should not exess its count in the input array. [solution](https://leetcode.com/problems/combination-sum-ii/submissions/941727613/)

### 10.[Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.
<br><br>**Learning**:
Partition means division of a string into substrings such that combining all the substring will give the original string. Out of those we have to give the partition in which all the substring are palindroms. So at each step we have the choise to use first i element of the string if it form a palindrom then we keep it in the temp array and pass the remaning string to the recursive function. If not then we continue till we find a palindrom. [solution](https://leetcode.com/problems/palindrome-partitioning/submissions/941994464/)

### 11.[Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)
### 12.[Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
### 13.[Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

