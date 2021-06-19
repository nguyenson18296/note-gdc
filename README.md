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
