
Q. 我為何學不會 list comprehension?
A.

* listcomp好像是造一個新的list
* 那在Ruby語言中，這會是 `Array#whatever ...` 也就是由資料來源物件來發動這件事
* 然後在Python中，每當我寫到了 `some_var = [ ` 然後就卡殼了…因為我不知道接下來的變數要寫啥

那麼今天我終於發現，要反著寫：

* 方括號先寫好來
* 在右方括號的左邊，寫上資料來源，比如 `[            a_list]` 這樣
* 決定要不要加上疊著呼叫的其他函數，比如 `enumerate` 函數，這裡就假裝要吧，那就是變成了  `[            enumerate(a_list)]` 
* 假設這時候資料來源的最終形式已經搞定了（以上式而言，至少會是一個 2-tuple 吧），那就可以進行下一步了：決定本 comprehension 中所要用的變數名稱；但是，but，容我再加一點東西：本步驟中要把 in 給加上了 =>  `[           in enumerate(a_list)]` 
* 若這是一個 2-tuple，因為 enumerate 函數之故，會是從 0 開始的一個整數，我命名為 idx；從串列中取出的東西，就叫 dungxi 好啦。於是本 comprehension 成了   `[          idx, dungxi in enumerate(a_list)]`
* 好心一點，把 for 加上   `[          for idx, dungxi in enumerate(a_list)]`
* 【插播一下】上面那個隱含了 `Python` 的一個實作法則："sequence unpacking" ，「一」個變數搞成了「二」個變數了
* 如果就原式輸出的話，還要考慮一下要不要再 tuple 化，那得 `(idx, dungxi)` 再加上括號才行。不過，也有可能會再呼叫其他函數加上後置處理，那就成了    `[ my_func(idx, dungxi) for idx, dungxi in enumerate(a_list)]` 。那一個簡單的(?) list comprehension 就完成了。
* 也許在來源部分還有 if statement （比如很多教材要在這裡分奇數偶數啥馬的），那就再加上就好囉。

