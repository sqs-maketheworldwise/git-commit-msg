# git-commit-msg

- .git/hooks/commit-msg

```shell
#!/bin/sh

COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat $COMMIT_MSG_FILE)

shopt -s nocasematch

case "$COMMIT_MSG" in
  # 신규 기능을 추가하는 경우
  Feat:* | feat:* | FEAT:*) sed -i '' -e '1s/^/✨ /' $COMMIT_MSG_FILE ;;
  # 실험적인 기능을 추가하는 경우 (for 퍼펭팀…)
  Experiment:* | experiment:* | EXPERIMENT:*) sed -i '' -e '1s/^/🐧 /' $COMMIT_MSG_FILE ;;
  # 빌드 작업, 패키지 관리자 구성의 업데이트 등 코드 변경이 없는 경우
  Chore:* | chore:* | CHORE:*) sed -i '' -e '1s/^/👷 /' $COMMIT_MSG_FILE ;;
  # 코드 병합
  Merge:* | merge:* | MERGE:*) sed -i '' -e '1s/^/🔀 /' $COMMIT_MSG_FILE ;;
  # 버그, 이슈 등 잘못된 무언가를 고치는 경우
  Fix:* | fix:* | FIX:*) sed -i '' -e '1s/^/🐛 /' $COMMIT_MSG_FILE ;;
  # 코드나 파일을 삭제하는 경우
  Remove:* | remove:* | REMOVE:*) sed -i '' -e '1s/^/🔥 /' $COMMIT_MSG_FILE ;;
  # 새 코드나 파일을 추가하는 경우
  Add:* | add:* | ADD:*) sed -i '' -e '1s/^/➕ /' $COMMIT_MSG_FILE ;;
  # 무언가를 구현한 경우, 구현한 대상을 강조할 때 사용 (Add와 비슷하지만 좀 더 큰 코드 단위 추가에 자주 쓰임)
  Implement:* | implement:* | IMPLEMENT:*) sed -i '' -e '1s/^/🎨 /' $COMMIT_MSG_FILE ;;
  # 구현을 위해 무언가를 사용한 경우, 특정 라이브러리나 프레임워크를 사용하기 위한 코드를 추가하는 경우
  Use:* | use:* | USE:*) sed -i '' -e '1s/^/📦 /' $COMMIT_MSG_FILE ;;
  # 코드를 리팩터링 하는 경우
  Refactor:* | refactor:* | REFACTOR:*) sed -i '' -e '1s/^/♻️ /' $COMMIT_MSG_FILE ;;
  # 무언가를 업데이트하는 경우
  Update:* | update:* | UPDATE:*) sed -i '' -e '1s/^/♻️ /' $COMMIT_MSG_FILE ;;
  # 문서를 수정하는 경우
  Docs:* | docs:* | DOCS:*) sed -i '' -e '1s/^/📝 /' $COMMIT_MSG_FILE ;;
  # 성능, 구조, 접근성 등을 개선하는 경우
  Improve:* | improve:* | IMPORVE:*) sed -i '' -e '1s/^/⚡️ /' $COMMIT_MSG_FILE ;;
  # 코드나 파일을 이동하는 경우
  Move:* | move:* | MOVE:*) sed -i '' -e '1s/^/🚚 /' $COMMIT_MSG_FILE ;;
  # 필요한 주석 추가 및 변경
  Comment:* | comment:* | COMMENT:*) sed -i '' -e '1s/^/💡 /' $COMMIT_MSG_FILE ;;
  # 코드 Formatting, 세미콜론 누락, console 삭제 등 코드 변경이 없는 경우
  Style:* | style:* | STYLE:*) sed -i '' -e '1s/^/🛠️ /' $COMMIT_MSG_FILE ;;
  # CSS 등 사용자 UI 디자인 변경
  Design:* | design:* | DESIGN:*) sed -i '' -e '1s/^/💄 /' $COMMIT_MSG_FILE ;;
  # 급하게 치명적인 버그를 고쳐야하는 경우
  Hotfix:* | hotfix:* | HOTFIX:*) sed -i '' -e '1s/^/🚑 /' $COMMIT_MSG_FILE ;;
  # 진행 중인 작업 (Work In Progress)
  Wip:* | wip:* | WIP:*) sed -i '' -e '1s/^/🚧 /' $COMMIT_MSG_FILE ;;
  # 변경 사항 되돌리기
  Revert:* | revert:* | REVERT:*) sed -i '' -e '1s/^/⏪ /' $COMMIT_MSG_FILE ;;
esac

shopt -u nocasematch
```

