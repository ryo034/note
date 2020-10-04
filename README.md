# sample1
## sample1
### sample1
#### sample1
##### sample1
###### sample1

- sample1
- sample1
- sample1

* sample1
* sample1
* sample1
* sample1


1. テキスト
2. テキスト
    3. テキスト

1行目__（←半角スペース２つ）
2行目
<br>
<br>
3行目

`テキストやコード`

例： `int i = 0`

```js:sample.md
const sampe = false;
document.addEventListener('DOMContentLoaded', () => {
  const code = document.getElementsByTagName('code');

  Array.from(code).forEach(el => {
    if (el.className) {
      const s = el.className.split(':');
      const highlightLang = s[0];
      const filename = s[1];
      if (filename) {
        el.classList.remove(el.className);
        el.classList.add(highlightLang);
        el.parentElement.setAttribute('data-lang', filename);
        el.parentElement.classList.add('code-block-header');
      }
    }
  });
});
```

例：[Qiita](http://qiita.com/)

> テキスト
>> テキスト

例： ![qiita-square.png](https://qiita-image-store.s3.amazonaws.com/0/126861/90386757-fd96-8ba6-3477-485669713c55.png "qiita-square")

例： <img width="200" alt="qiita-square" src="https://qiita-image-store.s3.amazonaws.com/0/126861/90386757-fd96-8ba6-3477-485669713c55.png">

|a|b|c|
|-|-|-|
|a1|b1|c1|

<font color="Red">テキスト</font>

**テキスト**

*テキスト*

~~テキスト~~

***

[^1]: 注釈内容

例： \`インライン表示されなくなる`