# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui/sign-up-web-cases.spec.ts >> @ui Sign Up — Web Cases doc >> Scenario 12 — email max length capped in UI
- Location: e2e/tests/ui/sign-up-web-cases.spec.ts:196:9

# Error details

```
Error: expect(received).toBeLessThanOrEqual(expected)

Expected: <= 254
Received:    306
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
                  - text: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa@x.com
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
  152 |     test('Scenario 8 — email trimming (deferred)', async () => {
  153 |         test.skip(true, 'Зависит от договорённостей по trim на бэкенде / validate-email');
  154 |     });
  155 | 
  156 |     test('Scenario 9 — email case sensitivity: duplicate of existing user', async ({ page }) => {
  157 |         const cred = getTestUser();
  158 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD');
  159 | 
  160 |         const reg = new RegisterPage(page);
  161 |         await reg.goto();
  162 | 
  163 |         await reg.emailInput.fill(cred!.email.toUpperCase());
  164 |         await reg.emailInput.blur();
  165 | 
  166 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toBeVisible({ timeout: 20_000 });
  167 |         await expect(page.locator('.step-1 .el-form-item__error').first()).toContainText(/email|already|exist|taken|registered/i);
  168 |     });
  169 | 
  170 |     test('Scenario 10 — multiple rapid Sign Up clicks (deferred)', async () => {
  171 |         test.skip(true, 'Нужна стратегия без дублирования пользователей на dev (idempotency / уникальный email)');
  172 |     });
  173 | 
  174 |     test('Scenario 11 — validation clears after correction', async ({ page }) => {
  175 |         const reg = new RegisterPage(page);
  176 |         await reg.goto();
  177 | 
  178 |         await reg.emailInput.fill('bad');
  179 |         await reg.emailInput.blur();
  180 |         await expect(reg.page.getByText(/invalid email format/i)).toBeVisible({ timeout: 10_000 });
  181 | 
  182 |         await reg.emailInput.fill(STEP1_THROWAWAY_EMAIL);
  183 |         await reg.emailInput.blur();
  184 |         await expect(reg.page.getByText(/invalid email format/i)).toHaveCount(0);
  185 | 
  186 |         await reg.fillStep1({
  187 |             email: STEP1_THROWAWAY_EMAIL,
  188 |             zip: DEFAULT_ZIP,
  189 |             password: STRONG_PASSWORD,
  190 |             confirm: STRONG_PASSWORD,
  191 |         });
  192 | 
  193 |         await expect(reg.continueButton).toBeEnabled({ timeout: 20_000 });
  194 |     });
  195 | 
  196 |     test('Scenario 12 — email max length capped in UI', async ({ page }) => {
  197 |         const reg = new RegisterPage(page);
  198 |         await reg.goto();
  199 | 
  200 |         const longLocal = `${'a'.repeat(300)}@x.com`;
  201 |         await reg.emailInput.fill(longLocal);
  202 |         const v = await reg.emailInput.inputValue();
> 203 |         expect(v.length).toBeLessThanOrEqual(254);
      |                          ^ Error: expect(received).toBeLessThanOrEqual(expected)
  204 |     });
  205 | 
  206 |     test('Scenario 13 — slow network / loading state (deferred)', async () => {
  207 |         test.skip(true, 'Опционально: route.fulfill / throttle + проверка disabled на время запроса');
  208 |     });
  209 | 
  210 |     test('Scenario 14 — ZIP code validation', async ({ page }) => {
  211 |         const reg = new RegisterPage(page);
  212 |         await reg.goto();
  213 | 
  214 |         await reg.emailInput.fill(STEP1_THROWAWAY_EMAIL);
  215 |         await reg.emailInput.blur();
  216 |         await reg.passwordInput.fill(STRONG_PASSWORD);
  217 |         await reg.passwordConfirmInput.fill(STRONG_PASSWORD);
  218 |         await reg.zipInput.fill('');
  219 |         await reg.zipInput.blur();
  220 | 
  221 |         await expect(reg.continueButton).toBeDisabled();
  222 | 
  223 |         await reg.zipInput.fill('123');
  224 |         await reg.zipInput.blur();
  225 |         await expect(reg.page.getByText(/invalid zip code/i)).toBeVisible({ timeout: 20_000 });
  226 |     });
  227 | 
  228 |     test('Scenario 15 — password visibility toggle on Sign Up', async ({ page }) => {
  229 |         const reg = new RegisterPage(page);
  230 |         await reg.goto();
  231 | 
  232 |         await reg.passwordInput.fill('Toggle1a!');
  233 |         await expect(reg.passwordInput).toHaveAttribute('type', 'password');
  234 | 
  235 |         await reg.passwordVisibilityToggle.click();
  236 |         await expect(reg.passwordInput).toHaveAttribute('type', 'text');
  237 |         await reg.passwordVisibilityToggle.click();
  238 |         await expect(reg.passwordInput).toHaveAttribute('type', 'password');
  239 | 
  240 |         await reg.passwordConfirmInput.fill('Toggle1a!');
  241 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'password');
  242 |         await reg.confirmPasswordVisibilityToggle.click();
  243 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'text');
  244 |         await reg.confirmPasswordVisibilityToggle.click();
  245 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'password');
  246 |     });
  247 | });
  248 | 
```