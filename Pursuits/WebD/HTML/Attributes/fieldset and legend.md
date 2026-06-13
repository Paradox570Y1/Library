##### 1. `<fieldset>`
- **Role**: The `<fieldset>` tag is used to group related elements within a form, typically to visually group and organize form controls. It provides a box around the grouped elements to indicate that they belong together. This helps improve the accessibility and structure of the form, especially when dealing with complex forms.
##### 2. `<legend>
**Role**: The `<legend>` tag is used to define a caption or title for the content inside a `<fieldset>`. It helps users understand the context or category of the grouped form controls. It is typically placed as the first child element inside a `<fieldset>`.
    
- **Attributes**:
    
    - `disabled`: If applied, it disables all form controls within the `<fieldset>`.
    - `form`: Specifies which form the `<fieldset>` is related to if it's outside of a `<form>` element.

---


```html
<form>
        <fieldset>
            <legend>Java Project</legend>
            Title:<input type="text"><br><br>
            Link:<input type="text"><br><br>
            Student ID:<input type="text">
        </fieldset>
        <br>
        <fieldset>
            <legend>PHP Project</legend>
            Title:<input type="text"><br><br>
            Link:<input type="text"><br><br>
            Student ID:<input type="text">
        </fieldset>
    </form>
```
![[Pasted image 20240709170901.png]]

```html
<form>
        <fieldset>
            <legend>User Login</legend>
            <table border>
                <tr>
                    <th>Username</th>
                    <th><input type="text" placeholder="Enter username"></th>
                </tr>
                <tr>
                    <th>Password</th>
                    <th><input type="text" placeholder="Enter password"></th>
                </tr>
                <tr>
                    <td colspan="2" align="center">
                        <input type="submit">
                        <input type="reset">
                    </td>
                </tr>
            </table>
        </fieldset>
    </form>
```
![[Pasted image 20240709171822.png|400]]
