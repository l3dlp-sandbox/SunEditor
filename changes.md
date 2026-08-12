### fix

- 하나의 인라인 래퍼가 이미지를 여러 개 감쌀 때(`<span><img><img></span>`) code view 전환이 실패하고 두 번째 이후 이미지가 유실되던 문제 수정 (`modules/contract/Figure` - `retainFigureFormat`)
- `plugins` 옵션을 배열 형식(`plugins: [image, link]`)으로 전달하면 플러그인이 등록되지 않고 에디터 생성이 실패하던 문제 수정 (`core/section/constructor`)
- `html.clean`이 커서가 들어갈 수 없는 빈 줄(`<br>` 없는 `<p></p>`)을 남기던 문제 수정 (`core/logic/dom/html`)
- 플러그인 `retainFormat` 훅에서 예외가 발생하면 `html.clean` 전체가 중단되던 문제 수정 — 이제 해당 요소만 건너뛰고 경고를 남긴 뒤 나머지를 계속 처리 (`core/logic/shell/pluginManager`) #1679
