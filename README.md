# Promise

> **Promise** in JS is like promising that i will response you once my **async task** is resolved *(promise fulfilled)*, or i will tell you if i was not able to do that task *(promise broken / rejected from completing it)*

## States of Promsie :

> `pending`: initial state, neither fulfilled nor rejected.
> `fulfilled`: meaning that the operation was completed successfully.
> `rejected`: meaning that the operation failed.

## Construction :

```JS
let promise = new Promise(function(resolve , reject )){
    // async task
}
// resolve and reject are actually functions passed as parameters to callback of Promise object 
```

## then

> what we will do when promise is fulfilled , **( then what ? )**
> whatever passed as parameters to **resolve()** can be used through **then()**

```JS
let promise = new Promise( function(resolve, reject){
    setTimeout(()=>{
        let response = "res"
        console.log("inside timeout");
        resolve(response``);
    } , 1000)
});

promise.then( (response)=> {
    console.log(response);
} );
/* Output : 
inside timeout
res
*/
```

> another method :

```JS
new Promise( function(resolve, reject){
    setTimeout(()=>{
        let response = "res"
        console.log("inside timeout");
        resolve(response);
    } , 1000)
}).then((response)=>{console.log(response);});
```

## catch

> what we will do when promise is rejected ?
> whatever passed as parameters to **reject()** can be used through **catch()**
> if reject() is invoked and we don't have catch() called , it will throw a runtime error

```JS
let promise = new Promise((resolve , reject)=>{
    let error = true ; 

    if(error){
        reject("Error");
    }
});

promise.catch((err)=>{console.log(err)});
// Output : Error 
```

> another method :

```JS
new Promise( function(resolve, reject){
    let error = true ; 

    if(error){
        reject("Error");
    }
}).catch((err)=>{console.log(err);});
```

## finally

> it will execute every time wheter promise is fulfilled or rejected

```JS
promise.catch( ()=>{...}).finally( ()=>{...} );

promise.finally( ()=>{...} );
```

## chaining :

> what is returned from first is then passed as parameters to second

```JS
promise.then( ()=>{
    return ___ ;
}).then( (___) => {
    return ___;
}).then( (___) => {
    ----
}).catch( () => {
    ----
}).finally( () => {
    ----
});
```

# Async Await

> it is another method of making async functions/methods

```JS
async function fun(...){

    let response = await __async-task___ ;
    ...
    ...
    return ... ;
}

fun(); 
// this fun will only be called when the async task reponse , till that , the function will wait.
```

> sometimes an error can also be there from async task , for that , wrap the code in try-catch

```JS
async function fun(...){
    try{
    let response = await __async-task___ ;
    ...
    ...
    return ... ;}
    catch{
        return error ;
    }
}

let result = fun();
```

> we can consume promises using async await as well

```JS
async function fun(...){
    try{
    let response = await promise ;
    ...
    ...
    return ... ;}
    catch{
        return error ;
    }
}

let result = fun();
```

# Fetch :

> sucessor for xmlHttpRequest
> fetch only returns network errors (not able to send request) as reject() , all other error that are returned from network side as response ( like 404 , etc) .

```JS
fetch("__URL___").then( () => {
    ....
}).catch( ()=>{
    ....
});
```

```JS
fetch(`https://api.github.com/users/manmohit-singh24`).then((response)=>{

    // Converting to json is also an async task as it may not response immediately , so we need to create a promise for this as well .
    new Promise( (resolve , reject)=> {
        resolve(response.json());
    }).then((response)=>{
        console.log(response.login);
    });

})

    // -----or----
fetch(`https://api.github.com/users/manmohit-singh24`).then((response)=>{ 
  
    async function fun (response) {
        let res = await response.json();
        console.log(res.login);
    }

    fun(response)  
})
```

> Fetch returns a Promise object

```JS
let response = fetch('...'); 
// response -> promise 
```
