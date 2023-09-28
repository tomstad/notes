#面试题 


```js

function isEqual(obj1, obj2) {
  if(obj1 === obj2){
    return true
  }

  const obj1kes = Object.keys(obj1)
  const obj2kes = Object.keys(obj2)

  if(obj1kes.length !== obj2kes.length){
    return false
  }
  
  for (const key in obj1) {
    if (Object.hasOwnProperty.call(obj, key)) {

      const res = isEqual(obj1, obj2);
      if(!res){
        return false
      }
    }
  }

  return false
}

const o1 = {};
const o2 = o1;
console.log(isEqual(o1, o2)); // true

```