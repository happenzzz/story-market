# 이야기 시장

짝과 정해진 시간 동안 이야기를 나누고, 타이머가 끝나면 **한 번도 짝이 된 적 없는 친구**와 새 짝이 되도록 자리를 바꿔 주는 교실용 웹앱입니다. 서버 없이 HTML 파일 하나로 돌아가서 어느 반에서나 쓸 수 있어요.

## 폴더 구성

```
story-market/
├─ public/                  ← 실제로 인터넷에 올라가는 폴더
│  ├─ index.html            ← 이야기 시장 앱 (한 파일)
│  ├─ round-end-music.mp3   ← 타이머 종료 음악
│  ├─ names-template.xlsx   ← 이름 목록 예시 엑셀
│  └─ _headers              ← Cloudflare 캐시 설정 (수정하면 바로 반영되게)
├─ wrangler.jsonc           ← Cloudflare Workers로 올릴 때만 쓰는 설정
├─ .gitignore
└─ README.md
```

## 수업에서 쓰는 순서

1. **세팅** — 가장 빠른 방법은 **복사해서 붙여넣기**입니다. 엑셀·한글 명렬표에서 번호·이름 칸을 드래그해 복사(Ctrl+C)한 뒤, 이야기 시장 화면에서 Ctrl+V 하면 1분단 앞자리부터 바로 앉습니다. 번호 칸·빈 칸은 알아서 건너뛰고, `김 재 준`처럼 글자 사이가 벌어진 이름도 붙여 줍니다. 잘못 넣었으면 Ctrl+Z로 되돌립니다. 자리 입력칸을 연 상태에서 붙여넣으면 그 자리부터 채웁니다. 한 명씩 넣으려면 `입력 모드`를 켜고 자리를 눌러 이름을 씁니다. Enter를 누르면 다음 자리로 넘어가요. 또는 `엑셀로 가져오기`로 세로 이름 목록(xlsx·csv)을 넣으면 1분단 앞자리 왼쪽 → 오른쪽 → 다음 줄 → 2분단 순서로 채워집니다. 이름은 끌어다 놓으면 자리가 바로 바뀝니다.
2. **준비** — `준비`를 누르면 지금 앉은 자리가 1라운드 짝이 됩니다. 이 자리를 기준으로 한 번 짝이 된 친구와는 다시 짝이 되지 않게 배치해요.
3. **진행** — `1라운드 시작` → 타이머 종료(음악) → 화면에 새 자리가 날아가 표시 → 학생 이동 → `2라운드 시작`… 을 반복합니다.
4. 끝나면 `활동 끝내기`를 누르면 처음 자리로 돌아옵니다.

그 밖의 기능

- 이름·교실 모양·시간 설정은 브라우저에 자동 저장되어 다음에 켜도 그대로 나옵니다. 활동 중에 새로고침해도 이어서 할 수 있어요.
- `JSON 저장` / `JSON 불러오기`로 우리 반 명단을 파일로 보관하거나 다른 컴퓨터로 옮길 수 있습니다.
- `설정`에서 학급 이름, 분단 수(1~6), 분단별 짝 수(1~10), 종료 음악 바꾸기, 음량을 정할 수 있습니다.
- 책상 모양: `기본` / `모둠`(두 줄씩 한 모둠, 모둠 앞줄 책상을 세로로) / `탐구공동체`(양쪽 끝 분단 책상을 세로로).
- 일시정지 중이나 이동 시간에는 이름을 끌어 자리를 바꿀 수 있습니다. 키보드 스페이스바로 일시정지/계속할 수 있어요.
- 모든 친구와 한 번씩 짝이 되면, 그다음부터는 가장 오래전에 만난 짝부터 다시 만나도록 배치합니다.

> 엑셀(xlsx) 파일을 읽을 때만 인터넷에서 작은 도구(SheetJS)를 불러옵니다. 인터넷이 막힌 곳에서는 엑셀에서 이름 칸을 복사해 `붙여넣기` 칸에 넣으면 됩니다.

---

## GitHub에 올리기

1. <https://github.com> 에 로그인 → 오른쪽 위 `+` → **New repository**
2. Repository name: `story-market` (원하는 이름) → **Public** 선택 → **Create repository**
3. 새 저장소 화면에서 **uploading an existing file** 글자를 누릅니다.
4. 압축을 푼 `story-market` 폴더 **안에 있는 것들**(`public` 폴더, `README.md`, `wrangler.jsonc`)을 한꺼번에 끌어다 놓습니다.
   - `public` 폴더째로 끌어다 놓아야 합니다. 폴더 안 파일만 올리면 안 돼요.
   - `.gitignore`는 숨김 파일이라 안 보일 수 있는데, 없어도 괜찮습니다.
5. 아래쪽 **Commit changes** 를 누릅니다.

## Cloudflare Pages와 연결하기 (추천)

1. <https://dash.cloudflare.com> 로그인 → 왼쪽 메뉴 **Workers & Pages** → **Create** (또는 Create application)
2. **Pages** 탭 → **Connect to Git** (Import an existing Git repository) → GitHub 계정 연결 → `story-market` 저장소 선택 → **Begin setup**
3. 설정 칸은 이렇게 적습니다.
   - Framework preset: **None**
   - Build command: **(비워 두기)**
   - Build output directory: **public**
4. **Save and Deploy** → 1분쯤 뒤 `https://story-market.pages.dev` 같은 주소가 생깁니다.

이후에는 GitHub에서 `public/index.html`을 고쳐서 Commit 하면 Cloudflare가 자동으로 다시 배포합니다.

### 화면에 Pages 대신 Workers만 보일 때

Cloudflare 화면이 바뀌어 **Import a repository**(Workers)로만 연결되는 경우에도 그대로 진행하면 됩니다. 저장소에 들어 있는 `wrangler.jsonc`가 `public` 폴더를 올리도록 이미 설정되어 있어요.

- Build command: **(비워 두기)**
- Deploy command: `npx wrangler deploy` (기본값 그대로)

### GitHub 없이 바로 올리기

**Workers & Pages → Create → Pages → Upload assets(Drag and drop)** → 프로젝트 이름 입력 → `public` 폴더를 끌어다 놓기 → **Deploy site**.
