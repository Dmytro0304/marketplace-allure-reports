# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui/sign-up-web-cases.spec.ts >> @ui Sign Up — Web Cases doc >> Scenario 12 — email max length capped in UI
- Location: e2e/tests/ui/sign-up-web-cases.spec.ts:230:9

# Error details

```
Error: expect(locator).toHaveAttribute(expected) failed

Locator:  locator('#email')
Expected: "254"
Received: ""
Timeout:  15000ms

Call log:
  - Expect "toHaveAttribute" with timeout 15000ms
  - waiting for locator('#email')
    30 × locator resolved to <input id="email" type="text" name="email" autocomplete="off" class="el-input__inner" placeholder="Enter your email address"/>
       - unexpected value "null"

```

```yaml
- textbox "Email Address":
  - /placeholder: Enter your email address
```

# Test source

```ts
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
  158 |         expect(v).toBe(STEP1_THROWAWAY_EMAIL);
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
> 234 |         await expect(reg.emailInput).toHaveAttribute('maxlength', '254');
      |                                      ^ Error: expect(locator).toHaveAttribute(expected) failed
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
  259 |         await expect(reg.signUpButton).toBeVisible({ timeout: 15_000 });
  260 | 
  261 |         const started = Date.now();
  262 |         await reg.signUpButton.click();
  263 |         await expect(page).not.toHaveURL(/\/register/, { timeout: 120_000 });
  264 |         expect(Date.now() - started).toBeGreaterThan(2000);
  265 |     });
  266 | 
  267 |     test('Scenario 14 — ZIP code validation', async ({ page }) => {
  268 |         const reg = new RegisterPage(page);
  269 |         await reg.goto();
  270 | 
  271 |         await reg.emailInput.fill(STEP1_THROWAWAY_EMAIL);
  272 |         await reg.emailInput.blur();
  273 |         await reg.passwordInput.fill(STRONG_PASSWORD);
  274 |         await reg.passwordConfirmInput.fill(STRONG_PASSWORD);
  275 |         await reg.zipInput.fill('');
  276 |         await reg.zipInput.blur();
  277 | 
  278 |         await expect(reg.continueButton).toBeDisabled();
  279 | 
  280 |         await reg.zipInput.fill('123');
  281 |         await reg.zipInput.blur();
  282 |         await expect(reg.page.getByText(/invalid zip code/i)).toBeVisible({ timeout: 20_000 });
  283 |     });
  284 | 
  285 |     test('Scenario 15 — password visibility toggle on Sign Up', async ({ page }) => {
  286 |         const reg = new RegisterPage(page);
  287 |         await reg.goto();
  288 | 
  289 |         await reg.passwordInput.fill('Toggle1a!');
  290 |         await expect(reg.passwordInput).toHaveAttribute('type', 'password');
  291 | 
  292 |         await reg.passwordVisibilityToggle.click();
  293 |         await expect(reg.passwordInput).toHaveAttribute('type', 'text');
  294 |         await reg.passwordVisibilityToggle.click();
  295 |         await expect(reg.passwordInput).toHaveAttribute('type', 'password');
  296 | 
  297 |         await reg.passwordConfirmInput.fill('Toggle1a!');
  298 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'password');
  299 |         await reg.confirmPasswordVisibilityToggle.click();
  300 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'text');
  301 |         await reg.confirmPasswordVisibilityToggle.click();
  302 |         await expect(reg.passwordConfirmInput).toHaveAttribute('type', 'password');
  303 |     });
  304 | });
  305 | 
```