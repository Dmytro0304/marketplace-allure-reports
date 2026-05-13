# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui/sign-up-web-cases.spec.ts >> @ui Sign Up — Web Cases doc >> Scenario 8 — surrounding spaces trimmed on blur (register)
- Location: e2e/tests/ui/sign-up-web-cases.spec.ts:152:9

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: "e2e-signup-flow@soilconnect.invalid"
Received: "   e2e-signup-flow@soilconnect.invalid   "
```

# Page snapshot

```yaml
- generic [active] [ref=e1]:
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
                - textbox "Email Address" [ref=e79]:
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
  152 |     test('Scenario 8 — surrounding spaces trimmed on blur (register)', async ({ page }) => {
  153 |         const reg = new RegisterPage(page);
  154 |         await reg.goto();
  155 |         await reg.emailInput.fill(`   ${STEP1_THROWAWAY_EMAIL}   `);
  156 |         await reg.emailInput.blur();
  157 |         const v = await reg.emailInput.inputValue();
> 158 |         expect(v).toBe(STEP1_THROWAWAY_EMAIL);
      |                   ^ Error: expect(received).toBe(expected) // Object.is equality
  159 |     });
  160 | 
  161 |     test('Scenario 9 — email case sensitivity: duplicate of existing user', async ({ page }) => {
  162 |         const cred = getTestUser();
  163 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD');
  164 | 
  165 |         const reg = new RegisterPage(page);
  166 |         await reg.goto();
  167 | 
  168 |         await reg.emailInput.fill(cred!.email.toUpperCase());
  169 |         await reg.emailInput.blur();
  170 | 
  171 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toBeVisible({ timeout: 20_000 });
  172 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toContainText(/email|already|exist|taken|registered/i);
  173 |     });
  174 | 
  175 |     test('Scenario 10 — multiple rapid Sign Up clicks send one register request', async ({ page }, testInfo) => {
  176 |         const email = `e2e-rapid-w${testInfo.workerIndex}-${Date.now()}@soilconnect.invalid`;
  177 |         let registerPosts = 0;
  178 |         await page.route('**/api/auth/register', async (route) => {
  179 |             if (route.request().method() === 'POST') {
  180 |                 registerPosts += 1;
  181 |             }
  182 |             await new Promise((r) => setTimeout(r, 3500));
  183 |             await route.continue();
  184 |         });
  185 | 
  186 |         const reg = new RegisterPage(page);
  187 |         await reg.goto();
  188 |         await reg.fillStep1({
  189 |             email,
  190 |             zip: DEFAULT_ZIP,
  191 |             password: STRONG_PASSWORD,
  192 |             confirm: STRONG_PASSWORD,
  193 |         });
  194 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  195 |         await reg.continueButton.click();
  196 |         await expect(reg.signUpButton).toBeVisible({ timeout: 15_000 });
  197 |         const registerResponse = page.waitForResponse(
  198 |             (res) => res.url().includes('auth/register') && res.request().method() === 'POST',
  199 |             { timeout: 120_000 }
  200 |         );
  201 |         await reg.signUpButton.click({ clickCount: 5, delay: 40 });
  202 | 
  203 |         expect(registerPosts).toBe(1);
  204 |         await expect(reg.signUpButton).toBeDisabled({ timeout: 2000 });
  205 |         await registerResponse;
  206 |     });
  207 | 
  208 |     test('Scenario 11 — validation clears after correction', async ({ page }) => {
  209 |         const reg = new RegisterPage(page);
  210 |         await reg.goto();
  211 | 
  212 |         await reg.emailInput.fill('bad');
  213 |         await reg.emailInput.blur();
  214 |         await expect(reg.page.getByText(/invalid email format/i)).toBeVisible({ timeout: 10_000 });
  215 | 
  216 |         await reg.emailInput.fill(STEP1_THROWAWAY_EMAIL);
  217 |         await reg.emailInput.blur();
  218 |         await expect(reg.page.getByText(/invalid email format/i)).toHaveCount(0);
  219 | 
  220 |         await reg.fillStep1({
  221 |             email: STEP1_THROWAWAY_EMAIL,
  222 |             zip: DEFAULT_ZIP,
  223 |             password: STRONG_PASSWORD,
  224 |             confirm: STRONG_PASSWORD,
  225 |         });
  226 | 
  227 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  228 |     });
  229 | 
  230 |     test('Scenario 12 — email max length capped in UI', async ({ page }) => {
  231 |         const reg = new RegisterPage(page);
  232 |         await reg.goto();
  233 | 
  234 |         await expect(reg.emailInput).toHaveAttribute('maxlength', '254');
  235 | 
  236 |         const longLocal = `${'a'.repeat(300)}@x.com`;
  237 |         await reg.emailInput.fill(longLocal);
  238 |         const v = await reg.emailInput.inputValue();
  239 |         expect(v.length).toBeLessThanOrEqual(254);
  240 |     });
  241 | 
  242 |     test('Scenario 13 — slow register response: UI waits then leaves Sign Up', async ({ page }, testInfo) => {
  243 |         const email = `e2e-slowreg-w${testInfo.workerIndex}-${Date.now()}@soilconnect.invalid`;
  244 |         await page.route('**/api/auth/register', async (route) => {
  245 |             await new Promise((r) => setTimeout(r, 2800));
  246 |             await route.continue();
  247 |         });
  248 | 
  249 |         const reg = new RegisterPage(page);
  250 |         await reg.goto();
  251 |         await reg.fillStep1({
  252 |             email,
  253 |             zip: DEFAULT_ZIP,
  254 |             password: STRONG_PASSWORD,
  255 |             confirm: STRONG_PASSWORD,
  256 |         });
  257 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  258 |         await reg.continueButton.click();
```