
## bom

[UTF-8 BOMを確認・追加・削除するコマンド](https://qiita.com/take_3/items/5d602906b6b02b33c32a)

```
function unbom { LC_ALL=C sed -e $'1s/^\xef\xbb\xbf//'; }
function bom { LC_ALL=C sed -e $'1s/^/\xef\xbb\xbf/'; }
echo -n 'あ' | bom | unbom
```