```shell
#!/bin/sh

COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat $COMMIT_MSG_FILE)

TYPE=$(echo $COMMIT_MSG | cut -d':' -f1)
MESSAGE=$(echo $COMMIT_MSG | cut -d':' -f2-)

case $TYPE in
  # 신규 기능을 추가하는 경우
  FEAT | Feat | feat)
    EMOJI="✨"
    ;;
  # 실험적인 기능을 추가하는 경우 (for 퍼펭팀…)
  EXPERIMENT | Experiment | experiment)
    EMOJI="🐧"
    ;;
  # 빌드 작업, 패키지 관리자 구성의 업데이트 등 코드 변경이 없는 경우
  CHORE | Chore | chore)
    EMOJI="👷"
    ;;
  # 코드 병합
  MERGE | Merge | merge)
    EMOJI="🔀"
    ;;
  # 버그, 이슈 등 잘못된 무언가를 고치는 경우
  FIX | Fix | fix)
    EMOJI="🐛"
    ;;
  # 코드나 파일을 삭제하는 경우
  REMOVE | Remove | remove)
    EMOJI="🔥"
    ;;
  # 새 코드나 파일을 추가하는 경우
  ADD | Add | add)
    EMOJI="➕"
    ;;
  # 무언가를 구현한 경우, 구현한 대상을 강조할 때 사용 (Add와 비슷하지만 좀 더 큰 코드 단위 추가에 자주 쓰임)
  IMPLEMENT | Implement | implement)
    EMOJI="🎨"
    ;;
  # 구현을 위해 무언가를 사용한 경우, 특정 라이브러리나 프레임워크를 사용하기 위한 코드를 추가하는 경우
  USE | Use | use)
    EMOJI="📦"
    ;;
  # 코드를 리팩터링 하는 경우
  REFACTOR | Refactor | refactor)
    EMOJI="♻️"
    ;;
  # 무언가를 업데이트하는 경우
  UPDATE | Update | update)
    EMOJI="♻️"
    ;;
  # 문서를 수정하는 경우
  DOCS | Docs | docs)
    EMOJI="📝"
    ;;
  # 성능, 구조, 접근성 등을 개선하는 경우
  IMPORVE | Improve | improve)
    EMOJI="⚡️"
    ;;
  # 코드나 파일을 이동하는 경우
  MOVE | Move | move)
    EMOJI="🚚"
    ;;
  # 코드나 파일을 이동하는 경우
  COMMENT | Comment | comment)
    EMOJI="💡"
    ;;
  # 코드 Formatting, 세미콜론 누락, console 삭제 등 코드 변경이 없는 경우
  STYLE | Style | style)
    EMOJI="🛠️"
    ;;
  # CSS 등 사용자 UI 디자인 변경
  DESIGN | Design | design)
    EMOJI="💄"
    ;;
  # 급하게 치명적인 버그를 고쳐야하는 경우
  HOTFIX | Hotfix | hotfix)
    EMOJI="🚑"
    ;;
  # 진행 중인 작업 (Work In Progress)
  WIP | Wip | wip)
    EMOJI="🚧"
    ;;
  # 변경 사항 되돌리기
  REVERT | Revert | revert)
    EMOJI="⏪"
    ;;
esac

# 타입의 첫 글자를 대문자로 변환하고 나머지는 소문자로 변환
FORMATTED_TYPE=$(echo ${TYPE:0:1} | tr '[:lower:]' '[:upper:]')$(echo ${TYPE:1} | tr '[:upper:]' '[:lower:]')

# 수정된 커밋 메시지 적용
echo "${EMOJI} ${FORMATTED_TYPE}:${MESSAGE}" > $COMMIT_MSG_FILE
```