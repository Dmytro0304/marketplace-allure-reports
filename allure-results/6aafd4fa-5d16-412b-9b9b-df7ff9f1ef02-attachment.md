# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui/sign-up-web-cases.spec.ts >> @ui Sign Up — Web Cases doc >> Scenario 8 — surrounding spaces stripped from email (input filter)
- Location: e2e/tests/ui/sign-up-web-cases.spec.ts:152:9

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: "e2e-signup-flow@soilconnect.invalid"
Received: "   e2e-signup-flow@soilconnect.invalid   "
```

# Page snapshot

```yaml
- generic [ref=e1]:
  - generic [ref=e2]:
    - banner [ref=e3]:
      - paragraph [ref=e6]:
        - text: Try
        - link "eTickets" [ref=e7] [cursor=pointer]:
          - /url: https://tickets.soilconnect.com
        - text: ", an easy way to capture, track and share the details of hauling materials from one destination to the next."
        - img [ref=e8] [cursor=pointer]
      - generic [ref=e10]:
        - link [ref=e12] [cursor=pointer]:
          - /url: /
          - img [ref=e14]
        - generic [ref=e20]:
          - generic [ref=e22] [cursor=pointer]: Create Post
          - generic [ref=e24] [cursor=pointer]: Quotes Hub
          - generic [ref=e26] [cursor=pointer]: My Posts
          - generic [ref=e28] [cursor=pointer]: Matches
          - link "Search" [ref=e29] [cursor=pointer]:
            - /url: /dashboard/posts/search
            - generic [ref=e31]: Search
          - button "Services" [ref=e33] [cursor=pointer]:
            - generic [ref=e35]: Services
            - img [ref=e36]
        - generic [ref=e38]:
          - link "Header Mobile Icon 1.833.230.SOIL" [ref=e39] [cursor=pointer]:
            - /url: tel:1.833.230.SOIL
            - generic [ref=e40]:
              - img "Header Mobile Icon" [ref=e41]
              - text: 1.833.230.SOIL
          - link "Login/Sign up" [ref=e42] [cursor=pointer]:
            - /url: /login
      - generic: 
    - main [ref=e43]:
      - generic [ref=e45]:
        - generic [ref=e48]:
          - heading "Meet the easiest way to buy or sell dirt & aggregates." [level=1] [ref=e49]
          - paragraph [ref=e50]: "Marketplace Benefits:"
          - list [ref=e51]:
            - listitem [ref=e52]:
              - img [ref=e53]
              - generic [ref=e56]: Find material buyers and suppliers by location
            - listitem [ref=e57]:
              - img [ref=e58]
              - generic [ref=e61]: Post your material needs to receive quality matches
            - listitem [ref=e62]:
              - img [ref=e63]
              - generic [ref=e66]: Quickly connect with buyers and suppliers
        - generic [ref=e71]:
          - heading "Sign Up" [level=2] [ref=e72]
          - generic [ref=e73]:
            - generic [ref=e74]:
              - generic [ref=e75]:
                - generic [ref=e76]: Email Address
                - textbox "Email Address" [active] [ref=e79]:
                  - /placeholder: Enter your email address
                  - text: e2e-signup-flow@soilconnect.invalid
              - generic [ref=e80]:
                - generic [ref=e81]: Zip Code
                - textbox "Zip Code" [ref=e84]:
                  - /placeholder: Enter your zip code
              - generic [ref=e85]:
                - generic [ref=e86]: Password
                - generic [ref=e87]:
                  - textbox "Create your password" [ref=e89]
                  - img [ref=e90] [cursor=pointer]
              - generic [ref=e95]:
                - generic [ref=e96]: Confirm Password
                - generic [ref=e97]:
                  - textbox "Confirm your password" [ref=e99]
                  - img [ref=e100] [cursor=pointer]
              - generic [ref=e106]:
                - button "Continue" [disabled] [ref=e107]:
                  - generic [ref=e108]:
                    - text: Continue
                    - img [ref=e109] [cursor=pointer]
                - paragraph [ref=e111]:
                  - text: By creating an account, you agree to the
                  - generic [ref=e113] [cursor=pointer]: Terms of Use
                  - text: and you acknowledge that you have read the
                  - generic [ref=e115] [cursor=pointer]: Privacy Policy
            - text: 
    - generic: 
    - generic: 
    - generic: 
    - generic [ref=e121]:
      - generic [ref=e122]: © 2022 - 2026 Soil Connect, Inc.
      - list [ref=e124]:
        - listitem [ref=e125]:
          - generic [ref=e127] [cursor=pointer]: Terms & Conditions
        - listitem [ref=e128]:
          - generic [ref=e130] [cursor=pointer]: Privacy Policy
  - paragraph [ref=e132]:
    - emphasis [ref=e133]: n/a
  - status
