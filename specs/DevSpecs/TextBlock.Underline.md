# InputValidation

## Proposal Link
https://github.com/microsoft/AdaptiveCards/issues/3051

## Dependencies
No dependencies required

## Rendering

### UWP & .NET WPF

TextBlock has a property called [TextDecorations](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.textblock.textdecorations) which include Underline

### Android

#### TextBlock

TextBlocks are rendered using TextViews, TextView has a property called PaintFlags which include [Paint.UNDERLINE_TEXT_FLAG](https://developer.android.com/reference/android/graphics/Paint)

#### RichTextBlock

TextRuns are rendered using SpannableStrings, between the possible spans to use there is [UnderlineSpan](https://developer.android.com/reference/android/text/style/UnderlineSpan) 

### iOS

NSMutableAttributedString are able to set underlines in the whole text and in some specific ranges using [NSUnderlineStyle](https://developer.apple.com/documentation/uikit/nsunderlinestyle)

### .NET HTML

The \<u> tag allows underlining

## Feature Defaults

The underline property will have the <i>false</i> value by default signalizing that no underline is required

## Backwards Compatibility Concerns

Underline will be ignored if sent to an older version of the renderer. No breaking changes are introduced.

## Fallback impact

### 1.0 Fallback text
None

### 1.2 Element level fallback
None

## Warning and Error States
None

## Open Issues

### Feature extensibility
The property may include support multiple line underlining at some point which will make the property accept numerical values as well as boolean values

## Testing

### Object Model
All Object model test suites should be updated to validate the new property. 

#### Test suites that should be updated:
- Shared model, via the EverythingBagel tests.
- UWP Object Model unit tests
- Android object model tests.

### Samples
The following samples will be added to validate rendering:
- TextBlock.Underline.json file which contains TextBlock with underline

```
{
	"$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
	"type": "AdaptiveCard",
	"version": "1.3",
	"body": [
        {
			"type": "TextBlock",
			"text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
		},
		{
			"type": "TextBlock",
			"text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
			"underline": true
		},
		{
			"type": "TextBlock",
			"text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
			"underline": false
		}
	]
}
```

- RichTextRun.Underline.json file which contains a RichTextBlock that contains a TextRun with underline

```
{
	"$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
	"type": "AdaptiveCard",
	"version": "1.3",
	"body": [
		{
			"type": "RichTextBlock",
			"inlines": [
				"This is the first inline. ",
				{
					"type": "TextRun",
					"text": "This inline has default underline value. "
				},
				{
					"type": "TextRun",
					"text": "This inline must have underline. ",
					"underline": true
				},
				{
					"type": "TextRun",
					"text": "This inline must not have underline. ",
					"underline": false
				}
			]
		}
	]
}

```