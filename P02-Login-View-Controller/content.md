---
title: "Connecting the Storyboard with the ViewController"
slug: login-view-controller
---

Now that we have the Login Screen all laid out, our next move is to add actions to the buttons and collect the input the user entered.

# Connecting the Storyboard with the ViewController

Go ahead and adjust your Xcode layout to have both the _Main.storyboard_ and the _ViewController.swift_ files open side by side.

> [action]
> 1. Add `@IBOutet`s to the **Username TextField** and the **Password **TextField**. Then,
> 1. Add `@IBAction`s to the **Login Button** and the **SignUp Button**.

> [solution]
>
```swift
class ViewController: UIViewController {
>
    @IBOutlet weak var textFieldUsername: UITextField!
    @IBOutlet weak var textFieldPassword: UITextField!
>    
    @IBAction func pressLogin(_ sender: Any) {
>        
    }
>    
    @IBAction func pressSignUp(_ sender: Any) {
>        
    }
}
```
>
> Your naming may be different from what you see here

Cool! Now that we have outlets to our textfields and an action for our login button, let's write a method that does our logging in:

# Write a Placeholder Method for Logging in

In this function, there should be two parameters, or arguments. One for the username, and the second for the password.
Don't worry, the body of this method will only have a comment.

> [action]
> Write a method in the ViewController class with the following signature:
> 1. Give it an appropriate method name for logging in a user. This method does not return a value
> 1. Two parameters: one for the username which is a `String`, and the second for the password which is also a `String`
> 1. Add the following comment inside the body of this method: `//TODO: login user`

> [solution]
>
```swift
class LoginViewController: UIViewController {
>
    func loginUser(username: String, password: String) {
>
        //TODO: login user
>
        print("Welcome, \(username)!")
    }
    ...
}
```
>
> Since we used a `TODO` comment, we can revisit this in the future when we want to implement the user login logic

# Validating the User's Input

Now that we have a method in our `ViewController`, let's use it in our **Login Button Action**.

> [action]
> Use the `loginUser(username:password:)` method we just added in the `pressLogin(sender:)` method.
> Note: you'll need to use the `IBOutlet`s that connect to the `UITextField`s to retrieve the text the user input in each text field.

> [solution]
>
```swift
class ViewController: UIViewController {
    ...
    @IBAction func pressLogin(_ sender: Any) {
>
        guard
            textFieldUsername.text?.isEmpty == false,
            let username = textFieldUsername.text,
            textFieldPassword.text?.isEmpty == false,
            let password = textFieldPassword.text else {
                return print("text fields must not be empty!")
        }
>
        //dismiss keyboard
        view.endEditing(false)
>
        loginUser(username: username, password: password)
    }
    ...
}
```
>
> Here, we guard that both text fields are not empty.
> Since each `textfield.text` property is an _Optional String_, we `guard let` each text field's text into a new variable.
> Then, with each variable, we use, or invoke, the `loginUser(username:password:)` method.
> As for the `view.endEditing(false)`, this allows us to dismiss the keyboard if it's present.
> Check out more [here](https://developer.apple.com/documentation/uikit/uiview/1619630-endediting) in the docs.

# Present the RegisterViewController















#$$$$$$$ End
