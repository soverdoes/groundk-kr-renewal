# Claude MCP 개념 및 설정 가이드

> **요약:** 비개발자 대상 Claude MCP 설치 가이드 — Filesystem, Notion, Slack, NotebookLM, Figma Console, YouTube, MCP Installer, Puppeteer, n8n 9종 설정 방법
>
> 상태: 완료 · 태그: AX, 정리 · 시작/완료: 2026-03-06

> 📌 이 문서는 Claude 앱에서 사용 중인 **MCP 서버 9종**을 본인의 PC에 설치하기 위한 가이드입니다.
> 개발 경험이 없어도 순서대로 따라하면 설정할 수 있도록 작성했습니다.

---

# MCP가 뭔가요?

MCP는 **Claude가 외부 서비스를 직접 사용할 수 있게 해주는 연결 도구**입니다.
예를 들어:

- "이 폴더에 있는 파일 목록 보여줘" → Claude가 내 PC 파일을 직접 탐색
- "Notion에서 금주 업무 찾아줘" → Claude가 Notion을 직접 검색
- "Slack에 메시지 보내줘" → Claude가 Slack에 직접 전송
- "Figma에서 이 컴포넌트 수정해줘" → Claude가 Figma를 직접 조작

> 💡 MCP 없이는 Claude가 "말만" 할 수 있지만, MCP가 있으면 Claude가 직접 "행동"할 수 있습니다.

---

# 사전 준비 (반드시 먼저!)

아래를 먼저 설치해야 합니다. 이미 설치되어 있다면 건너뛰세요.

## Node.js 설치

MCP 서버들이 Node.js 기반으로 동작하므로, 반드시 설치해야 합니다.

1. https://nodejs.org 접속
2. **LTS** 버전 다운로드 (왼쪽 초록색 버튼)
3. 설치 프로그램 실행 → 모두 "Next" 클릭하여 설치 완료

> ✅ **설치 확인:** 명령 프롬프트(cmd)를 열고 아래를 입력하세요.
> `node --version`
> `v18.x.x` 이상의 숫자가 나오면 성공입니다.

---

# MCP 서버 설치 가이드 (9종)

> 🔑 **설치 순서가 중요합니다!**
> **1번(Filesystem)**만 직접 설정 파일을 수정합니다. (딱 한 번!)
> 이것을 설치하면 Claude가 설정 파일을 직접 수정할 수 있게 되어, **2번부터는 Claude에게 말로 시키면 됩니다.**

---

## 1. Filesystem MCP — 가장 먼저 설치! (유일하게 직접 수정)

> 📁 **난이도:** ⭐⭐ (보통 — 설정 파일 복사/붙여넣기)
> **하는 일:** Claude가 지정된 폴더의 파일을 읽고, 쓰고, 검색할 수 있게 해줌
> **GitHub:** [modelcontextprotocol/servers - filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)

### 왜 가장 먼저 설치해야 하나요?

Filesystem MCP를 설치하면 Claude가 내 PC의 **설정 파일을 직접 수정**할 수 있게 됩니다.
즉, 이후 다른 MCP를 설정할 때 **"Claude, 설정 파일에 Figma 토큰 넣어줘"** 라고 말하면 Claude가 알아서 해줍니다.

### 설치 순서

**① 설정 파일 열기**
Claude 앱 좌측 상단 **☰ 메뉴** → **Settings** → **Developer** → **Edit Config** 클릭
`claude_desktop_config.json` 파일이 메모장으로 열립니다.

**② 아래 내용을 복사하여 설정 파일에 붙여넣기**

> ⚠️ **중요:** `본인계정이름` 부분을 실제 계정 이름으로 바꾸세요!
> 여러 폴더를 허용하고 싶으면 경로를 추가하면 됩니다.

**Windows의 경우:**

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:/Users/본인계정이름"
      ]
    }
  }
}
```

**Mac의 경우:**

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/본인계정이름"
      ]
    }
  }
}
```

이미 다른 설정이 있다면, `"mcpServers"` 안에 `"filesystem"` 부분만 추가하세요.

**③ 저장 후 Claude 앱 재시작**
파일을 저장하고 (Windows: Ctrl+S / Mac: Cmd+S), Claude 앱을 완전히 종료한 후 다시 실행합니다.

> ✅ **설치 확인:** Claude 앱을 재시작한 후, 채팅에서 **"내 바탕화면에 있는 파일 목록 보여줘"** 라고 말해보세요. 파일 목록이 나오면 성공!

