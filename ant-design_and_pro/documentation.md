# ProTable frontend
## Attributs in proTable
1. Columns
2. Pagination{showQuickJumper, pageSize: how many items in a page}
3. actionRef
4. rowKey ?
5. toolbarRender
6. search(false, {defaultCollapsed, optionRender({searchText, resetText}, {form} => [])})
7. dateFormatter
8. headerTitle
9. request(function)
10. options

## Attributs in Column attribute
### Title
### Width
### Dataindex
### render(func(currentDataUnit, wholeData, currentRowIndex, action))
#### syntax: 
```javascript
columns = [{
...
render: function callback(unknown1, wholeDataUnit, currentRowIndex, unknown2, currentObject) => {
// return react node expected to render
}
}]
```
#### parameters:
**callback**
Function used to replace original built-in render function, taking 5 values in total
* unknown1
* wholeDataUnit
  the whole data unit which is an object received from backend.
for example:
```javascript
{
key: 3
last_edit_time: "2020-11-10T07:41:17.942Z"
news_content: "test"
news_id: 3
news_title: "新闻标题 3"
news_type_id: 1
news_type_name: "会展信息"
publish_time: "2020-11-10T07:41:17.942Z"
setTop: {isTop: false, settingTime: "2020-11-10T07:41:17.942Z"}
thumbnail_image: "https://via.placeholder.com/100x80"
}
```

  * currentRowIndex
indicate the index of current row.
  * unknown2
based on what i read on documentation supplied by ant design, this parameter is so called action, specific function is still unknown
  * currentObject
for example:
```javascript
/*
* it has column like this
* column = [
* {},{}
* {
*     title: '操作',
      dataIndex: 'option',
      valueType: 'option',
      render: (_, record, a, b, c, d) => {
        console.log(_, record, a, b, c, d);
        return (
          <>
            <a href="">置顶</a>
            <Divider type="vertical" />
            <a
              onClick={() => {
                handleUpdateModalVisible(true);
                setStepFormValues(record);
              }}
            >
              编辑
            </a>
            <Divider type="vertical" />
            <MoreButton item={record} />
          </>
        );
      },
* }
* ]
*
*/
{
dataIndex: "option"
render: ƒ render(_, record, a, b, c, d)
title: "操作"
valueType: "option"
}
```
#### return value
react node

### Align
### Sorter: (a, b) => a.attr - b.attr
### initialValue
### valueEnum ?
### Key ?
### valueType (select, date, option)
### ellipsis
### copyable
### Tip
### formItemProps{     
	 rules: [
        {
          required: true,
          message: '此项为必填项',
        },
      ],}
### Search
### Filters
### Request ?
### Fixed (left)
### renderFormItem

# ProTable backend
## response

```javascript
const result = {
    data: dataSource,
    total: newsSourse.length,
    success: true,
    pageSize,
    current: parseInt(`${params.currentPage}`, 10) || 1,
  };
  return res.json(result);
```

it's supposed to return a object like the pattern as above, which has attributes as below

### total
total indicates the number of pages the frontend will receive.