```

# Test source

```ts
  57  |         await reg.emailInput.fill('');
  58  |         await reg.zipInput.fill('');
  59  |         await reg.passwordInput.fill('');
  60  |         await reg.passwordConfirmInput.fill('');
  61  | 
  62  |         await expect(reg.continueButton).toBeDisabled();
  63  |         await expect(page).toHaveURL(/\/register/);
  64  |     });
  65  | 
  66  |     test('Scenario 3 — invalid email format', async ({ page }) => {
  67  |         const reg = new RegisterPage(page);
  68  |         await reg.goto();
  69  | 
  70  |         await reg.passwordInput.fill(STRONG_PASSWORD);
  71  |         await reg.passwordConfirmInput.fill(STRONG_PASSWORD);
  72  |         await reg.zipInput.fill(DEFAULT_ZIP);
  73  |         await reg.zipInput.blur();
  74  | 
  75  |         await reg.emailInput.fill('notanemail');
  76  |         await reg.emailInput.blur();
  77  |         await expect(reg.page.getByText(/invalid email format/i)).toBeVisible({ timeout: 15_000 });
  78  |         await expect(reg.continueButton).toBeDisabled();
  79  | 
  80  |         await reg.emailInput.fill('test@');
  81  |         await reg.emailInput.blur();
  82  |         await expect(reg.page.getByText(/invalid email format/i)).toBeVisible();
  83  | 
  84  |         await reg.emailInput.fill('');
  85  |         await reg.emailInput.blur();
  86  |         await expect(reg.continueButton).toBeDisabled();
  87  |     });
  88  | 
  89  |     test('Scenario 4 — weak password: Continue disabled', async ({ page }) => {
  90  |         const reg = new RegisterPage(page);
  91  |         await reg.goto();
  92  | 
  93  |         await reg.emailInput.fill(STEP1_THROWAWAY_EMAIL);
  94  |         await reg.emailInput.blur();
  95  |         await reg.zipInput.fill(DEFAULT_ZIP);
  96  |         await reg.zipInput.blur();
  97  | 
  98  |         await reg.passwordInput.fill('abc');
  99  |         await reg.passwordConfirmInput.fill('abc');
  100 | 
  101 |         await expect(reg.continueButton).toBeDisabled();
  102 |         await expect(reg.page.getByText(/the password must contain/i)).toBeVisible();
  103 |         await expect(page).toHaveURL(/\/register/);
  104 |     });
  105 | 
  106 |     test('Scenario 5 — mismatched passwords', async ({ page }) => {
  107 |         const reg = new RegisterPage(page);
  108 |         await reg.goto();
  109 | 
  110 |         await reg.fillStep1({
  111 |             email: STEP1_THROWAWAY_EMAIL,
  112 |             zip: DEFAULT_ZIP,
  113 |             password: STRONG_PASSWORD,
  114 |             confirm: 'Otherpass1!',
  115 |         });
  116 | 
  117 |         await expect(page.getByText(/confirmation password do not match/i)).toBeVisible({ timeout: 15_000 });
  118 | 
  119 |         await reg.continueButton.click();
  120 |         await expect(reg.signUpButton).toBeVisible({ timeout: 10_000 });
  121 |         await reg.signUpButton.click();
  122 | 
  123 |         await expect(page).toHaveURL(/\/register/, { timeout: 30_000 });
  124 |         await expect(page.getByText(/do not match|does not match/i)).toBeVisible({ timeout: 20_000 });
  125 |     });
  126 | 
  127 |     test('Scenario 6 — existing email (check after blur)', async ({ page }) => {
  128 |         const cred = getTestUser();
  129 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD (существующий аккаунт на dev)');
  130 | 
  131 |         const reg = new RegisterPage(page);
  132 |         await reg.goto();
  133 | 
  134 |         await reg.emailInput.fill(cred!.email);
  135 |         await reg.emailInput.blur();
  136 | 
  137 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toBeVisible({ timeout: 20_000 });
  138 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toContainText(/email|already|exist|taken|registered/i);
  139 |     });
  140 | 
  141 |     test('Scenario 7 — password fields masked by default', async ({ page }) => {
  142 |         const reg = new RegisterPage(page);
  143 |         await reg.goto();
  144 | 
  145 |         await reg.passwordInput.fill('Secret1a!');
  146 |         await reg.passwordConfirmInput.fill('Secret1a!');
  147 | 
  148 |         await expect(reg.passwordInput).toHaveAttribute('type', 'password');
  149 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'password');
  150 |     });
  151 | 
  152 |     test('Scenario 8 — surrounding spaces stripped from email (input filter)', async ({ page }) => {
  153 |         const reg = new RegisterPage(page);
  154 |         await reg.goto();
  155 |         await reg.emailInput.fill(`   ${STEP1_THROWAWAY_EMAIL}   `);
  156 |         const v = await reg.emailInput.inputValue();
> 157 |         expect(v).toBe(STEP1_THROWAWAY_EMAIL);
      |                   ^ Error: expect(received).toBe(expected) // Object.is equality
  158 |     });
  159 | 
  160 |     test('Scenario 9 — email case sensitivity: duplicate of existing user', async ({ page }) => {
  161 |         const cred = getTestUser();
  162 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD');
  163 | 
  164 |         const reg = new RegisterPage(page);
  165 |         await reg.goto();
  166 | 
  167 |         await reg.emailInput.fill(cred!.email.toUpperCase());
  168 |         await reg.emailInput.blur();
  169 | 
  170 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toBeVisible({ timeout: 20_000 });
  171 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toContainText(/email|already|exist|taken|registered/i);
  172 |     });
  173 | 
  174 |     test('Scenario 10 — multiple rapid Sign Up clicks send one register request', async ({ page }, testInfo) => {
  175 |         const email = `e2e-rapid-w${testInfo.workerIndex}-${Date.now()}@soilconnect.invalid`;
  176 |         let registerPosts = 0;
  177 |         await page.route('**/api/auth/register', async (route) => {
  178 |             if (route.request().method() === 'POST') {
  179 |                 registerPosts += 1;
  180 |             }
  181 |             await new Promise((r) => setTimeout(r, 3500));
  182 |             await route.continue();
  183 |         });
  184 | 
  185 |         const reg = new RegisterPage(page);
  186 |         await reg.goto();
  187 |         await reg.fillStep1({
  188 |             email,
  189 |             zip: DEFAULT_ZIP,
  190 |             password: STRONG_PASSWORD,
  191 |             confirm: STRONG_PASSWORD,
  192 |         });
  193 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  194 |         await reg.continueButton.click();
  195 |         await expect(reg.signUpButton).toBeVisible({ timeout: 15_000 });
  196 |         const registerResponse = page.waitForResponse(
  197 |             (res) => res.url().includes('auth/register') && res.request().method() === 'POST',
  198 |             { timeout: 120_000 }
  199 |         );
  200 |         await reg.signUpButton.click({ clickCount: 5, delay: 40 });
  201 | 
  202 |         expect(registerPosts).toBe(1);
  203 |         await expect(reg.signUpButton).toBeDisabled({ timeout: 2000 });
  204 |         await registerResponse;
  205 |     });
  206 | 
  207 |     test('Scenario 11 — validation clears after correction', async ({ page }) => {
  208 |         const reg = new RegisterPage(page);
  209 |         await reg.goto();
  210 | 
  211 |         await reg.emailInput.fill('bad');
  212 |         await reg.emailInput.blur();
  213 |         await expect(reg.page.getByText(/invalid email format/i)).toBeVisible({ timeout: 10_000 });
  214 | 
  215 |         await reg.emailInput.fill(STEP1_THROWAWAY_EMAIL);
  216 |         await reg.emailInput.blur();
  217 |         await expect(reg.page.getByText(/invalid email format/i)).toHaveCount(0);
  218 | 
  219 |         await reg.fillStep1({
  220 |             email: STEP1_THROWAWAY_EMAIL,
  221 |             zip: DEFAULT_ZIP,
  222 |             password: STRONG_PASSWORD,
  223 |             confirm: STRONG_PASSWORD,
  224 |         });
  225 | 
  226 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  227 |     });
  228 | 
  229 |     test('Scenario 12 — email max length capped in UI', async ({ page }) => {
  230 |         const reg = new RegisterPage(page);
  231 |         await reg.goto();
  232 | 
  233 |         const longLocal = `${'a'.repeat(300)}@x.com`;
  234 |         await reg.emailInput.fill(longLocal);
  235 |         const v = await reg.emailInput.inputValue();
  236 |         expect(v.length).toBeLessThanOrEqual(254);
  237 |     });
  238 | 
  239 |     test('Scenario 13 — slow register response: UI waits then leaves Sign Up', async ({ page }, testInfo) => {
  240 |         const email = `e2e-slowreg-w${testInfo.workerIndex}-${Date.now()}@soilconnect.invalid`;
  241 |         await page.route('**/api/auth/register', async (route) => {
  242 |             await new Promise((r) => setTimeout(r, 2800));
  243 |             await route.continue();
  244 |         });
  245 | 
  246 |         const reg = new RegisterPage(page);
  247 |         await reg.goto();
  248 |         await reg.fillStep1({
  249 |             email,
  250 |             zip: DEFAULT_ZIP,
  251 |             password: STRONG_PASSWORD,
  252 |             confirm: STRONG_PASSWORD,
  253 |         });
  254 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  255 |         await reg.continueButton.click();
  256 |         await expect(reg.signUpButton).toBeVisible({ timeout: 15_000 });
  257 | 
```