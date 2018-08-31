---
title: "Laying out the Register Screen"
slug: register-view-controller
---

So, we have the **Register Screen** all set up in the storyboard including the button the user can tap to enter their birth date.
Now, we got to provide a UI for the user to pick a date.
Luckily for us, `UIKit` includes a class that does just this, the UIDatePicker.

# Use the UIDatePicker class

This class does just that, it allows the user to select a date, or time.
This class has a few useful properties:

- `date: Date` this will give us the selected date
- `maximumDate: Date?` by default this value is nil, but if we set this property to be tomorrow, the user can only select dates from today or in the past
- `minimumDate: Date?` just like maximumDate, this is the inverse
- `datePickerMode: UIDatePickerMode` this is an enum with the following cases:

```swift
enum UIDatePickerMode {
  case UIDatePickerModeTime //picker for the time only
  case UIDatePickerModeDate //picker for the date only
  case UIDatePickerModeDateAndTime //picker for both date and time
  case UIDatePickerModeCountDownTimer //picker for selecting hour and minute
}
```

For the `datePickerMode`, we'll be using `UIDatePickerModeDate` since we only need the year, day, and month.

Now, how will we add the `UIDatePicker`? We could add it to the **Outer StackView** but this date picker takes up a lot of space. Let's create a new view controller primarily responsible of selecting a date.

# DatePickerViewController

In this view controller, we're going to use the `UIDatePicker` to allow the user to select a date and we'll add a **Done** and **Cancel** button as well.

> [action]
> Create a new view controller named `DatePickerViewController` and add the following code inside the class:
>
```swift
class DatePickerViewController: UIViewController {
>
    @IBOutlet weak var datePicker: UIDatePicker!
>
    @IBAction func pressDone(sender: Any) {
>
    }
>
    @IBAction func pressCancel(sender: Any) {
>
    }
}
```

Here we've added two `@IBAction`s for the done and cancel buttons.
Also, we've added an `@IBOutlet` to the date picker so we can retrieve the `date` the user selects.

# Laying out the DatePickerViewController in the Storyboard

Here we got the final result our date picker screen:

![xcode date picker screens](assets/final_date_picker_screen.png "Final Result of Date Picker Screen")

Here is the annotated result of our register screen:

![xcode date picker screens annotated](assets/final_date_picker_screen-annotated.png "Final Result of Date Picker Screen-Annotated")















### ENd
