# 語

zaoqi

```racket
 #lang lang package: [lang](https://pkgs.racket-lang.org/package/lang)
```

WIP:有錯誤

## 1. 物

```racket
(等？ 甲 乙) -> :陰-陽？
  甲 : (非 :誤？)    
  乙 : (非 :誤？)    
```

返回`甲`是否等於`乙`。

```racket
(:列/構？ 物) -> :陰-陽？
  物 : (非 :誤？)     
```

返回`物`是否是`(→:列/構 首 尾)`。

```racket
(→:列/構 首 尾) -> 首尾？
  首 : :物？         
  尾 : :列？         
```

沒有強制類型限制。

```racket
(:列/構.首 物) -> :物？
  物 : :列/構？      
```

若`物`是`(→:列/構 首 尾)`，返回`首`。

```racket
(:列/構.尾 物) -> :物？
  物 : :列/構？      
```

若`物`是`(→:列/構 首 尾)`，返回`尾`。

```racket
(:列/空？ 物) -> :陰-陽？
  物 : (非 :誤？)     
```

返回`物`是否是`()`。

```racket
:列/空 : 列/空？ = ()
```

```racket
(:名/文？ 物) -> :陰-陽？
  物 : (非 :誤？)     
```

```racket
(:名/構？ 物) -> :陰-陽？
  物 : (非 :誤？)     
```

```racket
(→:名/構 名 列) -> :陰-陽？
  名 : :名？           
  列 : :列？           
```

沒有強制類型限制。

```racket
(:名/構.名 物) -> 名？
  物 : :名/構？     
```

沒有強制類型限制。

```racket
(:名/構.列 物) -> :列？
  物 : :名/構？      
```

沒有強制類型限制。

```racket
(:集/定？ 物) -> :陰-陽？
  物 : (非 :誤？)     
```

```racket
空:集/定 : :集/定？
```

```racket
(:集/定.增 物 名 甲) -> :集/定？
  物 : :集/定？            
  名 : :物？              
  甲 : :物？              
```

```racket
(:集/定.改 物 名 機) -> :集/定？
  物 : :集/定？            
  名 : :物？              
  機 : (-> :物？ :物？)     
```

```racket
(:集/定.取 物 名) -> :物？
  物 : :集/定？        
  名 : :物？          
```

```racket
(:集/定.含？ 物 名) -> :陰-陽？
  物 : :集/定？           
  名 : :物？             
```

```racket
(:集/定.删 物 名) -> 映？
  物 : :集/定？       
  名 : :物？         
```

必須有，才能刪。

```racket
(:集/定→:列 物) -> (listof (cons/c any/c any/c))
  物 : :集/定？                                 
```

```racket
(#%式 式 甲 ...)
```

使用一個`引機？`（`式`）。可以寫作`{式 甲 ...}`。

```racket
(#%頂 名)
```

頂層的物。

```racket
(:機？ 物) -> :陰-陽？
  物 : (非 :誤？)   
```

```racket
(→:機 形 物) -> :機？
  形 : :物？       
  物 : :物？       
```

沒有強制類型限制。

```racket
(:機.用 物 形) -> :物？
  物 : :機？        
  形 : :物？        
```

用`形`應用`物`。 `(算 (:機.物 物) -境)`。 `-境`只包含用`(:機.形 物)`和`形`得到的。

如果`形`和`物`不能匹配，這個`誤？`是`形`產生的。

```racket
(:機.形 物) -> :物？
  物 : :機？      
```

類似Scheme。如果有不是`名？`的，也加入到`集/定`。後面的可以覆蓋前面的。

```racket
(:機.物 物) -> 未算？
  物 : :機？      
```

```racket
→:列 : :機？ = (→:機 '(:列) ':列)
```

```racket
:名？ : :機？                                                         
 = (→:機 '(:物) '((#%頂 :陰陽.若) ((#%頂 :名/構？) :物) #t ((#%頂 :名/文？) :物)))
```

```racket
陰 : :陰-陽？
```

```racket
陽 : :陰-陽？
```

```racket
(:陰陽.若 物 甲 乙) -> :物？
  物 : 陰-陽？          
  甲 : :物？           
  乙 : :物？           
```

若`陰陽`是`陽`，則返回`乙`，否則返回`丙`。

```racket
(:式？ 物) -> :陰-陽？
  物 : (非 :誤？)   
```

```racket
(→:式 機) -> :式？              
  機 : (-> :集/定？ :物？ ... :物？)
```

沒有強制類型限制。 first-class的宏和特殊形式。

```racket
(→:式-1 物) -> (-> :集/定？ :物？ ... :物？)
  物 : :式？                          
```

沒有強制類型限制。

```racket
引 : 引機？ = (→:式 (→:機 '(:集/定 :物) ':物))
```

```racket
(:誤？ 物) -> :陰-陽？
  物 : :物？       
```

