### fix

- iOS Browser 의 물리 키보드 사용시의 한글 IME 문제 — 조합 문자 (한글) 입력 중 Enter 시 마지막 글자가 다음 줄로 새던 문제 수정 (Enter 처리를 `keydown` → `beforeinput`으로 이전). #1654
- Tab 키 이동 시 화면 밖 숨김 요소(focus-temp, `aria-hidden`)에 포커스가 걸려 커서가 사라지던 문제 수정
