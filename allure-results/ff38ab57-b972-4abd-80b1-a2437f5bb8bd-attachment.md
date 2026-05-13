# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui/sign-in-web-cases.spec.ts >> @ui Sign In — Web Cases doc >> Scenario 10 — error clears after correction, then login succeeds
- Location: e2e/tests/ui/sign-in-web-cases.spec.ts:126:9

# Error details

```
Error: expect(locator).toBeHidden() failed

Locator:  locator('.el-form-item__error').first()
Expected: hidden
Received: visible
Timeout:  10000ms

Call log:
  - Expect "toBeHidden" with timeout 10000ms
  - waiting for locator('.el-form-item__error').first()
    21 × locator resolved to <div class="el-form-item__error">↵                        Incorrect email and / or…</div>
       - unexpected value "visible"

```

```yaml
- text: Incorrect email and / or password.
```

# Test source

```ts
  39  | 
  40  |         await expect(page).toHaveURL(/\/login/, { timeout: 15_000 });
  41  |         const err = page.locator('.el-form-item__error').first();
  42  |         await expect(err).toBeVisible({ timeout: 15_000 });
  43  |         await expect(err).toContainText(/incorrect|invalid|password|email/i);
  44  |     });
  45  | 
  46  |     test('Scenario 3 — Log in with empty form (Sign In disabled)', async ({ page }) => {
  47  |         const login = new LoginPage(page);
  48  |         await login.goto();
  49  |         await login.expectOnLoginPage();
  50  | 
  51  |         await login.emailInput.fill('');
  52  |         await login.passwordInput.fill('');
  53  | 
  54  |         await expect(login.signInButton).toBeDisabled();
  55  |         await expect(page).toHaveURL(/\/login/);
  56  |     });
  57  | 
  58  |     test('Scenario 4 — invalid email format: validation error and Sign In disabled', async ({ page }) => {
  59  |         const login = new LoginPage(page);
  60  |         await login.goto();
  61  | 
  62  |         await login.emailInput.fill('notanemail');
  63  |         await login.passwordInput.fill('AnyPassword1!');
  64  |         await login.emailInput.blur();
  65  | 
  66  |         await expect(login.signInButton).toBeDisabled();
  67  |         await expect(page.getByText(/email is not valid/i)).toBeVisible({ timeout: 10_000 });
  68  |         await expect(page).toHaveURL(/\/login/);
  69  |     });
  70  | 
  71  |     test('Scenario 5 — incorrect password (valid email)', async ({ page }) => {
  72  |         const cred = getTestUser();
  73  |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  74  | 
  75  |         const login = new LoginPage(page);
  76  |         await login.goto();
  77  |         await login.fillCredentials(cred!.email, `${cred!.password}_wrong`);
  78  |         await login.submit();
  79  | 
  80  |         await expect(page).toHaveURL(/\/login/);
  81  |         const err = page.locator('.el-form-item__error').first();
  82  |         await expect(err).toBeVisible({ timeout: 15_000 });
  83  |         await expect(err).toContainText(/incorrect|password|email/i);
  84  |     });
  85  | 
  86  |     test('Scenario 6 — password field is masked by default', async ({ page }) => {
  87  |         const login = new LoginPage(page);
  88  |         await login.goto();
  89  |         await login.passwordInput.fill('SecretValue1');
  90  | 
  91  |         await expect(login.passwordInput).toHaveAttribute('type', 'password');
  92  |     });
  93  | 
  94  |     test('Scenario 7 — email trimming (deferred)', async () => {
  95  |         test.skip(
  96  |             true,
  97  |             'Doc expects success with padded email; LoginRequest only lowercases (no trim). Enable after trim on server.'
  98  |         );
  99  |     });
  100 | 
  101 |     test('Scenario 8 — email case insensitivity', async ({ page }) => {
  102 |         const cred = getTestUser();
  103 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  104 | 
  105 |         const login = new LoginPage(page);
  106 |         await login.goto();
  107 |         const upperEmail = cred!.email.toUpperCase();
  108 |         await login.fillCredentials(upperEmail, cred!.password);
  109 |         await login.submit();
  110 | 
  111 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  112 |     });
  113 | 
  114 |     test('Scenario 9 — multiple rapid Sign In clicks still yield single successful login', async ({ page }) => {
  115 |         const cred = getTestUser();
  116 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  117 | 
  118 |         const login = new LoginPage(page);
  119 |         await login.goto();
  120 |         await login.fillCredentials(cred!.email, cred!.password);
  121 |         await login.signInButton.click({ clickCount: 3, delay: 40 });
  122 | 
  123 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  124 |     });
  125 | 
  126 |     test('Scenario 10 — error clears after correction, then login succeeds', async ({ page }) => {
  127 |         const cred = getTestUser();
  128 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  129 | 
  130 |         const login = new LoginPage(page);
  131 |         await login.goto();
  132 |         await login.fillCredentials(cred!.email, `${cred!.password}_bad`);
  133 |         await login.submit();
  134 | 
  135 |         const err = page.locator('.el-form-item__error').first();
  136 |         await expect(err).toBeVisible({ timeout: 15_000 });
  137 | 
  138 |         await login.fillCredentials(cred!.email, cred!.password);
> 139 |         await expect(err).toBeHidden({ timeout: 10_000 });
      |                           ^ Error: expect(locator).toBeHidden() failed
  140 |         await login.submit();
  141 | 
  142 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  143 |     });
  144 | 
  145 |     test('Scenario 11 — leading/trailing spaces in password: login fails', async ({ page }) => {
  146 |         const cred = getTestUser();
  147 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  148 | 
  149 |         const login = new LoginPage(page);
  150 |         await login.goto();
  151 |         await login.emailInput.fill(cred!.email);
  152 |         await login.passwordInput.fill(` ${cred!.password} `);
  153 |         await login.submit();
  154 | 
  155 |         await expect(page).toHaveURL(/\/login/);
  156 |         const err = page.locator('.el-form-item__error').first();
  157 |         await expect(err).toBeVisible({ timeout: 15_000 });
  158 |     });
  159 | 
  160 |     test('Scenario 12 — slow network / loader (deferred)', async () => {
  161 |         test.skip(true, 'Run manually with throttling (Web Cases doc Scenario 12).');
  162 |     });
  163 | 
  164 |     test('Scenario 13 — password visibility toggle (eye icon)', async ({ page }) => {
  165 |         const login = new LoginPage(page);
  166 |         await login.goto();
  167 |         await login.passwordInput.fill('ToggleMe123');
  168 | 
  169 |         await expect(login.passwordInput).toHaveAttribute('type', 'password');
  170 |         await login.togglePasswordVisibility();
  171 |         await expect(login.passwordInput).toHaveAttribute('type', 'text');
  172 |         await login.togglePasswordVisibility();
  173 |         await expect(login.passwordInput).toHaveAttribute('type', 'password');
  174 |     });
  175 | });
  176 | 
```