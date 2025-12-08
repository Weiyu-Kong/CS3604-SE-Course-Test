## WebTestPilot CLI Setup

### Steps
0. Open your this in VSCode or Trae.
1. Run `cp .env.example .env`. Make sure .env file in project folder have keys for OPENAI_QQ_API_KEY= and BAML_LOG=warn.
2. Install CLI tool and try it.

```bash
# Start the browser
powershell -ExecutionPolicy Bypass -File browser.ps1
source browser.sh

# (Optional) if have not installed Playwright before
npx install playwright

# Install the tool using uv tool
uv tool install ieee-gui

# Check if it works (might have to restart shell)
gui-test --help
```

### Test on real-website
**NOTE:** Before running tests on real site, please login first (on the just-started browser).

```bash
gui-test /ctrip/manage-addresses --env production
gui-test 2.1.1 --env production
```

### Test on your own sites
To test on local: First, check the values in environment `.webtestpilot/.environment/local.json`, make sure it points to the right localhost in your machine i.e. http://localhost:5173. Then run the CLI.

```bash
gui-test /ctrip/manage-addresses --env local
```

### Upgrades
In case of upgrades:
```bash
uv tool upgrade ieee-gui
```


### Tips
**Important:** Login first if testing on real site for login-needed features.

DONTs:
- Don't resize the browser.
- Try to not interfere with the agent browser session.

How to write easy to work actions and expectations? Be specific.
- Good actions: be specific, if the agent still struggles, describe the element more (where it is, distinct features, ...).
  - ✅ DOs: Click "City" dropdown, then choose "Shanghai" from dropdown list.
  - ❌ DONTs: Fill out the form for me.
- Good expectations: be specific and check for feature you are implementing, which element to look for, which message to look for, ... Avoid ambiguous expectations. Also it can be left empty.
  - ✅ DOs: A flight page with search form, list of flights and ... shows up.
  - ❌ DONTs: Correct flight page shows up.
- Try to use the same language used on the tested website. -> Leads to better screen understanding.
