### html5新特征总结

#### 语义化标签

优点： 1. 提升可访问性   2. SEO   3. 结构清晰，利于维护   

常见标签:  

- title
- h1~h6
- header
- nav
- article
- section 
- aside
- footer
- small
- strong 
- pre
- progress


#### 标签新属性

- dataset

```
<div id="food" data-drink="coffee" data-food="moka" data-meal="lunch">¥20.12</div>
<script>
    var food = document.getElementById('food')
    var typeOfDrink = food.dataset.drink
</script>
```

- classList

 - obj.classList.add()
 - obj.classList.remove()
 - obj.classList.contains()
 - obj.classList.toggle()
 - obj.classList.length()


#### 表单新类型

```
// email
E-mail: <input type="email" placeholder="please input your email"/>

// url
Url: <input type="url" placeholder="please input your url"/>

// number
Num: <input type="number" />

// range
Range: <input type="range" min="1" max="10" />

// autocomplete
E-mail: <input type="email" name="email" autocomplete="off" />

// autofocus
User name: <input type="text" name="user_name"  autofocus="autofocus" />
```