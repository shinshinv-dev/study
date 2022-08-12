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

- pull merge 되돌리기 (복원하기)
```
git reset --head ORIG_HEAD
git reset --merge ORIG_HEAD
```

- 원격 브랜치 가져오기
```
# 원격 정보를 업데이트 한다.
git remote update

# 브랜치를 생성하고 가져온다.
git checkout -t origin/브랜치명

# 다른 브랜치를 생성하고 가져온다.
git checkout -b 새로운브랜치명 origin/브랜치명

# 브랜치가 아닌 커밋을 직접 참조한 상태에서 가져온다. Detached HEAD 라고한다.
git checkout origin/브랜치명
```

- 변경된 상태 초기화하기
```
# 특정 파일 변경 상태 초기화하기
$ git restore 파일명

# 스테이지 상태를 내리기
--stage

# 변경 상태 초기화 하기
$ git reset --hard 

--mixed               HEAD와 인덱스를 초기화
--soft                HEAD만 초기화
--hard                HEAD, 인덱스, 작업폴더를 초기화

# 변경사항 청소하여 정리하기
$ git clean -i -d

-d: 폴더까지 제거
```

- 현재 브랜치 변경하기
```
git switch 브랜치명
```

- 강제 원격저장소 push 하기
```
git push -u 원격저장소명 +브랜치명
```

- stash
```
$ git stash

or

# 현재 스테이지을 스태쉬에 저장하기
$ git stash save

# 저장된 스태쉬 목록보기
$ git stash list

# 스태쉬 적용하기
$ git stash apply stash@{0}

# 적용한 스태쉬 되돌리기 (복원하기)
$ git stash show -p | git apply -R

# 저장된 스태쉬 삭제하기
$ git stash drop stash@{0}
```

- 커밋 히스토리 변경 : rebase
```
$ git rebase -i @~3

-i: 인터랙티브 (상호간에 협의에 의해 결정하는 것) 즉 사용자가 리베이스할 커밋 목록을 편집할 수 있도록 한다.
@~3: 최근 3개의 커밋을 rebase 한다.
--root: 전체 커밋을 rebase 한다.

# p, <commit> 선택 = 커밋 사용
# r, reword <commit> = 커밋을 사용하지만 커밋 메시지를 편집합니다.
# e, edit <commit> = 커밋을 사용하지만 수정을 위해 중지
# s, squash <commit> = 커밋을 사용하지만 이전 커밋에 병합
# f, fixup <commit> = "squash"와 비슷하지만 이 커밋의 로그 메시지를 버립니다.
# x, exec <command> = 쉘을 사용하여 명령(나머지 줄) 실행
# b, break = 여기서 중지(나중에 'git rebase --continue'로 계속 리베이스)
# d, drop <commit> = 커밋 제거
# l, <label> 레이블 = 현재 HEAD에 이름으로 레이블 지정
# t, <label> 재설정 = HEAD를 레이블로 재설정

--continue 계속
--skip 현재 패치를 건너뛰고 계속
--abort 중단하고 원래 분기를 확인합니다.

코멘트변경

$ git commit --amend
```

- 커밋 히스토리 조회
```
# 2개 커밋 로그 출력

$ git log -p -2

# 커밋 로그 통계 출력

$ git log --stat

# 커밋 로그 한줄 출력

$ git log --pretty=oneline

# 커밋 로그 그래프로 보기

$ git log --pretty=oneline --graph

상태(log, diff, show) 출력시 사용할 수 있는 옵션
common diff options:
  -z            output diff-raw with lines terminated with NUL.
  -p            output patch format.
  -u            synonym for -p.
  --patch-with-raw
                output both a patch and the diff-raw format.
  --stat        show diffstat instead of patch.
  --numstat     show numeric diffstat instead of patch.
  --patch-with-stat
                output a patch and prepend its diffstat.
  --name-only   show only names of changed files.
  --name-status show names and status of changed files.
  --full-index  show full object name on index lines.
  --abbrev=<n>  abbreviate object names in diff-tree header and diff-raw.
  -R            swap input file pairs.
  -B            detect complete rewrites.
  -M            detect renames.
 ```

- 원격 브랜치 확인
```
$ git branch -r
```

- 원격 브랜치 삭제
```
$ git push origin --delete [branch name]
```
- 로컬 브랜치 삭제
```
$ git branch -d [branch name]
```
