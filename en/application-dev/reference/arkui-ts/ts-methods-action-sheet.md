# Action Sheet

An action sheet is a dialog box that displays actions a user can take.

>  **NOTE**
>
>  The APIs of this module are supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.


## Required Permissions

None


## ActionSheet.show

show(value: { title: string | Resource, message: string | Resource, confirm?: {value: string | Resource, action:() => void}, cancel?:()=>void, sheets: Array&lt;SheetInfo&gt;, autoCancel?:boolean, alignment?: DialogAlignment, offset?: { dx: number | string | Resource; dy: number | string | Resource } })

Defines and shows the action sheet.

**Parameters**

| Name       | Type                   | Mandatory | Description                         |
| ---------- | -------------------------- | ------- | ----------------------------- |
| title      | string \| [Resource](ts-types.md#resource) | Yes    |  Title of the dialog box.|
| message    | string \| [Resource](ts-types.md#resource) | Yes    | Content of the dialog box. |
| autoCancel | boolean                           | No    | Whether to close the dialog box when the overlay is clicked.<br>Default value: **true**|
| confirm    | {<br>value: string \| [Resource](ts-types.md#resource),<br>action: () =&gt; void<br>} | No | Text content of the confirm button and callback upon button clicking.<br>Default value:<br>**value**: button text.<br>**action**: callback upon button clicking.|
| cancel     | () =&gt; void           | No    | Callback invoked when the dialog box is closed after the overlay is clicked.  |
| alignment  | [DialogAlignment](ts-methods-custom-dialog-box.md#dialogalignment) | No    |  Alignment mode of the dialog box in the vertical direction.<br>Default value: **DialogAlignment.Default**|
| offset     | {<br>dx: Length,<br>dy: Length<br>} | No     | Offset of the dialog box relative to the alignment position.<br/>Default value: **{<br>dx: 0,<br>dy: 0<br>}** |
| sheets     | Array&lt;SheetInfo&gt; | Yes      | Options in the dialog box. Each option supports the image, text, and callback.|

## SheetInfo

| Name| Type                                                    | Mandatory| Description         |
| ------ | ------------------------------------------------------------ | ---- | ----------------- |
| title  | string \| [Resource](ts-types.md#resource) | Yes  | Sheet text.      |
| icon   | string \| [Resource](ts-types.md#resource) | No  | Sheet icon. By default, no icon is displayed.    |
| action | ()=&gt;void                                          | Yes  | Callback when the sheet is selected.|


## Example


```ts
// xxx.ets
@Entry
@Component
struct ActionSheetExample {

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Button('Click to Show ActionSheet')
        .onClick(() => {
          ActionSheet.show({
            title: 'ActionSheet title',
            message: 'message',
            confirm: {
              value: 'Confirm button',
              action: () => {
                console.log('Get Alert Dialog handled')
              }
            },
            sheets: [
              {
                title: 'apples',
                action: () => {
                  console.error('apples')
                }
              },
              {
                title: 'bananas',
                action: () => {
                  console.error('bananas')
                }
              },
              {
                title: 'pears',
                action: () => {
                  console.error('pears')
                }
              }
            ]
          })
        })
    }.width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001212058508](figures/en-us_image_0000001212058508.gif)
