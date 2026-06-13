# Basic

- [[Stack & Queue Theory]]
- [[Implement Stack using Arrays]]
- [[Queue using Array]]
- [[Implement Stack using Queue]]
- [[Implement Queue using Stack]]
- [[Implement Stack using Node]]
- [[Implement Queue using LL]]
- [[Check for balanced Parenthesis]]
- [[Implement Min Stack]]

# Prefix, Infix & Postfix Conversion

- [[Conversion Theory]]
- [[Infix to Postfix]]
- [[Infix to Prefix]]
- [[Prefix to Infix]]
- [[Postfix to Infix]]
- [[Postfix to Prefix]]
- [[Prefix to Postfix]]


# Monotonic Stack

- [[Monotonic Stack Theory]]
- [[Next Greater Element (Modified NGE)]]
- [[NGE 2]]
- [[Nearest Smallest Element]]
- [[No. of NGE's to the right]]
- [[Trapping Rain Water]]
- [[Sum of Subarray Minimums]]
- [[Asteroid Collisions]]
- [[Sum of subarray ranges]]
- [[Remove k digits]]
- [[Largest Rectangle in Histogram]]
- [[85. Maximal Rectangle]]

# Implementation problems

- [[Sliding Window Problem]]
// Brute force gives TC -> O (N\*k)
// Priority Queue can be used to retrieve the max element while polling the biggest elements if the index of that element is out of window. 
// Similarly is the case with using tree set but with tree set you remove any index in between therefore you can always add upcoming element and remove the element which is k-1 distance before that.
//Optimal approach is similar to monotonic stack , here you always try to maintain biggest element within the current window in the head of the dequeue, by removing all elements from tail which seems to be smaller then the current element, this ensures next bigger element is right next to the cur windows biggest element by removing all small elements in between and remove the biggest element if it's out of range.
- [[Online Stock Span]]
- [[The Celebrity Problem]]
- [[LRU Cache]]
- [[Maximum Frequency Stack]]
- [[LFU Cache]]

# Other problems

- [[Basic Calculator]]
- [[2197. Replace Non-Coprime Numbers in Array]]
- [[3542. Minimum Operations to Convert All Elements to Zero]]
- [[2211. Count Collisions on a Road]]