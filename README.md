# 語

zaoqi

```racket
 #lang lang package: [lang](https://pkgs.racket-lang.org/package/lang)
```

## 1. 物

```racket
(等？ 甲 乙) -> 陰陽？
  甲 : (非 誤？)   
  乙 : (非 誤？)   
```

返回`甲`是否等於`乙`。

```racket
(首-尾？ 物) -> 陰陽？
  物 : (非 誤？)   
```

返回`物`是否是`(首-尾 之首 之尾)`。

```racket
(首-尾 首 尾) -> 首尾？
  首 : 物？        
  尾 : 列？        
```

沒有強制類型限制。

```racket
(首-尾.首 物) -> 物？
  物 : 首-尾？     
```

若`物`是`(首-尾 之首 之尾)`，返回`之首`。

```racket
(首-尾.尾 物) -> 物？
  物 : 首-尾？     
```

若`物`是`(首-尾 之首 之尾)`，返回`之尾`。

```racket
(空？ 物) -> 陰陽？
  物 : (非 誤？) 
```

返回`物`是否是`()`。

```racket
空 : 空？ = ()
```

```racket
(文？ 物) -> 陰陽？
  物 : (非 誤？) 
```

返回`物`是否是字符。

```racket
(名/文？ 物) -> 陰陽？
  物 : (非 誤？)   
```

```racket
(名/文 物) -> 名-文？
  物 : (列 文？)   
```

沒有強制類型限制。

```racket
(名/文-1 物) -> (列 文？)
  物 : 名/文？         
```

沒有強制類型限制。

```racket
(名/構？ 物) -> 陰陽？
  物 : (非 誤？)   
```

```racket
(名/構 名 列) -> 陰陽？
  名 : 名？        
  列 : 列？        
```

沒有強制類型限制。

```racket
(名/構.名 物) -> 名？
  物 : 名/構？     
```

沒有強制類型限制。

```racket
(名/構.列 物) -> 列？
  物 : 名/構？     
```

沒有強制類型限制。

```racket
(集/定？ 物) -> 陰陽？
  物 : (非 誤？)   
```

```racket
集/定/空 : 集/定？
```

```racket
(集/定.增 物 名 甲) -> 映？
  物 : 集/定？         
  名 : 物？           
  甲 : 物？           
```

```racket
(集/定.改 物 名 機) -> 映？
  物 : 集/定？         
  名 : 物？           
  機 : (-> 物？ 物？)   
```

```racket
(集/定.增-改 物 名 甲) -> 映？
  物 : 集/定？           
  名 : 物？             
  甲 : 物？             
```

返回創建或修改了的`"集/定"`。

```racket
(集/定.取 物 名) -> 物？
  物 : 集/定？       
  名 : 物？         
```

```racket
(集/定.含？ 物 名) -> 陰陽？
  物 : 集/定？         
  名 : 物？           
```

```racket
(集/定.删 物 名) -> 映？
  物 : 集/定？       
  名 : 物？         
```

必須有，才能刪。

```racket
(集/定→列 物) -> (listof (cons/c any/c any/c))
  物 : 集/定？                                
```

```racket
(！式 甲 ...)
```

使用一個`引機？`。可以寫作`{甲 ...}`。

```racket
(！頂 名)
```

頂層的物。

```racket
(機？ 物) -> 陰陽？
  物 : (非 誤？) 
```

```racket
(機 形 物) -> 機？
  形 : 物？     
  物 : 未算？    
```

沒有強制類型限制。

```racket
(機.用 物 形) -> 物？
  物 : 機？       
  形 : 物？       
```

用`形`應用`物`。 `(算 (機.物 物) -境)`。 `-境`只包含用`(機.形 物)`和`形`得到的。

如果`形`和`物`不能匹配，這個`誤？`是`形`產生的。

```racket
(機.形 物) -> 物？
  物 : 機？     
```

類似Scheme。

```racket
(機.物 物) -> 未算？
  物 : 機？      
```

```racket
列 : 機？ = (機 '(列) '列)
```

```racket
名？ : 機？ = (機 '(物) '((！頂 陰陽.若) ((！頂 名/構？) 物) #t ((！頂 名/文？) 物)))
```

```racket
陰 : 陰陽？
```

```racket
陽 : 陰陽？
```

```racket
(陰陽.若 物 甲 乙) -> 物？
  物 : 陰-陽？        
  甲 : 物？          
  乙 : 物？          
```

若`陰陽`是`陽`，則返回`乙`，否則返回`丙`。

```racket
(式？ 物) -> 陰陽？
  物 : (非 誤？) 
```

```racket
(式 機) -> 式？             
  機 : (-> 映？ 未算？ ... 物？)
```

沒有強制類型限制。 first-class的宏和特殊形式。

```racket
(式-1 物) -> (-> 映？ 未算？ ... 物？)
  物 : 式？                     
```

沒有強制類型限制。

```racket
引 : 引機？ = (式 (機 '(集/定 物) '物))
```

```racket
(誤？ 物) -> 陰陽？
  物 : 物？     
```

```racket
(誤 物) -> 誤？
  物 : 物？   
```

```racket
(誤-1 物) -> 物？
  物 : 誤？     
```

```racket
(算 物 集/定) -> 物？
  物 : 未算？      
  集/定 : 映？     
```

```racket
集/定/頂 : 映？
```

```racket
{定 ([名 之物] ...) 物}
```

`letrec`

```racket
(構？ 物) -> 陰陽？
  物 : (非 誤？) 
```

返回`甲`是否是`(構 名 列)`。

```racket
(構 名 列) -> 構？
  名 : 名？     
  列 : 列？     
```

沒有強制類型限制。

```racket
(構.名 物) -> 物？
  物 : 構？     
```

若`甲`是`(構 名 列)`，返回`名`。

```racket
(構.列 物) -> 物？
  物 : 構？     
```

若`甲`是`(構 名 列)`，返回`列`。

```racket
(取 名) -> 物
  名 : 名？  
```

獲取一個包

```racket
(或 甲 乙) -> 物？
  甲 : 物？     
  乙 : 物？     
```

一般是`甲`，可以是`乙`。

## 2. 誤

### 2.1. 停機

實現應該識別出儘量多的停機，改爲`(誤 (構 {引 誤/界/停} -未定義))`，`-未定義`是一個`物？`。

### 2.2. 內置

`"沒有強制類型限制。"`在一些構建數據的`機？`中出現，表示特定的某些參數或返回值的類型可以是任何`物？`。

`(非 誤？)`表示不能是一個`誤？`，否則返回值是一個`誤？`。

#### 2.2.1. 機

內置的任何`機？`產生的`誤？`是`(誤 (構 {引 誤/界/機} (列 -名 -式 -位)))`，
`-名`是它的名稱，`-式`是它的參數，`-位`是產生一個`誤？`的參數的名稱。

#### 2.2.2. 式

內置的任何`式？`產生的`誤？`是`(誤 (構 {引 誤/界/式} (列 -名 -集/定 -式 -位)))`，
`-名`是它的名稱（一個`名？`），`-集/定`是環境，`-式`是它的參數，`-位`是參數的名稱。

#### 2.2.3. 未定義

`算`和`！頂`未定義時產生的`誤？`是`(誤 (構 {引 誤/界/名} (列 -名
-集/定)))`，`-名`是那個`名？`，`-集/定`是環境。
