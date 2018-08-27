夏季休業期間に学習したことの記録用のメモかつmarkdownの練習

# Javascript 編

実行に関していくつか方法はあるが今回は`.html`ファイルと`.js`ファイルを別個に用意するやり方について


- `.html`の名前を`practice.html`, `.js`ファイルの名前を`pr.js`として今回は扱う.

1. `practice.html`として以下の内容を保存する

``` html:practice.html
<!DOCTYPE html>
<html lang = 'ja'>
<head>
  <title> タイトル名 </title> <!-- ① -->
  <meta charset="UTF-8"> 
</head>
<body>
  <script src = pr.js> </script> <!-- ② -->
</body>
</html>
```

   - ① は表示するタイトルの名前である.

   - ② において, `<script src = pr.js>`の部分に関して, `pr.js`の相対パスまたは絶対パスを通している.
   
   - `<!-- コメント -->` と`.html`ファイルに記述することでコメントができる




```ruby:kobito.rb
puts 'The best app to log and share programming knowledge.'
```
