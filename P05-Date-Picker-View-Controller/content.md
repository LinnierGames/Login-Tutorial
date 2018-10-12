---
title: "Date Picker Controller"
slug: date-picker-controller
---

After laying out the **Date Picker ViewController**, we can now begin to hook up the controller with its view

In the **DatePickerViewController.swift** file, you should already have the following:

```swift
class DatePickerViewController: UIViewController {
>
    @IBOutlet weak var datePicker: UIDatePicker!
>
    @IBAction func pressDone(_ sender: Any) {
>
    }
>
    @IBAction func pressCancel(_ sender: Any) {
>
    }
}
```

# Hook up the `@IBAction`s and the `@IBOutlet`

Let's connect the `@IBAction`s and the `@IBOutlet` we have in the controller with the storyboard.

> [action]
> Open the **Main.storyboard**, and complete the following:
>
> 1. Connect the **datePicker** `@IBOutlet` to the `UIDatePicker`
> 2. Connect the **pressDone** `@IBAction` to the `UIButton` titled as **Done**
> 3. Connect the **pressCancel** `@IBAction` to the `UIButton` titled as **Cancel**

For testing purposes, add a print statement in both `@IBAction`s to see if it works.
Run it and tap on each button.

# Collecting the date from the DatePicker

Now that our controller is hooked up, we can now read the date when the user taps on **Done**.

> [action]
> In the print statement for the done button, try to print out the selected date from the date picker.

> [solution]
>
```swift
class DatePickerViewController: UIViewController {
>
    ...
>
    @IBAction func pressDone(_ sender: Any) {
        print(datePicker.date)
    }
>
    ...
>
}
```

# Sending the selected date to the Register Screen

Great! So, we've made it this far, we have the screen laid out to allow the user to select a date.
And now, we're going to send the selected date to the Register Screen
How will we achieve this?

We can use an **unwind segue**, but let's try something new.

# Protocols

# Writing a Protocol for the DatePickerViewController

Let's add one method to our protocol, or "contract".

> [action]
> Add the following to **DatePickerViewController.swift** file:
>
```swift
import UIKit
>
protocol DatePickerViewControllerDelegate: class {
    func datePicker(_ datePickerViewController: DatePickerViewController, didFinishWith selectedDate: Date)
}
>
class DatePickerViewController: UIViewController {
>    
    ...
>
}
```

This method has the following:

1. the date picker class itself
1. the date selected

So, whoever conforms the this protocol will have to implement this method.
This is how we'll send the selected date to an object that conforms to this protocol.

# Sending the selected date to the Delegate

Right now we only have a protocol with one method as part of its "contract".
But, the next two steps is what enables the delegate pattern between our **DatePickerViewController** and, in our situation, the **RegisterViewController**.

> [action]
> Add a property to the **DatePickerViewController** class with the following attributes:
>
> 1. name the property `delegate`
> 1. the data type is `DatePickerViewControllerDelegate?`

> [solution]
>
```swift
...
>
class DatePickerViewController: UIViewController {
>
    var delegate: DatePickerViewControllerDelegate?
>
    ...
>
}
```

This property will store who is the delegate of our **DatePickerViewController**.
That way we can now send whoever is our delegate our selected date.

> [action]
> Update `@IBAction func pressDone` to be the following
>
```swift
...
>
class DatePickerViewController: UIViewController {
>
    ...
>
    @IBAction func pressDone(_ sender: Any) {
        delegate?.datePicker(self, didFinishWith: datePicker.date)
    }
>
    ...
>
}
```

What does this do?
So, whatever is the value of our `delegate` property, if not nil, this value will receive our message of `datePicker(datePickerViewController:didFinishWith:)` which is the method we have in our `protocol`.

Right now, if we ran and tested this new code this property will be nil.
So, the last step is to set the `delegate` property to be equal to what?

> [solution]
> The delegate needs to be set to the **RegisterViewController**.

# Updating the delegate to be the **RegisterViewController**

To update the delegate value to be the **RegisterViewController**, we'll have to have both the **RegisterViewController** and the **DatePickerViewController**.
The best place to update this property is in the `prepare(for segue:)` in the **RegisterViewController**.

> [action]
> Open the **Main.storyboard** and select the segue that connects the **RegisterViewController** and the **DatePickerViewController**.
> Update the segue's identifier to **show date picker**.

> [action]
> Add the following to the **RegisterViewController.swift**:
>
```swift
class RegisterViewController: UIViewController {
>
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if let identifier = segue.identifier {
            switch identifier {
            case "show date picker":
                //TODO: update the segue.destination's delegate to be self
            default: break
            }
        }
    }
}
```

Here in the TODO comment we can update the delegate.

> [action]
> Given the segue in this method, update the segue.destination's delegate to be self

> [solution]
>
```swift
class RegisterViewController: UIViewController {
>
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if let identifier = segue.identifier {
            switch identifier {
            case "show date picker":
                guard let datePickerViewController = segue.destination as? DatePickerViewController else {
                    return print("storyboard not set up correctly")
                }

                datePickerViewController.delegate = self
            default: break
            }
        }
    }
}
```

As you can see, Xcode is giving us an error when we try to assign self to `datePickerViewController.delegate`.
Xcode is telling us that the **RegisterViewController** does not conform to the `DatePickerViewControllerDelegate`.
So, let's fix that!

# Conforming to the DatePickerViewControllerDelegate protocol

extension RegisterViewController: DatePickerViewControllerDelegate {
    func datePicker(_ datePickerViewController: DatePickerViewController, didFinishWith selecteDate: Date) {
        selectedBirthday = selecteDate

        let birthdayString = selecteDate.stringValue
        buttonBirthdate.setTitle(birthdayString, for: .normal)

        dismiss(animated: true)
    }
>
}
```

```swift


extension RegisterViewController: DatePickerViewControllerDelegate {
    func datePicker(_ datePickerViewController: DatePickerViewController, didFinishWith selecteDate: Date) {
        selectedBirthday = selecteDate

        let birthdayString = selecteDate.stringValue
        buttonBirthdate.setTitle(birthdayString, for: .normal)

        dismiss(animated: true)
    }
>
}
```
















###END
