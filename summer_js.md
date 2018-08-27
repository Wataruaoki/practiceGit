夏季休業期間に学習したことの記録用のメモかつmarkdownの練習

# Javascript 編

実行に関していくつか方法はあるが今回は`.html`ファイルと`.js`ファイルを別個に用意するやり方について


- `.html`の名前を`practice.html`, `.js`ファイルの名前を`pr.js`として今回は扱う.
1 `practice.html`として以下の内容を保存する
``` html
<!DOCTYPE html>
<html lang = 'ja'> <!-- ① --->
<head>
  <title> タイトル名 </title> <!-- ② -->
  <meta charset="UTF-8"> <!-- ③ -->
</head>
<body>
  <script src = pr.js> </script> <!-- ④ -->
</body>
</html>
```
   - ④ において, `<script src = pr.js>`の部分に関して, `pr.js`の相対パスまたは絶対パスを通す.
   
   - `<!-- コメント -->` と`.html`ファイルに記述することでコメントができる



