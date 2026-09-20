# 변경 보고서

공통 규칙(`.cursor/rules/harness-core.mdc`)을 따른다. 금지 행위와 근거 표기는 그 규칙을 참조하고, 여기서 반복하지 않는다.

역할: 실제 변경과 테스트·검토 기록을 모아 보고서를 만든다. `src/`를 추가로 고치지 않는다.

대상 작업: 이 대화에서 진행한 `harness/records/<YYYY-MM-DD-짧은설명>/` 폴더. 어느 작업인지 불분명하면 개발자에게 묻고 멈춘다.

## 절차

1. 아래 조회만으로 실제 변경을 확인한다. Git 상태를 바꾸지 않는다. staged·untracked도 포함한다.
   - `git status --short -- src/`
   - `git diff HEAD -- src/`
   - `git ls-files --others --exclude-standard -- src/`
   untracked 파일 내용은 `git add` 없이 Read로 확인한다.
2. `record.md`의 예상 변경 파일과 비교해 세 가지로 분류한다.
   - 예상대로 변경됨
   - 예상했으나 변경 안 됨
   - 예상 밖 변경 → 오류가 아니라 **확인 대상**으로 표시한다.
   Git 조회에 없는 파일은 실제 변경에 적지 않는다.
3. 같은 폴더의 `test-result.md`, `review.md`를 읽는다. 없으면 결과를 만들어 내지 말고 `NOT_TESTED` / 추가 확인 필요로 둔다.
4. `record.md`의 아래 구역만 채운다. 앞 단계가 쓴 내용은 덮어쓰지 않는다.
   - 실제 변경: Git 조회 기준 파일, 예상 대비 차이와 사유
   - 검증: `test-result.md`의 실행 결과와 Tester가 추가한 테스트
   - 최종 상태: `test-result.md`에 `NOT_TESTED`/`FAIL`이 있거나 `review.md`가 `CHANGES_REQUIRED`이면 **추가 확인 필요**, 둘 다 문제 없으면 **완료**. 잔여 확인 사항도 적는다.
5. 같은 폴더에 `report.md`를 만든다. 구성은 아래만 쓴다. **`record.md`, `test-result.md`, `review.md`, Git 조회에 없는 내용은 넣지 않는다.**
   - 최초 수정 요청
   - 영향도 분석 결과
   - 실제 변경 파일
   - 변경 내용 요약
   - 테스트 실행 결과
   - Tester가 추가한 테스트
   - Reviewer 검토 결과 (`CHANGES_REQUIRED`이면 숨기지 말고 명확히 표시)
   - 남아 있는 위험 요소
   - 추가 확인 필요 사항
