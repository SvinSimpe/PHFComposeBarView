# PHFComposeBarView

![demo](demo.gif)

This is a precise reconstruction of the compose bar from the iOS Messages.app,
mimicking the behaviors and graphics while also allowing you to customize many
aspects of it.

It basically consists of a text view, a placeholder label, a utility
button located to the left of the text view, and a main button located to the
right of the text view.

## Features

- title of main button (the one on the right) can be changed
- tint color of main button can be changed
- title of the placeholder can be changed
- placeholder is exposed as a property for further customization
- text view is exposed as a property for further customization
- utility button (the one on the left) can be shown by setting the utility
  button image (best results for white images on transparent background with up
  to 32pt side length)
- optional character counter when specifying a max character count (similar to
  typing an SMS in Messages.app; the max char count limit is not imposed)
- uses delegation to notify of button presses
- forwards delegation methods from the text view
- automatically grows when text wraps and posts "will" and "did" notifications
  for frame changes so you can adjust your views
- by default grows upwards, alternatively downwards
- max height for growth can be specified in terms of points or line numbers

## Installation

The prefered way is to use [CococaPods](http://cocoapods.org).

```ruby
pod 'PHFComposeBarView', '~> 1.0'
```

If you can't use CocoaPods for some reason (you really should though, it's the
cool kid on the block), then grab the files in `Classes/` and `Resources/` and
put it in your project. The code uses ARC, so make sure to turn that on for the
files if you're not already using ARC. There's a dependency on
[`PHFDelegateChain`](https://github.com/fphilipe/PHFDelegateChain), so make sure
to add that to your project, too.

## Usage

The compose bar visible in the demo above was created as follows:

```objectivec
CGRect viewBounds = [[self view] bounds];
CGRect frame = CGRectMake(0.0f,
                          viewBounds.size.height - PHFComposeBarViewInitialHeight,
                          viewBounds.size.width,
                          PHFComposeBarViewInitialHeight);
PHFComposeBarView *composeBarView = [[PHFComposeBarView alloc] initWithFrame:frame];
[composeBarView setMaxCharCount:160];
[composeBarView setMaxLinesCount:5];
[composeBarView setPlaceholder:@"Type something..."];
[composeBarView setUtilityButtonImage:[UIImage imageNamed:@"Camera"]];
[composeBarView setDelegate:self];
```

To get notified of button presses, implement the optional methods from the
`PHFComposeBarViewDelegate` protocol:

```objectivec
@protocol PHFComposeBarViewDelegate <NSObject, UITextViewDelegate>

@optional
- (void)textBarViewDidPressButton:(PHFComposeBarView *)textBarView;
- (void)textBarViewDidPressUtilityButton:(PHFComposeBarView *)textBarView;

@end
```

Note that all methods from the `UITextViewDelegate` protocol are forwarded, so
you can add your own behavior to the text view such as limiting the text length
etc.

Refer to [`PHFComposeBarView.h`](Classes/PHFComposeBarView.h) for the available
properties and their descriptions.

## Small Print

### License

`PHFComposeBarView` is released under the MIT license.

### Dependencies

- [`PHFDelegateChain`](https://github.com/fphilipe/PHFDelegateChain)

### Author

Philipe Fatio ([@fphilipe](http://twitter.com/fphilipe))

