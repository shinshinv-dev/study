- Init
```
echo "# modernJavascriptInit" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/shinshinv-dev/modernJavascriptInit.git
git push -u origin master
```

- 패스워드 변경시
```
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'
```


- 설정보기
```
git config -l'
```

- 저장소 복사
```
git clone http://....
```

- 기본 원격 저장소 설정
```
git push -u 원격저장소명
```

- 원격 저장소 등록
```
git remote add origin http://...
```

- 원격 저장소 이름 변경
```
git remote rename origin remote
```

- 원격 저장소 내려받고 rebase 하기
```
git pull --rebase
```

-
```

```





-
```

```
