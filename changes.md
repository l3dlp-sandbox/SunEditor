### feat

- Block handle 기능 추가 — 라인 사이드 핸들에서 hover/drag/액션 메뉴 제공
- SelectMenu 서브메뉴 지원
- `toolbar_innerWidth` / `innerWidth` 옵션 추가
- `slashCommand` 플러그인 추가 — Notion/Tiptap 스타일 명령 메뉴. 트리거 문자(기본 `/`)와 메뉴 아이템을 사용자가 지정 (`src/plugins/field/slashCommand.js`)
- `placeholder_line` 옵션 추가 — Notion 스타일 라인 placeholder. 커서가 빈 라인에 있을 때 해당 라인 위치에 출력. 기존 `placeholder`와 함께 켜져 있으면 포커스된 빈 라인에서는 라인 placeholder가 우선

### change

- Dropdown 플러그인 메뉴 생성 방식을 공통 메서드 기반으로 통일
    - `menu.initDropdownTarget(classObj, itemsOrNode, options?)` — 기존 `Node`(HTML 직접 작성) 인자에 더해 `Array<DropdownItem>`을 받아 내부에서 `<button>`/`<li>` markup을 생성 (기존 `Node` 시그니처 호환 유지)
    - `DropdownItem` 스키마: `{ command, value?, title, innerHTML, className?, attrs? }` — `title`은 `title`/`aria-label`에 동시 적용, `attrs`로 임의 data 속성 부여
    - `options`: `{ className?, prependHTML? }` — wrapper 추가 클래스, `<ul>` 내부 prepend HTML
    - 항목 등록 후 `menu.itemsMap[key]`에 item 배열이 보관되고 각 item의 `_element`에 렌더된 `<button>` 참조가 주입됨 — BlockHandle action menu가 이를 재사용해 dropdown submenu를 구성
    - 내장 dropdown 플러그인 10종(`align`, `blockStyle`, `font`, `hr`, `layout`, `lineHeight`, `list`, `paragraphStyle`, `template`, `textStyle`)이 신규 방식으로 마이그레이션 — 각 플러그인의 `CreateHTML(...)` 헬퍼가 `CreateItems(...)`로 대체됨
    - 데모 사이트의 custom dropdown plugin 가이드/예제도 신규 item 배열 방식으로 업데이트 필요
- wysiwyg `mousemove` 핸들러를 `requestAnimationFrame` 기반으로 코얼레스
- SelectMenu 항목 hover/active 색상을 푸른 톤으로 변경

### fix

- pageBreak 컴포넌트를 클릭해 선택한 뒤 Delete/Backspace로 삭제되지 않던 문제 — 컴포넌트 삭제 훅이 `destroy`에서 `componentDestroy`로 리네임되었으나 pageBreak launcher만 옛 이름을 유지해 발생 #1670
- 배포 타입(`types/`)의 `Hook.*`(component/modal/controller/browser/colorPicker/hueSlider) 타입이 깨져 있던 문제 수정
- SelectMenu: `left`/`right` 모드에서 좌우 flip이 좌표계 혼합으로 동작하지 않던 문제
- `list-style-position: inside`로 변경 — 글머리기호가 바깥으로 넘치지 않도록
- 컨트롤러가 wysiwyg-inner 내부 스크롤로 target이 가시 영역을 벗어나도 hide되지 않거나 에디터 가장자리에 걸려있던 문제 수정
- `documentType`에서 placeholder 위치가 어긋나던 문제 수정
- 빈 줄(`<br>`만 있는 줄)을 클릭한 뒤 Enter를 누르면 새 줄이 위에 생기고 커서가 원래 줄에 남던 문제 수정 — 빈 단락/리스트 항목/헤딩 모두 커서가 새 줄로 이동
- 선택 영역을 지정한 상태(줄 전체·여러 줄 전체 선택 포함)에서 Enter를 누를 때 커서가 위쪽 줄에 남던 문제 수정 — 커서가 아래 줄에 위치
- Firefox에서 빈 줄(Enter로 생성 등)의 backspace/delete가 동작하지 않던 문제 수정 #1671
- Table의 셀에 붙여널기시 자바스크립트 오류 발생으로 미작동하던 버그 수정 #1668
- HTML 정리 시 `&nbsp;` 등 공백만 있는 텍스트가 삭제되던 문제 수정 #1667
- `value` 등 HTML 정리 시 블록 요소 사이의 공백(`</p>\n<p>` 등)이 `<br>` 없는 죽은 라인(`<p></p>`)으로 변환되거나, 라인 내부 `<br>` 뒤의 줄바꿈(`<p><br>\n</p>`)이 공백으로 남던 문제 수정
- 빈 줄/빈 에디터에서 Enter 시 단락이 중복 생성(빈 에디터에선 wysiwyg 컨테이너 자체가 복제)되던 문제 수정 #1657
- 스크롤 컨테이너 안에 임베드된 에디터에서 PRE(코드블록) 안 Enter 시 스크롤이 줄이 아닌 PRE 블록 전체 기준으로 동작하던 문제 수정 — Enter 후의 실제 커서 위치 기준으로 스크롤하도록 변경
