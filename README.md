본 레포는 잘못된 커밋 내용 입력시 수정하는 방안과 사전에 방지하는 방법을 담고 있는 중

1. commit을 잘못 입력한 경우 -> git commit --amend 를 활용해 편집기로 수정시 반영되며
   임시 저장 파일은 .git/COMMIT_EDITMSG에 있음 해당 파일은 임시저장이기에 편집해도 원격저장소에 올라가는 커밋 내용이 바뀌지 않음

2. commit 내용의 확인을 위해 .git/hooks/pre-commit/commit-msg.sample을 수정 후
   commit-msg.sample -> commit-msg로 변경하여 chmod(change mode) +x 를 통해 실행 가능하게 변경 사실 ls -al 보면 실행모드긴 함 따라서 상관 없음 (본인 Pc마다 다름)

   본인은 대체적으로 commit 내용을 Gitmoji를 사용하기 때문에 Gitmoji가 아닌 경우 에러 메시지 출력이 가능하게 설정함
   [.git/hooks/commit-msg]
   커밋 메시지가 :star: 처럼 이모지로 시작하는지 검사 (이모지는 :"String": 형태)

   커밋 메시지 파일의 내용을 읽음
   COMMIT_MSG=$(cat $1)

   깃 이모지 패턴 확인 (여기서는 :sparkles:, :bug:, :memo:, :fire: 등을 예로 사용)
   if ! echo "$COMMIT_MSG" | grep -qE "^\:[a-zA-Z0-9\-]+\:"; then
   echo "Error: Commit message must start with a Gitmoji (e.g. :sparkles:, :bug:, :memo:, :fire:)"
   exit 1
   fi

pre-push 및 pre-commit은 추후에..
