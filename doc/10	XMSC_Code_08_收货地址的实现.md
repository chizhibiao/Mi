# 10 XMSC_Code_08_收货地址的实现
## 10.1	任务描述
### 10.1.1 任务介绍
实现收货地址的添加、修改和删除等功能。
### 10.1.2	任务要求
* 参考小米网站，实现收货地址界面。
* 一行最多放三个地址，左边第一列放添加新地址
* 点击左边的添加新地址，弹出模态框添加数据。除了标签其他数据都必填，姓名和手机号码参考之前任务中的验证，邮政编码6位数字（更详细的验证要求请自行百度）。选择省/市/区/街道，改为三个select（省/市/区）。数据放在json文件中（自行编写数据），需实现三个下拉框之间的联动。保存后，页面添加一条收货地址数据。
* 在某项收货地址上点击修改，弹出模态框修改数据。
* 删除和修改数据后记得更新页面。
* 在某项收货地址上点击删除，询问用户是否要删除，确认后再删除。用自定义的模态框代替confirm函数
* 感兴趣的同学可以使用本地存储存放收货地址数据。

## 10.2	工作指导说明
    用户在个人中心页面，选个人中心菜单→收货地址菜单进入收货地址管理页面。 
### 10.2.1 实现UI
省略
### 10.2.2 页面初始化
1. 声明一个数组存放收货地址数据，并从本地存储中读取数据。
```javascript
var ADDRESS_KEY = 'Address';
var addresses = store.get(ADDRESS_KEY,[]);
```
2. 生成地址列表
```javascript
function renderAddressList(addresses){
  var html = '';
  for(var i = 0, len = addresses.length; i < len; i++){
    html += renderAddressItem(addresses[i]);生成
  }
  $('#addressList').append(html);
}
//生成地址详情
function renderAddressItem(address){
  var html = '';
  //显示收货地址时需要把收货地址相关属性的值拼接在一起。
  //......代码省略
  return html;
}
renderAddressList(addresses);
```
3. 为添加收货地址的模态框中的保存按钮设置click事件
```javascript
$('#saveForAdd').on('click', function(){
  //实现参考 “实现添加地址功能”
});
```
说明：saveForAdd是添加收货地址的模态框中的保存按钮的id。
4. 为修改收货地址的模态框中的保存按钮设置click事件
```javascript
$('#saveForUpdate').on('click', function(){
  //实现参考 “实现修改地址功能”
});
```
说明：saveForUpdate是修改收货地址的模态框中的保存按钮的id。
5. 为详细收货地址中的修改和删除两个链接设置click事件
```javascript
//找到所有的删除链接的共同祖先，利用共同父元素的事件委托给子元素设置事件
$('#addressList').on('click','.delete',function(){
  //实现参考 “实现删除地址功能”
});

$('#addressList').on('click','.update',function(){
  //实现参考 “实现修改地址功能”
});
```
说明：addressList是共同父元素的id，delete和update是设置在两个链接上的class属性。
### 10.2.3 实现添加地址功能
1. 数据验证
省略
2. 自动生成id，取出数组中的最后一条地址数据的id，+1。
```javascript
var id = 1;//数组中没有地址数据时，添加的地址数据id的值为1
if(addresses.length > 0){
  id = addresses[addresses.length - 1].id + 1;
}
```
3. 每条收货地址数据用object类型存放，包含：id、姓名、手机号、省、市、区、详细地址、邮政编码和标签等属性。
```javascript
//属性右边的值，通过jQuery的选择器，找到相应的input和select
var address = {
  id:id,
  name:,
  phone:,
  province:,
  city:,
  districtOrCounty:,
  detailAddress:,
  postcode:
  label:
};

```
4. 保存新增的收货地址数据并更新界面
```javascript
addresses.push(address);
store.update(ADDRESS_KEY, addresses);
renderAddressItem(address);
```
### 10.2.4 实现删除地址功能
1. 要想删除或者修改数据，首先要找到需要删除或者修改数据的id。修改之前的renderAddressItem函数中的代码，找合适的元素添加自定义属性data-id,为自定属性设置收货地址id的值。
2. 找到收货地址的id
```javascript
var $a = $(this);
var id = $a.parent().data('id');//从自定义属性data-id中获得属性值，元素的遍历根据实际情况调整
```
3. 根据id查找数据
```javascript
/*for(var i = 0, len = addresses.length; i < len; i++){
  if(addresses[i].id === id){
    //需要给用户提示，确认要删除吗？
    addresses.splice(i,1);
    break;
  }
}*/
var index = addresses.findIndex(function(item){
  return item.id === id;
});
```
4. 如果有查到，保存数据并更新界面
```javascript
if(index != -1){
  //需要给用户提示，确认要删除吗？
  addresses.splice(index,1);
  store.update(ACCOUNT_KEY, addresses);
  $a.parent().parent().remove();//元素的遍历根据实际情况调整
}
```
### 10.2.4 实现修改地址功能

## 10.3	工作产品要求
收货地址的界面参考如下：
![收货地址管理界面](https://github.com/chizhibiao/Mi/raw/master/images/收货地址.png)

![收货地址修改界面](https://github.com/chizhibiao/Mi/raw/master/images/添加收货地址.png)

![收货地址详情界面](https://github.com/chizhibiao/Mi/raw/master/images/收货地址详情.png)
