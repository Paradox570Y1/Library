#### **Telephone Input** (`type="tel"`)
The tel input type allows the user to enter a telephone number. It doesn't provide built-in validation but can be customized with a pattern attribute for specific formats.

```html
<label for="tel">Phone Number:</label>
<input type="tel" id="tel" name="tel" placeholder="123-456-7890" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" required>
```