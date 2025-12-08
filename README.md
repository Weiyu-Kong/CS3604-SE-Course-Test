## WebTestPilot CLI Setup

### Step 0: Open this project in VSCode or Trae.

### Step 1: Install dependencies

**Install uv**
Install uv using the following scripts (if have not installed already):
```bash
# For MacOS
curl -LsSf https://astral.sh/uv/install.sh | sh

# For Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# Test the command
uv
```

**Install playwright**
```
npx install playwright
```

### Step 2: Install WebTestPilot CLI
Install CLI tool
```bash
# Install the tool using uv tool
uv tool install ieee-gui

# Check if it works (might have to restart shell)
gui-test --help

# If you have installed before, then upgrade
uv tool upgrade ieee-gui
```

### Step 3: Start the browser (before running tests)
```bash
# Start the browser (for Windows)
powershell -ExecutionPolicy Bypass -File browser.ps1

# Start the browser (for MacOS / Linux)
source browser.sh
```

**NOTE:** If you are running into errors saying ECONNREFUSED to http://localhost:9222. Run the script above to start a new browser again.

### Step 4: Running webtestpilot on real website

**Setup .env variables:**
```bash
cp .env.example .env

# ... and then open .env file and fill in API key given to OPENAI_QQ_API_KEY
```

**Start running tests**

**⚠️ IMPORTANT:** Before running tests on real site, please login first (on the just-started browser in Step 3).

**⚠️ IMPORTANT:** Please use SJTU network while running. It only works inside SJTU network or using VPN.

```bash
# Run a single test by id
gui-test 1 --env production
gui-test 2 --env production
gui-test 3 --env production

# Run a folder of tests (sequentially)
gui-test /ctrip/manage-orders --env production
```

If you run into 401 Unauthorized error, please try running with this configuration:
```bash
gui-test 1 --env production --openai_api_key="..."
```

### Step 5: Start writing new test cases
**Test Structure:** Please make sure:
- "id" and "name" should have format as "{test_number} - {test_name}". For example: "58 - 修改个人信息（姓名）".
- Put value in "id" and "name" same.

```
{
  "id": "57 - 修改个人信息（邮箱与昵称）",
  "name": "57 - 修改个人信息（邮箱与昵称）",
  ...
}
```

**✍️ How to write actions and expectations?** - Be specific.
- **Good actions:** be specific, if the agent still struggles, describe the element more (where it is, distinct features, ...).
  - ✅ DOs: Click "City" dropdown, then choose "Shanghai" from dropdown list.
  - ❌ DONTs: Fill out the form for me.
- **Good expectations:** be specific and check for feature you are implementing, which element to look for, which message to look for, ... Avoid ambiguous expectations. Also it can be left empty.
  - ✅ DOs: A flight page with search form, list of flights and ... shows up.
  - ❌ DONTs: Correct flight page shows up.
- **Language:** Try to use the **same language** used on the tested website.

**❌ AVOID:**
- Don't resize the browser agent is using.
- Try to not interfere with the agent browser session.

**⚠️ Important:** Login first if testing on real site for login-needed features.

### Upgrades
In case of tool upgrades / bug fixes:
```bash
uv tool upgrade ieee-gui
```

