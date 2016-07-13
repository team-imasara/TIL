# 터미널에 서블라임 텍스트 단축 명령어 넣기

### 추가하기

```bash
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
```

### 삭제하기

`/usr/local/bin/` 에 `subl` 이라는 링크를 만들어준 것이니 이걸 다시 삭제하면 된다:

```bash
cd /usr/local/bin
rm subl
```