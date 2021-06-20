# note-gdc

```
export default dragSource(ItemTypes.INSIGHT_PLACEHOLDER, InsightSource, collect)(AddInsightPlaceholder);
```
Nhận dragSource của "react-dnd" làm high order component, nó sẽ xét `ItemTypes.INSIGHT_PLACEHOLDER` là drop cái nào để highlight phần drop tương ứng.

![image](https://user-images.githubusercontent.com/61957094/122550725-3505ae00-d05e-11eb-8281-4887b2e3dc41.png)


item được drag nhận high order component là DragSource,
```
export default DragSource<IAttributeFilterDraggableOwnProps>(
    ItemTypes.ATTRIBUTE_FILTER,
    attributeFilterSource,
    collect,
)(AttributeFilterDraggable);
```
Phần có thể drop là được bọc = component DropTarget, ta có thể thấy là match bằng `ItemTypes.ATTRIBUTE_FILTER`
```
export default DropTarget<IDeleteDropZoneOwnProps>(
    ItemTypes.ATTRIBUTE_FILTER,
    squareTarget,
    collect,
)(DeleteDropZone);
```

###### Chart component
![image](https://user-images.githubusercontent.com/61957094/122647896-ba698b00-d150-11eb-83c6-95129dc234c7.png)

Cái chart component là component DrillModalVisualization

##### Chế độ edit mode
![image](https://user-images.githubusercontent.com/61957094/122661742-d2c0c080-d1b7-11eb-862f-6b73a86f83d4.png)

component `DashboardEditHeader` khi click vào function `onEditClick` sẽ chuyển thành chế độ edit mode. Và sẽ có biến cờ để biết là liệu có thay đổi cái chart không? Cái đó để khi mà user reload thì sẽ hiện popup confirm.
Đây là function gắn cờ xem có thay đổi hay không

```
export const editModeRequested = (postMessageContext?: IPostMessageContextContent) => (
    dispatch: Dispatch,
    getState: GetState,
) => {
    const appState = getState();
    const areAttributeFiltersMod = isAttributeFiltersModified(appState);
    const isDateFilterChanged = isSelectedDateFilterDifferentFromStored(appState);

    const action: IEditModeRequestedAction = buildMessage(ActionTypeKeys.EDIT_MODE_REQUESTED, {
        isDateFilterChanged,
        areAttributeFiltersMod,
        postMessageContext,
    });

    dispatch(action);
};
```