```racket
(→:誤 物) -> :誤？
  物 : :物？     
```

```racket
(→:誤-1 物) -> :物？
  物 : :誤？       
```

```racket
(算 物 集/定) -> :物？
  物 : :物？       
  集/定 : :集/定？   
```

```racket
頂:集/定 : :集/定？
```

```racket
{定 ([名 之物] ...) 物}
```

`letrec`。`([名 之物] ...)`的名稱是

```racket
(:構？ 物) -> :陰-陽？
  物 : (非 :誤？)   
```

```racket
(->:構 :名 :列) -> :構？
  :名 : :名？         
  :列 : :列？         
```

沒有強制類型限制。

```racket
(:構.:名 物) -> :物？
  物 : :構？       
```

```racket
(:構.:列 物) -> :物？
  物 : :構？       
```

```racket
(取 名) -> 物
  名 : 名？  
```

獲取一個包

```racket
(或 甲 乙) -> :物？
  甲 : :物？     
  乙 : :物？     
```

一般是`甲`，可以是`乙`。

## 2. 頂層的物

### 2.1. 機

看起來是`(機 '<形> '((#%頂 <名>) . <形>))`。

### 2.2. 式

看起來是`(式 (機 '(集/定 . <形>) '((#%頂 算) ((#%頂 列) '#%式 (#%頂 <名>) .
<形>)`   `集/定)))`。

## 3. 誤

### 3.1. 停機

替換：在進行0或更多次替換後，可以把會停止的任意個`物？`替換爲`(→:誤 (構 {引 誤/界/停}
<未定義>))`，`<未定義>`是任意的一個`物？`。

實現應該識別出儘量多的停止。

實現應該儘量避免替換。

### 3.2. 內置

`"沒有強制類型限制。"`在一些構建數據的`機？`中出現，表示特定的某些參數或返回值的類型可以是任何`物？`。

`(非 :誤？)`表示不能是一個`誤？`，否則返回值是一個`誤？`。

#### 3.2.1. 機

內置的任何`機？`產生的`誤？`是`(誤 (構 {引 誤/界/機} (列 -名 -式 -位)))`，
`-名`是它的名稱，`-式`是它的參數，`-位`是產生一個`誤？`的參數的名稱。

#### 3.2.2. 式

內置的任何`式？`產生的`誤？`是`(誤 (構 {引 誤/界/式} (列 -名 -集/定 -式 -位)))`，
`-名`是它的名稱（一個`名？`），`-集/定`是環境，`-式`是它的參數，`-位`是參數的名稱。

#### 3.2.3. 未定義

`算`和`#%頂`未定義時產生的`:誤？`是`(→:誤 (構 {引 誤/界/名} (列 -名
-集/定)))`，`-名`是那個`名？`，`-集/定`是環境。

## 4. 類Racket語法

每個vector和symbol會被轉換爲一個`:名？`。

```racket
{define L->V                                                                                
{match-lambda                                                                               
 [(列 #\！ cs ..1) `#(一 式 ,(L->V cs))]                                                        
 [(列 #\# #\% cs ..1) `#(式 ,(L->V cs))]                                                      
 [(列 cs ..1 #\- #\1)                                                                        
  {match (L->V cs)                                                                          
[`#(一 ,t) `#(一 ,t 反)]                                                                       
[`#(一 ,t ,n) `#(一 ,t (反 ,n))]                                                               
[(? symbol? s) `#(反 ,s)]}]                                                                  
[(列 #\→ (and (not #\→) cs) ..1) `#(一 #(#(子 化 至) ,(L->V cs)))]                               
[(列 (and (not #\→) cs1) ..1 #\→ (and (not #\→) cs2) ..1) `#(一 #(化 ,(L->V cs1) ,(L->V cs2)))]
[(列 cs ..1 #\？) `#(一 #(子 化 乎) ,(L->V cs))]                                                  
[(列 (and (not #\.) t) ..1 #\. (and (not #\.) n) ..1) `#(一 #(#(子 化 對) ,(L->V t)) ,(L->V n))] 
[(列 #\: t ..1) `#(一 ,(L->V t))]                                                             
[(列 x ..1 #\: t ..1) `#(一 ,(L->V t) ,(L->V x))]                                             
[(列 a ..1 (or #\/ #\\) (and (not (or #\/ #\\)) b) ..1) `#(子 ,(L->V a) ,(L->V b))]           
[(列 (and (not #\-) h) ..1 #\- t ..1)                                                        
 {match (L->V t)                                                                            
[`#(列 ,@xs) `#(列 ,(L->V h) ,@xs)]                                                           
[s `#(列 ,(L->V h) ,s)]}]                                                                    
[(and xs (not (列 _ ... (or #\？ #\！ #\# #\% #\- #\1 #\→ #\. (or #\/ #\\) #\:) _ ...)))       
 (string->symbol (list->string xs))]}}                                                      
```