> ⚠️ **보안 참고:** Claude는 설치 시 지정한 폴더 **안에서만** 파일을 읽고 쓸 수 있습니다. 지정하지 않은 폴더에는 접근할 수 없으니 안심하세요.

---

> 🎉 **여기까지 했으면 나머지는 정말 쉽습니다!**
> 이제부터는 Claude 앱 채팅창에 **아래 가이드의 회색 박스 내용을 그대로 복사/붙여넣기** 하면 됩니다.
> Claude가 설정 파일 수정부터 패키지 설치까지 알아서 처리해줍니다.
> 설치가 끝나면 **Claude 앱을 재시작**하세요.

---

## 2. Notion 연결

> 📝 **난이도:** ⭐ (매우 쉬움)
> **하는 일:** Notion 페이지 검색, 생성, 수정, 데이터베이스 조회

### 사전 준비: Notion API 키 발급

1. https://www.notion.so/my-integrations 접속
2. **새 API 통합 만들기(New integration)** 클릭
3. 이름 입력 (예: "Claude MCP") → 워크스페이스 선택 → **제출(Submit)**
4. **Internal Integration Secret** (API 키)을 복사합니다
5. Notion에서 Claude가 접근할 페이지/DB를 열고 → 우측 상단 **⋯** → **연결(Connections)** → 방금 만든 통합 추가

### 설치 방법

Claude에게 아래를 복사해서 붙여넣으세요 (API 키 부분을 실제 값으로 교체):

> 💬 (Claude에게 붙여넣기)
> Notion MCP를 설치해줘.
> `claude_desktop_config.json` 파일에 notion 설정을 추가해줘.
> - command: "npx", args: ["-y", "@notionhq/notion-mcp-server"]
> - env에 NOTION_API_KEY: "여기에 복사한 API 키 붙여넣기"

> 설치 후 Claude 앱을 **재시작**하세요. "Notion에서 OO 찾아줘"라고 말하면 됩니다.

---

## 3. Slack 연결

> 💬 **난이도:** ⭐ (매우 쉬움)
> **하는 일:** Slack 채널 읽기, 메시지 전송, 사용자 검색

### 설치 방법

Claude 앱에 **내장된 통합 기능**입니다. 별도 설정 파일 수정이 필요 없습니다.
Claude에게 아래를 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> Slack 연결해줘.

> Claude가 Slack 연결 방법을 안내해줍니다. 브라우저에서 로그인하면 됩니다.

---

## 4. NotebookLM 연결

