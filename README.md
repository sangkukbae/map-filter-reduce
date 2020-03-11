# Map-Filter-Reduce

## [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
```javascript
var numberArray = [1,2,3,4,5,6,7,8,9,10];

//for 
var squareNumbers = [];
for (var counter=0; counter < numberArray.length; counter++){
   squareNumbers.push(numberArray[counter] * numberArray[counter])
}
console.log(squareNumbers);
```
```javascript
//forEach 
var squareNumbers1 = [];
numberArray.forEach(number => {
    squareNumbers1.push(number*number);
})
console.log(squareNumbers1);
```
```javascript
//es5 
var squareNumbers2 = numberArray.map(function(number){
     return number*number;
});
//es6 
var squareNumbers2 = numberArray.map(number => number*number);
```

```javascript
var persons = [
  {id : 1, name : "John", tags : "javascript"}, 
  {id : 2, name : "Alice", tags : "javascript"}, 
  {id : 3, name : "Roger", tags : "java"},
  {id : 4, name : "Adam", tags : "javascript"},
  {id : 5, name : "Alex", tags : "java"}
];
//es5 
var nameArray = persons.map(function(personObj){
      return personObj.name;
});
//es6 
var nameArray = persons.map(personObj => personObj.name);
```

## [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
```javascript
var numberArray = [1,2,3,4,5,6,7,8,9,10];

//for 
var evenNumbers = [];
for (var counter=0; counter < numberArray.length; counter++){
    if (numberArray[counter] %2 === 0){
        evenNumbers.push(numberArray[counter])
    }
}
console.log(evenNumbers);
```

```javascript
//forEach 
var evenNumbers1 = [];
numberArray.forEach(number => {
    if (number%2 === 0){
        evenNumbers1.push(number)
    }
})
console.log(evenNumbers1);
```

```javascript
// es5
var evenNumbers2 = numberArray.filter(function(number){
   return number%2===0;
});
// es6 
var evenNumbers2 = numberArray.filter(number => number%2===0);
console.log(evenNumbers2);
```

```javascript
var persons = [
  {id : 1, name : "John", tags : "javascript"}, 
  {id : 2, name : "Alice", tags : "javascript"}, 
  {id : 3, name : "Roger", tags : "java"},
  {id : 4, name : "Adam", tags : "javascript"},
  {id : 5, name : "Alex", tags : "java"}
];
//es5
var javscriptPersons = persons.filter(personObj => personObj.tags.indexOf("javascript") > -1);
//es6
var javscriptPersons = persons.filter(function(personObj){
   return personObj.tags.indexOf("javascript") > -1
});
```


## [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
```javascript
var numberArray = [1,2,3,4,5,6,7,8,9,10];

//for 
var sum = 0;
for (var counter=0; counter < numberArray.length; counter++){
     sum += numberArray[counter]
}
console.log(sum);
```
```javascript
//forEach 
var sum1 = false;
numberArray.forEach(number => {
     sum1 += number;
})
console.log(sum1);
```
```javascript
//es5 
var sum2 = numberArray.reduce(function(acc, num){
   acc += num;
   return acc;
}, 0);
//es6
var sum2 = numberArray.reduce(((acc, num) => acc + num), 0);
```

```javascript
var persons = [
  {id : 1, name : "John", tags : "javascript"}, 
  {id : 2, name : "Alice", tags : "javascript"}, 
  {id : 3, name : "Roger", tags : "java"},
  {id : 4, name : "Adam", tags : "javascript"},
  {id : 5, name : "Alex", tags : "java"}
];
//es5 
var uniqueTags = persons.reduce(function(acc, personObj){
    acc[personObj.tags] = 1;
    return acc;
},{});
//es6
var uniqueTags = persons.reduce((acc, personObj) => {
    acc[personObj.tags] = 1;
    return acc;
},{});
console.log(Object.keys(uniqueTags));
```

```javascript
var categories = [{
     type : "category1",
     cols : ["col A", "col B"]
}, {
     type : "category2",
     cols : ["col C", "col D", "col E"]
}, {
     type : "category3",
     cols : ["col F"]
}]
//es5
var colList = categories.reduce(function(acc, category){
    acc = acc.concat(category.cols);
    return acc;
}, []);
//es6
var colList = categories.reduce((acc, category) => {
    acc = acc.concat(category.cols);
    return acc;
}, []);
console.log(colList); //logs ["Col A", "Col B", "Col C", "Col D", "Col E", "Col F"];
```

**Iterating on Objects** :fire:
```javascript
const input = [123, 456, 789, 102, 345];
const output = input.reduce((accumulator, item, index) => {
    accumulator[`item-${index+1}`] = item;
    return accumulator;
}, {});
console.log(output); // {item-1: 123, item-2: 456, item-3: 789, item-4: 102, item-5: 345}
```

```javascript
const inObj = {'item-1': 123, 'item-2': 456, 'item-3': 789, 'item-4': 102, 'item-5': 345};
const outObj = Object.keys(inObj).reduce((accumulator, key, index) => {
    accumulator[`item-${index+1}`] = {
      label: `Item ${index+1}`,
      value: inObj[key],
    };
    return accumulator;
}, {});
console.log(outObj);

//   {item-1: {…}, item-2: {…}, item-3: {…}, item-4: {…}, item-5: {…}}
//    item-1: {label: "Item 1", value: 123}
//    item-2: {label: "Item 2", value: 456}
//    item-3: {label: "Item 3", value: 789}
//    item-4: {label: "Item 4", value: 102}
//    item-5: {label: "Item 5", value: 345}
 ```
 **filter-map-reduce chain**:fire:
 ```javascript
var numberArray = [1,2,3,4,5,6,7,8,9,10];
var evenNumberFilterFn = (number => number%2===0);
var squareMapFn = (number => number*number);
var sumFn = ((sum, number) => sum + number);

var sumOfSquareOfEvenNumbers = numberArray
                              .filter(evenNumberFilterFn)
                              .map(squareMapFn)
                              .reduce(sumFn,0);
console.log(sumOfSquareOfEvenNumbers)
```
 
 :memo: **참고 자료**
 * [https://medium.com/@JeffLombardJr/understanding-foreach-map-filter-and-find-in-javascript-f91da93b9f2c](https://medium.com/@JeffLombardJr/understanding-foreach-map-filter-and-find-in-javascript-f91da93b9f2c)   
 * [https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d](https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d) :heavy_check_mark:   
 * [https://medium.com/poka-techblog/simplify-your-javascript-use-some-and-find-f9fb9826ddfd](https://medium.com/poka-techblog/simplify-your-javascript-use-some-and-find-f9fb9826ddfd)   
 * [https://medium.com/front-end-weekly/stop-array-foreach-and-start-using-filter-map-some-reduce-functions-298b4dabfa09](https://medium.com/front-end-weekly/stop-array-foreach-and-start-using-filter-map-some-reduce-functions-298b4dabfa09)   
 * [https://time2hack.com/iterating-data-with-map-reduce-foreach-and-filter/](https://time2hack.com/iterating-data-with-map-reduce-foreach-and-filter/)   
 * [https://gist.github.com/alexhawkins/28aaf610a3e76d8b8264](https://gist.github.com/alexhawkins/28aaf610a3e76d8b8264)
