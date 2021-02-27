## 集合

### 特征
- 元素确定性 (每一个元素都是真实存在的)
- 元素唯一性 (顾名思义,每一个元素都是唯一的)
- 元素无序性 (每个元素的排列没有先后顺序)

>**好了,我们先来观察laravel集合里面都有些什么,我们先在路由文件中写一个闭包函数查看该元素的类型.**
```php
Route::get('collect',function(){
    $data = collect([2,54,135,62,52,2]);
    dd($data);
});
```


>**访问一下浏览器,我们得到了一个Collection对象**
```html
Collection {#241 ▼
  #items: array:6 [▼
    0 => 2
    1 => 54
    2 => 135
    3 => 62
    4 => 52
    5 => 2
  ]
}
```

-- --
### 函数示例
- **avg()**
> 获取集合元素平均值
```php
Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->avg();
      dd($data);
});
```

> avg()返回结果
```html
 51.166666666667
```

-- --
 - **concat()**
 > 在元素结尾添加元素
 ```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->concat(['Test']);;
      dd($data);
 });
```
> 返回collect
 ```html
 Collection {#236 ▼
    #items: array:7 [▼
      0 => 2
      1 => 54
      2 => 135
      3 => 62
      4 => 52
      5 => 2
      6 => "Test"
     ]
  }
```
> 所以concat 会在集合结尾添加元素

-- --
- **contains()**
> 判断集合中是否包含该元素
 ```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->contains('54');
      dd($data);
    });
 
 //true
 ```
> 也可以用于判断元素
 ```html
  Route::get('collect',function(){
       $res = 0;
       $data = collect([2,54,135,62,52,2])->contains(function($val){
            return $val > 2;
       });
       dd($data);
   });
 
 //true
 ```

-- --
- **count()**
> 判断集合总数
 ```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->count('54');
      dd($data);
    });
 
 //6
 ```

-- --
- **countBy()**
> 判断集合总数
 ```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->countBy();
      dd($data);
    });
 ```
> 返回结果
 ```html
 Illuminate\Support\Collection {#267 ▼
 #items: array:5 [▼
      3 => 2
      55 => 1
      136 => 1
      63 => 1
      53 => 1
     ]
    }
 ```

-- --
 - **first()**
 > 获取集合第一条元素
 ```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->first();
      dd($data);
 });
 
 //2
 ```
> 我们可以添加一个回调函数加上判断条件
 ```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])
              ->first(function($val){
                  return $val > 3;
              });
      dd($data);
 });
 
 //54
 ```

-- --
- flatten()
> 将多维集合转化为一维
```php
 Route::get('collect', function () {
      $data = collect(['test' => '131654', 'index' => [1231, 551, 651], 'today' => 'hello'])
          ->flatten();
      dd($data);
    });
 ```
> flatten() 方法返回
 ```html
 Illuminate\Support\Collection {#261 ▼
 #items: array:5 [▼
      0 => "131654"
      1 => 1231
      2 => 551
      3 => 651
      4 => "hello"
     ]
    }
 ```

-- --
- map()
> 将集合内的元素进行计算，返回新的实例
```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2])->map(function ($index){
          $index += 1;
          return $index;
      });
      dd($data);
    });       
 ```
> map()返回结果
 ```html
 Illuminate\Support\Collection {#268 ▼
 #items: array:6 [▼
      0 => 3
      1 => 55
      2 => 136
      3 => 63
      4 => 53
      5 => 3
     ]
   }
 ```

-- --
- filter()
> 将集合内的元素进行计算，过滤为空,false,null的元素
```php
 Route::get('collect',function(){
      $data = collect([2,54,135,62,52,2,'',false,null])->filter()->all();
      dd($data);
  });
 ```
> filter()返回结果
 ```html
 array:6 [▼
   0 => 2
   1 => 54
   2 => 135
   3 => 62
   4 => 52
   5 => 2
 ]
 ```
