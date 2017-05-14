+++
date = "2017-05-14T14:46:40+06:00"
tags = ["ios", "programming"]
categories = ["ios"]
title = "Automatic view push for UITextField in iOS"
banner = "img/blog/ios-uitextfield-keyboard-push.jpg"

+++

**Client**: *I can enter my first name, middle name and last name fine in iPhone 7, but in iPhone 5S the last name text field is covered by keyboad, why this is happening?* <br><br>

One of the oldest and basic problem of using [UITextField][uiTextFieldAppleReference] in iOS. If you are making a form or adding multiple UI components in one page for your iOS application, its pretty much normal that the bottom [UITextFields][uiTextFieldAppleReference] could be covered by your keyboard. So we do a lot of tricks, if-else, switch-case to determine how much I need the view to push up, or we design the entire form/input fields in a UIScrollView. Well, what if we could implement a mechanism where the view will be pushed automatically by calculating the position of the textfield? Lets find out!
<br><br>(Jump: Browse to the [sample code][githubref] on Github Gists)

![Keyboard move up needed](http://redgreen.studio/img/blog/ios-uitextfield-keyboard-push.jpg  "Keyboard need to move up")

### The Basics
When the text field become active for writing(AKA becomes firstResponder), we will get delegate calls via [UITextFieldDelegate][uiTextFieldDelegateAppleReference], by which we can determine that which textfield is going active and keyboard is about to show.
```
-(void)textFieldDidBeginEditing:(UITextField *)textField
{
	//do something here with the reference "textfield"
}
```
As we get the reference of the textfield, we can determine what is its position in the window. Is it going to be covered with Keyboard? If so, we can just push the view much enough so that the textField stays just little over the keyboard. If it's not going to covered up by the keyboard, then just leave the view as it is. Also, in the ```-(void)textFieldDidEndEditing:(UITextField *)textField``` delegate call, we can determine if the view is pushed up or not, if pushed up we can bring it down. Thats the basic and overall idea!

### OK, show me the code already!

Its surprisingly very simple to implement the mechanism, all we need the height of the device screen, lets say *screenHeight*, the textfields lowest y value, lets say *textFieldBottomPoint* and the height of the keyboard, say *AVERAGE_KEYBOARD_HEIGHT* , so if 
```
(screenHeight - textFieldBottomPoint) < AVERAGE_KEYBOARD_HEIGHT
```
that means this textField going to cover by keyboard, so we need to push the view up for *viewMoveUpOffsetForKeyboard* amount...
```
viewMoveUpOffsetForKeyboard = AVERAGE_KEYBOARD_HEIGHT - (screenHeight - textFiledBottomPoint) + 30 ;
```
where 30 is vertical space between keyboard and the textfield. If we check this before every textfield becomes firstResponder, we can easily determine wheather or not we need to move the view up for making the textfield visible, and also we can determine how much we need to move the view up for that particular keyboard.

### Github Gist 
Here is the total gist of the sample code hosted in github.


<script src="https://gist.github.com/benzamin/fc96755dd0f985f99ab80850993686d8.js"></script>

Hope you like the way it determines the view pushing  is necessary or not.

**Dont forget to explore and star my [github][account] repos, comment if you have something in your mind 😊** 

[githubref]: https://gist.github.com/benzamin/fc96755dd0f985f99ab80850993686d8
[account]: https://github.com/benzamin/
[uiTextFieldAppleReference]: https://developer.apple.com/reference/uikit/uitextfield
[uiTextFieldDelegateAppleReference]: https://developer.apple.com/reference/uikit/uitextfielddelegate



