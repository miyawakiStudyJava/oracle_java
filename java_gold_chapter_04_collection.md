# chapter04 Collection

### ラッパークラス
### Boxing/Unboxing

基本データ型同士は、暗黙の型変換が行われる。
基本データ型　⇒　ラッパークラス

|インターフェース名|説明|
|---|---|
|List||
|Set ← SortedSet||
|Queue||
|Map ← SortedMap||

### Collectionインターフェースの主なメソッド

|戻り値|メソッド名|説明|
|---|---|---|
|boolean    |add(E e)||
|void       |clear()||
|boolean    |contains(Object obj)||
|boolean    |containsAll(Collection\<?>c||
|boolean    |isEmpty()||
|boolean    |remove(Object o)||
|boolean    |removeAll(Collection\<?>c||
|Iterator\<E>|iterator()||
|Object[]   |toArray()||
|\<T> T[]    |toArray(T[] array)||
|int size()|||

### Mapインターフェースの主なメソッド

|戻り値|メソッド名|説明|
|void|clear()||
|boolean|containsKey(Object key)||
|boolean|containsValue(Object vale)||
|V|get(Object key)||
|void|putAll()||
|V|remove(Object key)||
|int|size()||
|Collection\<V>|values()||

### Listインターフェースの主な実装クラス

|クラス名    |説明|同期性|
|---|---|---|
|ArrayList  |ランダムアクセスが高速|×|
|LinkedList |挿入と削除が高速|×|
|Vector     |マルチスレッド環境時|〇|

|クラス名    |説明|同期性|
|---|---|---|
|HashSet|未ソート|×|
|TreeSet|ソート済み|×|
|LinkedHashSet|挿入順|×|

### イテレーターの利用

|戻り値|メソッド名|説明|
|---|---|---|
|boolean|hasNext()||
|E|next()||
|default void|remove()||


### Queueインターフェースの主なメソッド

|操作|戻り値|メソッド名|例外|
|---|---|---|---|
|挿入|boolean|add(E e)||
||boolean|offer(E e)||
|削除|E|remove()||
||E|poll()||
|検査|E|element()|NoSuchElementExeption|
||E|peek|null|


### Dequeインターフェースの主なメソッド

  
先頭操作用メソッド
|操作|例外のスロー|特殊な値|説明|
|---|---|---|---|
|挿入|void addFirst(E e)  |boolean offerFirst(E e)|指定された要素を先頭に挿入する|
|削除|E removeFirst()     |E pollFirst()|キューの先頭を取得及び削除する|
|検査|E getFirst()        |E peekFirst()|キューの先頭を取得するが削除しない|

末尾操作用メソッド
|操作|例外のスロー|特殊な値|説明|
|---|---|---|---|
|挿入|void addLast(E e)  |boolean offerLast(E e)|指定された要素を先頭に挿入する|
|削除|E removeLast()     |E pollLast()|キューの先頭を取得及び削除する|
|検査|E getLast()        |E peekLast()|キューの先頭を取得するが削除しない|

### Map
NavigableMap:「指定されたキーに対し、もっとも近い要素を返す。」
- higherKey()
- lowerKey()

### ジェネリクスを用いたインターフェース宣言
```java
interface myIn<T>{void method(T t);}
class Foo implements MyIn<String>{
  public void method(String s){System.out.println(S);}
}
```

### 継承を使用したジェネリックス
```java
<T extends データ型>
```

### ワイルドカードを使用したジェネリックス
```java
Map<Integer, ?> map = method();
<? extends タイプ>
<? super タイプ>
```

### ComparableとComparatorインターフェース

```java
//Comparableインターフェース
//java.langパッケージ
public int compareTo(T o)

//Comparatorインターフェース
//java.utilパッケージ
public int compare(T o1,T o2)
```

### Comparatorインターフェースの主なメソッド

|メソッド|説明|
|---|---|
|naturalOrder()||
|reverseOrder()||
|nullsFirst()|nullを含めた比較を行う。nullは先頭になる。|
|nullsLast()|nullを含めた比較を行う。nullは末尾になる。|
|reversed()|Comparatorの逆順を義務付ける|


```java
Random rnd = new Random();
List<Integer> list = rnd
		.ints(1,100)
		.limit(10)
		.boxed()
		.collect(Collectors.toList());
list.forEach(i->System.out.printf("%d ", i));
System.out.println();
Collections.sort(list,Comparator.naturalOrder());
list.forEach(i->System.out.printf("%d ", i));
```

### ファクトリメソッド
List,Set,Mapの各インターフェースにstaticメソッドとしてof()メソッドが提供。

- 変更不可能 -> UnsupportedOperationExceptionが発生。
- set,listはnull要素を使用できない。 -> NullPointerExeptionが発生
- setの場合、重複する値は使用できない -> IllegalArgumentExceptionが発生
- mapの場合、重複するキーは使用できない -> IllegalArgumentExceptionが発生