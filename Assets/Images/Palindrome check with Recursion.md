```java
class Solution {
    // Recursive function to check if the string is a palindrome
    static boolean isPalindrome(String str, int i) {
        // Base case: if the index crosses the middle of the string
        if (i >= str.length() / 2) {
            return true;
        }
        // Check if characters at the current index and its mirror index are not equal
        if (str.charAt(i) != str.charAt(str.length() - 1 - i)) {
            return false;
        }
        // Recursive call for the next index
        return isPalindrome(str, i + 1);
    }

    public static void main(String[] args) {
        String testString = "madam";
        boolean result = isPalindrome(testString, 0);
        System.out.println("Is the string \"" + testString + "\" a palindrome? " + result);
    }
}

```