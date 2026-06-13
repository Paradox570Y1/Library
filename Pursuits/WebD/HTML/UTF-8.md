### What is UTF-8?

- **UTF-8** stands for **Unicode Transformation Format - 8-bit**.
- It is a variable-width character encoding that can represent every character in the Unicode character set.(like copyright character etc.)
- UTF-8 is backward-compatible with ASCII, which means that any ASCII text is also valid UTF-8.

### Why Use UTF-8 in HTML?

1. **Compatibility**: UTF-8 is compatible with many existing standards and systems.
2. **Internationalization**: It supports a wide range of characters from different languages, making it ideal for international content.
3. **Uniformity**: Ensures consistent text representation across different platforms and browsers.
4. **Default Encoding**: Many modern browsers use UTF-8 as the default character encoding.

### How to Use UTF-8 in the Meta Tag

The meta tag specifying UTF-8 should be placed within the `<head>` section of your HTML document. Here is the syntax:
![[Pasted image 20240625163825.png]]

### Explanation of the Meta Tag

- `<meta charset="UTF-8">`: This meta tag declares the character encoding for the HTML document. The attribute `charset="UTF-8"` tells the browser to use UTF-8 encoding.

### Benefits of Using UTF-8

- **Universal Character Set**: UTF-8 can encode all characters in Unicode, which means you can use any character from any language.
- **Efficiency**: It is a variable-width encoding, so it uses one byte for ASCII characters, making it efficient for texts that are primarily in English.
- **Interoperability**: Ensures that text is displayed correctly on different devices and platforms.
- **Support for Emojis**: With UTF-8, you can include emojis and other special characters in your web pages.

### Example
![[Pasted image 20240625163917.png]]