> 📓 **난이도:** ⭐⭐ (보통)
> **하는 일:** Google NotebookLM 노트북 관리, 소스 추가, 오디오/비디오 생성, AI 리서치
> **GitHub:** [PleasePrompto/notebooklm-mcp](https://github.com/PleasePrompto/notebooklm-mcp)

### 설치 방법

Claude에게 아래를 그대로 복사해서 붙여넣으세요:

> ⚠️ 이 MCP는 전역 설치(`npm install -g`)가 필요합니다. 아래 프롬프트에 설치 명령어가 포함되어 있으니 Claude가 알아서 처리합니다.

> 💬 (Claude에게 붙여넣기)
> NotebookLM MCP를 설치해줘.
> 1. 먼저 `npm install -g notebooklm-mcp` 명령어로 전역 패키지 설치해줘
> 2. `claude_desktop_config.json` 파일에 notebooklm-mcp 설정 추가해줘 (command: "notebooklm-mcp", env에 NOTEBOOKLM_HL: "ko")
> 3. `nlm login` 명령어로 Google 인증 실행해줘

> Claude가 전역 패키지 설치, 설정 파일 수정, 인증까지 순서대로 처리해줍니다. 브라우저가 열리면 Google 계정으로 로그인하세요.
> 설치 후 Claude 앱을 **재시작**하세요.

---

## 5. Figma Console MCP

> 🖥️ **난이도:** ⭐⭐ (보통) — 토큰 발급 + 플러그인 설치 필요
> **하는 일:** Figma에서 디자인 직접 생성/수정/삭제, 컴포넌트 검색, 변수 관리
> **GitHub:** [southleft/figma-console-mcp](https://github.com/southleft/figma-console-mcp)

### 사전 준비 1: Figma 토큰 발급

1. 브라우저에서 [Figma](https://www.figma.com/) 접속 → 로그인
2. 좌측 상단 프로필 아이콘 → **Settings** 클릭
3. 아래로 스크롤 → **Security** 탭
4. **Personal access tokens** 섹션 → **Generate new token** 클릭
5. 이름 입력 (예: "Claude MCP") → **Generate** 클릭
6. **토큰을 복사**합니다 (이 화면을 벗어나면 다시 볼 수 없으므로 메모장에 붙여넣기!)

### 사전 준비 2: Figma Console 플러그인 설치

Claude가 Figma 파일을 조작하려면, 해당 파일에서 **Figma Console 플러그인**이 실행 중이어야 합니다.

1. Figma 데스크톱 앱에서 아무 파일을 엽니다
2. 상단 메뉴 **Resources** (혹은 플러그인 아이콘) 클릭
3. **Plugins** 탭 → 검색창에 **"Figma Console"** 검색
4. **Figma Console MCP** 플러그인 클릭 → **Run** (또는 **Save** 후 Run)
5. 플러그인 창이 열리면 **"Start"** 버튼 클릭

> 💡 플러그인 창에 **"MCP Ready"** 또는 **"Connected"** 상태가 표시되어야 Claude와 연결됩니다.
> Claude로 Figma 작업을 할 때마다 이 플러그인이 실행 중이어야 합니다.

### 설치 방법 — Windows

토큰을 발급했으면, Claude에게 아래를 복사해서 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> Figma Console MCP를 설치해줘.
> `claude_desktop_config.json` 파일에 figma-console 설정을 추가해줘.
> - command: "npx", args: ["figma-console-mcp@latest"]
> - env에 FIGMA_ACCESS_TOKEN: "여기에 복사한 토큰 붙여넣기", ENABLE_MCP_APPS: "true"

### 설치 방법 — Mac

Mac에서는 설정 파일 경로가 다릅니다. Claude에게 아래를 복사해서 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> Figma Console MCP를 설치해줘.
> `~/Library/Application Support/Claude/claude_desktop_config.json` 파일에 figma-console 설정을 추가해줘.
> - command: "npx", args: ["figma-console-mcp@latest"]
> - env에 FIGMA_ACCESS_TOKEN: "여기에 복사한 토큰 붙여넣기", ENABLE_MCP_APPS: "true"

> 토큰 부분만 실제 값으로 교체해서 붙여넣으세요. 설치 후 Claude 앱을 **재시작**하세요.

> ⚠️ **사용 전 체크리스트:**
> 1. Figma 데스크톱 앱에서 작업할 파일을 열었나요?
> 2. Figma Console 플러그인을 실행했나요?
> 3. 플러그인 상태가 **"MCP Ready"** 인가요?
> → 3가지 모두 예여야 Claude가 Figma를 조작할 수 있습니다.

---

## 6. YouTube MCP

> 🎬 **난이도:** ⭐ (매우 쉬움)
> **하는 일:** YouTube 영상의 자막/트랜스크립트를 가져와서 요약·분석
> **GitHub:** [anaisbetts/mcp-youtube](https://github.com/anaisbetts/mcp-youtube)

### 설치 방법

Claude에게 아래를 그대로 복사해서 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> YouTube MCP를 설치해줘.
> `claude_desktop_config.json` 파일에 mcp-youtube 설정을 추가해줘.
> - command: "npx", args: ["-y", "@anaisbetts/mcp-youtube"]

> 설치 후 Claude 앱을 **재시작**하세요.

---

## 7. MCP Installer

> 🔧 **난이도:** ⭐ (매우 쉬움)
> **하는 일:** 다른 MCP 서버를 Claude 안에서 바로 설치할 수 있게 해주는 유틸리티
> **GitHub:** [anaisbetts/mcp-installer](https://github.com/anaisbetts/mcp-installer)

### 설치 방법

Claude에게 아래를 그대로 복사해서 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> MCP Installer를 설치해줘.
> `claude_desktop_config.json` 파일에 mcp-installer 설정을 추가해줘.
> - command: "npx", args: ["-y", "@anaisbetts/mcp-installer"]

> 💡 이 MCP를 설치하면 앞으로 새로운 MCP를 추가할 때 Claude에게 **"OO MCP 설치해줘"** 라고 말하면 됩니다.

> 설치 후 Claude 앱을 **재시작**하세요.

---

## 8. Puppeteer MCP

> 🌐 **난이도:** ⭐ (매우 쉬움)
> **하는 일:** Claude가 브라우저를 직접 조작 — 웹페이지 열기, 스크린샷, 클릭, 입력 등
> **GitHub:** [modelcontextprotocol/servers - puppeteer](https://github.com/modelcontextprotocol/servers/tree/main/src/puppeteer)

### 설치 방법

Claude에게 아래를 그대로 복사해서 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> Puppeteer MCP를 설치해줘.
> `claude_desktop_config.json` 파일에 puppeteer 설정을 추가해줘.
> - command: "npx", args: ["-y", "@modelcontextprotocol/server-puppeteer"]

> 설치 후 Claude 앱을 **재시작**하세요.

---

## 9. n8n MCP

> ⚡ **난이도:** ⭐⭐⭐ (고급 — 관리자 설정 필요)
> **하는 일:** n8n 워크플로우 자동화 플랫폼을 Claude에서 직접 조회·실행
> **GitHub:** n8n-mcp (사내 구축)

> ⚠️ 이 MCP는 **사내 n8n 서버가 구축되어 있어야** 사용 가능합니다.
> 관리자에게 **n8n-mcp 파일 경로**, **API URL**, **API Key** 3가지를 받으세요.

### 설치 방법

관리자에게 받은 정보를 채운 후, Claude에게 아래를 복사해서 붙여넣으세요:

> 💬 (Claude에게 붙여넣기)
> n8n MCP를 설치해줘.
> `claude_desktop_config.json` 파일에 n8n-mcp 설정을 추가해줘.
> - command: "node", args: ["관리자에게 받은 파일 경로"]
> - env 설정:
>   - N8N_API_URL: "관리자에게 받은 n8n 서버 주소"
>   - N8N_API_KEY: "관리자에게 받은 API 키"
>   - MCP_MODE: "stdio"
>   - LOG_LEVEL: "error"
>   - DISABLE_CONSOLE_OUTPUT: "true"

> 관리자에게 받은 값으로 교체한 후 붙여넣으면, Claude가 설정 파일을 직접 수정해줍니다.
> 설치 후 Claude 앱을 **재시작**하세요.

---

# 설치 후 최종 확인

Claude 앱을 **재시작**한 후, 채팅에서 각 MCP가 잘 동작하는지 확인하세요:

- [ ] filesystem → "내 바탕화면 파일 목록 보여줘"
- [ ] Notion → "Notion에서 최근 페이지 검색해줘"
- [ ] Slack → "Slack에서 최근 메시지 보여줘"
- [ ] notebooklm-mcp → "NotebookLM 노트북 목록 보여줘"
- [ ] figma-console → "Figma에서 열린 파일 보여줘"
- [ ] mcp-youtube → "이 YouTube 영상 자막 가져와줘"
- [ ] mcp-installer → (다른 MCP 설치 시 자동 사용)
- [ ] puppeteer → "이 웹페이지 스크린샷 찍어줘"
- [ ] n8n-mcp → "n8n 워크플로우 목록 보여줘"

> 🚨 **안 되는 MCP가 있으면?**
> Claude에게 **"claude_desktop_config.json 파일 내용 보여줘"** 라고 말하세요.
> Claude가 설정 내용을 확인하고 문제를 찾아 수정해줍니다.

> 💡 **설정 파일 위치가 궁금하다면?**
> Claude 앱 **☰ 메뉴** → **Settings** → **Developer** → **Edit Config** 을 클릭하면 설정 파일이 열립니다.

---

# 문제가 생겼을 때 (FAQ)

<details>
<summary>Q. Node.js가 설치되어 있는지 모르겠어요</summary>

명령 프롬프트(cmd)를 열고 `node --version` 을 입력하세요. 버전 번호가 나오면 설치된 것입니다. "인식할 수 없는 명령" 이 나오면 Node.js를 설치해야 합니다.
</details>

<details>
<summary>Q. Filesystem MCP에서 "access denied" 에러가 나요</summary>

설치 시 지정한 폴더 밖의 파일에 접근하려고 할 때 발생합니다. Claude에게 **"claude_desktop_config.json 파일에서 filesystem의 접근 폴더에 D:/Works 추가해줘"** 라고 말하면 됩니다.
</details>

<details>
<summary>Q. Figma 토큰을 잃어버렸어요</summary>

Figma Settings → Security → Personal Access Tokens에서 기존 토큰을 삭제하고 **새로 발급**하면 됩니다.
</details>

<details>
<summary>Q. NotebookLM에서 "authentication error"가 나요</summary>

Claude에게 **"nlm login 실행해줘"** 라고 말하면 Google 계정으로 재인증할 수 있습니다.
</details>

<details>
<summary>Q. MCP 서버를 삭제하고 싶어요</summary>

Claude에게 **"claude_desktop_config.json 파일에서 OO MCP 설정 삭제해줘"** 라고 말하면 됩니다.
</details>

<details>
<summary>Q. 설정 파일이 꼬였어요 / MCP가 전부 안 돼요</summary>

Claude에게 **"claude_desktop_config.json 파일 내용 보여줘"** 라고 말하면 현재 설정을 확인할 수 있습니다. JSON 형식 오류를 Claude가 직접 수정해줍니다.
</details>

<details>
<summary>Q. 설정 파일을 직접 열고 싶어요</summary>

Claude 앱 **☰ 메뉴** → **Settings** → **Developer** → **Edit Config** 을 클릭하세요.
</details>

---

# 참고 링크

- [MCP 공식 사양](https://spec.modelcontextprotocol.io/)
- [MCP 서버 목록 (커뮤니티)](https://github.com/modelcontextprotocol/servers)
- [Filesystem MCP GitHub](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- [Figma Console MCP GitHub](https://github.com/southleft/figma-console-mcp)
- [NotebookLM MCP GitHub](https://github.com/PleasePrompto/notebooklm-mcp)

---

# ⚠️ Figma Console MCP — Windows 트러블슈팅 (2026-03-19)

Windows 환경에서 Figma Console MCP 플러그인이 연결되지 않는 문제와 해결법. Claude가 이 내용을 참고하여 자동으로 진단/해결할 수 있도록 정리.

## 【문제 1】 플러그인 "Scanning..." 반복 — serverVersion 0.0.0 버그 (핵심)

- **증상:** Desktop Bridge 플러그인 실행 시 "Scanning..." 깜빡임 반복, MCP Ready 녹색불 안 뜸
- **원인:** figma-console-mcp 서버가 SERVER_HELLO에서 serverVersion: "0.0.0"을 보냄 → 플러그인 bootloader(ui.html)가 버전 체크 실패 → full UI 로드 불가 (GitHub Issue #39, OPEN)
- **해결법:** ui.html을 ui-full.html로 교체하여 bootloader 프로토콜 우회

**Claude 해결 절차:**
- 1단계: npm 캐시에서 ui-full.html 원본 찾기 → `dir /s /b C:\Users\USER\AppData\Local\npm-cache\_npx\*\node_modules\figma-console-mcp\figma-desktop-bridge\ui-full.html`
- 2단계: 플러그인 폴더의 ui.html 백업 → `copy C:\Users\USER\.figma-console-mcp\plugin\ui.html ui.html.bak`
- 3단계: ui-full.html 내용을 ui.html로 복사 → `copy [npm캐시경로]\ui-full.html C:\Users\USER\.figma-console-mcp\plugin\ui.html`
- 4단계: Figma에서 플러그인 재실행 → 녹색불 확인
- 주의: figma-console-mcp 패키지 업데이트 시 npm 캐시 hash 변경될 수 있음. ui-full.html 별도 백업 권장

## 【문제 2】 WebSocket 포트 점유 (9223~9232 모두 사용 중)

- **증상:** 서버 시작 실패, 포트 9223~9232 모두 점유됨
- **원인:** Claude Desktop + Claude Code(VSCode) 각각 figma-console-mcp 인스턴스 실행. Claude Desktop이 트레이 아이콘 없이 백그라운드 실행되어 인지 못함
- **해결법:** 작업관리자(Ctrl+Shift+Esc)에서 claude.exe 백그라운드 프로세스 종료 후 재시작

**Claude 해결 절차:**
- 진단: `netstat -ano | findstr "9223 9224 9225 9226"` 으로 포트 점유 확인
- 정리: `tasklist | findstr "claude node"` 으로 좀비 프로세스 확인 후 `taskkill /f /pid [PID]`

## 【문제 3】 IPv6 바인딩 문제

- **증상:** 서버가 [::1] (IPv6)에 바인딩되어 플러그인에서 연결 실패
- **해결법:** MCP 설정에 환경변수 추가 → `"env": { "FIGMA_WS_HOST": "127.0.0.1" }`

## 【문제 4】 manifest.json allowedDomains 오류

- **증상:** Invalid value for allowedDomains. 'http://127.0.0.1' must be a valid URL
- **원인:** Figma 플러그인 manifest에 포트 없는 IP URL 추가 시 거부됨
- **해결법:** manifest.json은 원본 유지. 127.0.0.1 직접 추가하지 말 것

## 【참고】 Docker Desktop과는 무관

- Docker Desktop(Hyper-V) 설치 후 증상 발생하여 Docker가 원인으로 의심되었으나, Docker 컨테이너 실행 중에도 정상 동작 확인됨
- Docker가 hosts 파일에서 127.0.0.1 localhost를 주석 처리하는 것은 발견됨 → 주석 해제 권장 (네트워킹 일반)
