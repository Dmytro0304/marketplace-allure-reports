# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui/sign-in-web-cases.spec.ts >> @ui Sign In — Web Cases doc >> Scenario 7 — email with leading/trailing spaces
- Location: e2e/tests/ui/sign-in-web-cases.spec.ts:94:9

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: locator('.el-form-item__error').first()
Expected: visible
Timeout: 15000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" with timeout 15000ms
  - waiting for locator('.el-form-item__error').first()

```

```yaml
- banner:
  - paragraph:
    - text: Try
    - link "eTickets":
      - /url: https://tickets.soilconnect.com
    - text: ", an easy way to capture, track and share the details of hauling materials from one destination to the next."
    - img
  - link:
    - /url: /
    - img
  - text: Create Post Quotes Hub NEW My Posts Matches
  - link "Search":
    - /url: /dashboard/posts/search
  - button "Services":
    - text: Services
    - img
  - link "Header Mobile Icon 1.833.230.SOIL":
    - /url: tel:1.833.230.SOIL
    - img "Header Mobile Icon"
    - text: 1.833.230.SOIL
  - button "User Avatar ":
    - img "User Avatar"
    - text: 
- main:
  - img "SoilConnect Homepage Background"
  - heading "Got Dirt? Need Dirt? Soil Connect Has You Covered!" [level=1]
  - button "I have materials"
  - button "I need materials"
  - img
  - textbox "Select your material type"
  - text: 
  - img
  - img
  - textbox "Enter an address, city or ZIP code"
  - button "Get Matched" [disabled]:
    - img
    - text: Get Matched
  - text: "Materials Near:"
  - img
  - text: New York, NY
  - img
  - button "" [disabled]
  - button ""
  - img "Clay"
  - img "SC-copyright"
  - heading "Clay" [level=3]
  - img
  - text: Available  2 Posts
  - button "CONTACT US"
  - img "Clean / Common Fill"
  - img "SC-copyright"
  - heading "Clean / Common Fill" [level=3]
  - img
  - text: Available  20 Posts
  - button "CONTACT US"
  - img "Loam"
  - img "SC-copyright"
  - heading "Loam" [level=3]
  - img
  - text: Available  4 Posts
  - button "CONTACT US"
  - img "Select / Structural Fill"
  - img "SC-copyright"
  - heading "Select / Structural Fill" [level=3]
  - img
  - text: Available  8 Posts
  - button "CONTACT US"
  - img "TopSoil"
  - img "SC-copyright"
  - heading "TopSoil" [level=3]
  - img
  - text: Available  55 Posts
  - button "CONTACT US"
  - img "Crushed Stone"
  - img "SC-copyright"
  - heading "Crushed Stone" [level=3]
  - img
  - text: Available  5 Posts
  - button "CONTACT US"
  - img "Gravel"
  - img "SC-copyright"
  - heading "Gravel" [level=3]
  - img
  - text: Available  6 Posts
  - button "CONTACT US"
  - img "Limestone"
  - img "SC-copyright"
  - heading "Limestone" [level=3]
  - img
  - text: Available  2 Posts
  - button "CONTACT US"
  - img "Sand"
  - img "SC-copyright"
  - heading "Sand" [level=3]
  - img
  - text: Available  No Posts
  - button "CONTACT US"
  - text: Our Customers & Reviews
  - button "" [disabled]
  - button ""
  - blockquote:
    - img
    - paragraph: Since utilizing the SoilConnect app for haulers, we have streamlined ticketing in a way that far exceeded any expectations we had! The level of customization really gives us the ability to track every item that is critical, specific to our company. There are no lost tickets, no deciphering handwriting, easy to download tickets and easy to download into excel for tracking job specific. More importantly, the commitment the SoilConnect team has made to our company and our needs has been unparalleled. Each member of their team has always made the Esposito team a top priority and worked diligently to ensure we feel valued, and all our needs are met. This software has been priceless to our company's success!
  - img "Esposito Construction"
  - text: Esposito Construction Colts Neck, NJ
  - blockquote:
    - img
    - paragraph: Soil Connect has been and continues to be a great to work with, even after the deal is done. In the construction industry, long periods of time go by without any communication, but that's not how Soil Connect worked. They were intentional with their follow-up, and that CANNOT be undervalued! They were easy to work with, and I hope to have the pleasure of working with them again in the near future!
  - img "Grand Strand Materials"
  - text: Grand Strand Materials Myrtle Beach, SC
  - blockquote:
    - img
    - paragraph: It's been great working with Soil Connect and they really make my life easier with all the different things I have going on. The visibility and data that the Soil Connect application provides on the import progress and budget tracking has been extremely helpful and gives me the confidence that we're getting accurate volumes that we are paying for. Highly recommend Soil Connect for all big import jobs.
  - img "Prologis"
  - text: Prologis East Rutherford, NJ
  - blockquote:
    - img
    - paragraph: Soil connect was instrumental in finding a home for our significant amount of soil export for a project on Long Island that generated cost savings for both us and the Owner. The constant communication and reporting of quantities was also super helpful in tracking our export. Highly recommend reaching out for all projects with unbalanced sites!
  - img "ARCO Design Build"
  - text: ARCO Design Build Murray
  - blockquote:
    - img
    - paragraph: Soil Connect has made sourcing and transporting materials seamless. The platform is user-friendly, and their team is always ready to assist. We've saved time and costs on every project thanks to their innovative tools. Highly recommend Soil Connect!
  - img "North Shore Paving"
  - text: North Shore Paving Kings Park, NY
  - blockquote:
    - img
    - paragraph: If it wasn't for Soil Connect, we wouldn't have known about multiple problems on the site. We also wouldn't have found out that dirt was being pulled from multiple unapproved locations. Those are big value adds on top of the main reasons we got up and running with you all.
  - img "Prologis Texas"
  - text: Prologis Texas Dallas, TX
  - blockquote:
    - img
    - paragraph: In working with Soil Connect, we have been able to help our projects find and get rid of dirt fast and cost efficiently. We have used other platforms for our dirt needs in the past, and Soil Connect has proven to be the best and most reliable.
  - img "Wallace Ventures"
  - text: Wallace Ventures Dallas, TX
  - blockquote:
    - img
    - paragraph: Working with Soil Connect has been a game-changer for us. They've helped us save money and introduced us to reputable trucking companies in Charlotte, streamlining our operations and improving efficiency.
  - img "Sunbelt Utilities Corp"
  - text: Sunbelt Utilities Corp Charlotte, NC
  - blockquote:
    - img
    - paragraph: We turned to Soil Connect to help us get rid of the excess dirt on our site. Within days, we got several matches and were quickly able to understand the going market rate in our area.
  - img "Pittman Partners"
  - text: Pittman Partners Indianapolis, IN
  - blockquote:
    - img
    - paragraph: For anyone in construction or utilities looking to simplify their material sourcing and hauling, we highly recommend Soil Connect. They've become an invaluable partner to JCP Utilities.
  - img "JCP Utilities"
  - text: JCP Utilities Dallas, TX
  - blockquote:
    - img
    - paragraph: I like working with Soil Connect. It puts me in touch with prospective clients and also helps me with the removal of my materials.
  - img "LMC Corp"
  - text: LMC Corp Long Island, NY
  - blockquote:
    - img
    - paragraph: Your brokerage service is great, but I think the most valuable thing you do is this data collection and reporting.
  - img "Prologis"
  - text: Prologis Dallas, TX
  - blockquote:
    - img
    - paragraph: You have permanently changed our Owner / Contractor meetings for the better.
  - img "Peinado Construction"
  - text: Peinado Construction Austin, TX
  - blockquote:
    - img
    - paragraph: The Soil Connect app makes moving or getting fill very easy.
  - img "IGC"
  - text: IGC Westhampton, NY
  - img "Bokman"
  - img "CHDS logo-01"
  - img "Crowne Partners"
  - img "DR Horton"
  - img "DalDirt"
  - img "Earl company"
  - img "Elevated Execavating"
  - img "Fuller"
  - img "GTIS"
  - img "Grid"
  - img "Next Level"
  - img "North shore"
  - img "Pittman"
  - img "Prologis"
  - img "Reality Link"
  - img "Sanitary"
  - img "Scheideck"
  - img "SunBelt"
  - img "UL"
  - img "Wallace"
  - img "Zachary Construction"
  - img "Alliance Industrial Group"
  - img "Arco Murray"
  - img "Ashton Woods"
  - img "Factor Group"
  - img "Hollon"
  - img "Peinado"
  - img "Precast"
  - img "T Disney"
  - img "Bokman"
  - img "CHDS logo-01"
  - img "Crowne Partners"
  - img "DR Horton"
  - img "DalDirt"
  - img "Earl company"
  - img "Elevated Execavating"
  - img "Fuller"
  - img "GTIS"
  - img "Grid"
  - img "Next Level"
  - img "North shore"
  - img "Pittman"
  - img "Prologis"
  - img "Reality Link"
  - img "Sanitary"
  - img "Scheideck"
  - img "SunBelt"
  - img "UL"
  - img "Wallace"
  - img "Zachary Construction"
  - img "Alliance Industrial Group"
  - img "Arco Murray"
  - img "Ashton Woods"
  - img "Factor Group"
  - img "Hollon"
  - img "Peinado"
  - img "Precast"
  - img "T Disney"
  - 'heading "The Nation''s #1 Dirt Marketplace on your phone or tablet." [level=5]'
  - paragraph: Find the materials you need and Move the materials you have with Soil Connect.
  - link "Google Play Qr Code Google Play":
    - /url: https://play.google.com/store/apps/details?id=com.soilconnect
    - img "Google Play Qr Code"
    - img "Google Play"
  - link "App Store Qr Code App Store":
    - /url: https://apps.apple.com/us/app/soil-connect/id1364441763
    - img "App Store Qr Code"
    - img "App Store"
  - text: Connect With Our Community
  - list:
    - listitem:
      - link "Facebook":
        - /url: https://www.facebook.com/SoilConnect/
        - img "Facebook"
    - listitem:
      - link "LinkedIn":
        - /url: https://www.linkedin.com/company/soil-connect/?viewAsMember=true
        - img "LinkedIn"
    - listitem:
      - link "Twitter":
        - /url: https://twitter.com/SoilConnect
        - img "Twitter"
    - listitem:
      - link "Instagram":
        - /url: https://instagram.com/SoilConnect
        - img "Instagram"
    - listitem:
      - link "Youtube":
        - /url: https://www.youtube.com/channel/UCDOnjCMEW9P-WlXaY9a6Abw/featured
        - img "Youtube"
- heading "Products" [level=5]
- list:
  - listitem: Marketplace
  - listitem:
    - link "eTickets":
      - /url: https://etickets.soilconnect.com
- heading "Services" [level=5]
- list:
  - listitem:
    - link "Dirt Expedited":
      - /url: https://www.soilconnect.com/contractors
  - listitem:
    - link "Dirt Reporting":
      - /url: https://www.soilconnect.com/dirt-reports
  - listitem:
    - link "Dirt Hauling":
      - /url: https://www.soilconnect.com/haulers
- heading "Company" [level=5]
- list:
  - listitem:
    - link "About Us":
      - /url: https://www.soilconnect.com/about-us/
  - listitem:
    - link "In the News":
      - /url: https://www.soilconnect.com/in-the-news
  - listitem:
    - link "Leadership Team":
      - /url: "#"
  - listitem:
    - link "Case Studies":
      - /url: https://www.soilconnect.com/case-studies/
- heading "Connect" [level=5]
- list:
  - listitem:
    - link "Contact Us":
      - /url: https://www.soilconnect.com/contact-us
  - listitem:
    - link "Footer Mobile Icon 1.833.230.SOIL":
      - /url: tel:1.833.230.SOIL
      - img "Footer Mobile Icon"
      - text: 1.833.230.SOIL
  - listitem:
    - link "Facebook":
      - /url: https://www.facebook.com/SoilConnect/
      - img "Facebook"
    - link "LinkedIn":
      - /url: https://www.linkedin.com/company/soil-connect/?viewAsMember=true
      - img "LinkedIn"
    - link "Twitter":
      - /url: https://twitter.com/SoilConnect
      - img "Twitter"
    - link "Instagram":
      - /url: https://instagram.com/SoilConnect
      - img "Instagram"
    - link "YouTube":
      - /url: https://www.youtube.com/channel/UCDOnjCMEW9P-WlXaY9a6Abw/featured
      - img "YouTube"
- text: © 2022 - 2026 Soil Connect, Inc.
- list:
  - listitem: Terms & Conditions
  - listitem: Privacy Policy
- paragraph:
  - emphasis: n/a
- status
```

# Test source

```ts
  13  | 
  14  |         const login = new LoginPage(page);
  15  |         await login.goto();
  16  |         await login.expectOnLoginPage();
  17  |         await expect(login.emailInput).toBeVisible();
  18  |         await expect(login.passwordInput).toBeVisible();
  19  | 
  20  |         await login.fillCredentials(cred!.email, cred!.password);
  21  |         await login.submit();
  22  | 
  23  |         try {
  24  |             await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  25  |         } catch {
  26  |             const err = page.locator('.el-form-item__error').first();
  27  |             const msg = (await err.isVisible()) ? (await err.innerText()).trim() : '(no inline error)';
  28  |             throw new Error(
  29  |                 `Expected redirect after login; still on /login. Check TEST_USER_* on dev. Form: ${msg}`
  30  |             );
  31  |         }
  32  |     });
  33  | 
  34  |     test('Scenario 2 — Log in with non-existing user', async ({ page }) => {
  35  |         const login = new LoginPage(page);
  36  |         await login.goto();
  37  |         await login.fillCredentials('e2e-not-registered-user@soilconnect.invalid', 'AnyPassword1!');
  38  |         await login.submit();
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
  94  |     test('Scenario 7 — email with leading/trailing spaces', async ({ page }) => {
  95  |         const cred = getTestUser();
  96  |         test.skip(!cred, 'Set TEST_USER_EMAIL and TEST_USER_PASSWORD in .env');
  97  | 
  98  |         const login = new LoginPage(page);
  99  |         await login.goto();
  100 |         await login.emailInput.fill(`  ${cred!.email}  `);
  101 |         await login.passwordInput.fill(cred!.password);
  102 |         await login.emailInput.blur();
  103 | 
  104 |         if (await login.signInButton.isDisabled()) {
  105 |             await expect(page.getByText(/email is not valid/i)).toBeVisible({ timeout: 10_000 });
  106 |             return;
  107 |         }
  108 | 
  109 |         await login.submit();
  110 | 
  111 |         if (page.url().includes('/login')) {
  112 |             const err = page.locator('.el-form-item__error').first();
> 113 |             await expect(err).toBeVisible({ timeout: 15_000 });
      |                               ^ Error: expect(locator).toBeVisible() failed
  114 |             return;
  115 |         }
  116 | 
  117 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 15_000 });
  118 |     });
  119 | 
  120 |     test('Scenario 8 — email case insensitivity', async ({ page }) => {
  121 |         const cred = getTestUser();
  122 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  123 | 
  124 |         const login = new LoginPage(page);
  125 |         await login.goto();
  126 |         const upperEmail = cred!.email.toUpperCase();
  127 |         await login.fillCredentials(upperEmail, cred!.password);
  128 |         await login.submit();
  129 | 
  130 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  131 |     });
  132 | 
  133 |     test('Scenario 9 — multiple rapid Sign In clicks still yield single successful login', async ({ page }) => {
  134 |         const cred = getTestUser();
  135 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  136 | 
  137 |         const login = new LoginPage(page);
  138 |         await login.goto();
  139 |         await login.fillCredentials(cred!.email, cred!.password);
  140 |         await login.signInButton.click({ clickCount: 3, delay: 40 });
  141 | 
  142 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  143 |     });
  144 | 
  145 |     test('Scenario 10 — error clears after correction, then login succeeds', async ({ page }) => {
  146 |         const cred = getTestUser();
  147 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  148 | 
  149 |         const login = new LoginPage(page);
  150 |         await login.goto();
  151 |         await login.fillCredentials(cred!.email, `${cred!.password}_bad`);
  152 |         await login.submit();
  153 | 
  154 |         const err = page.locator('.el-form-item__error').first();
  155 |         await expect(err).toBeVisible({ timeout: 15_000 });
  156 | 
  157 |         await login.fillCredentials(cred!.email, cred!.password);
  158 |         await login.submit();
  159 | 
  160 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 45_000 });
  161 |     });
  162 | 
  163 |     test('Scenario 11 — leading/trailing spaces in password: login fails', async ({ page }) => {
  164 |         const cred = getTestUser();
  165 |         test.skip(!cred, 'Нужны TEST_USER_EMAIL и TEST_USER_PASSWORD в .env');
  166 | 
  167 |         const login = new LoginPage(page);
  168 |         await login.goto();
  169 |         await login.emailInput.fill(cred!.email);
  170 |         await login.passwordInput.fill(` ${cred!.password} `);
  171 |         await login.submit();
  172 | 
  173 |         await expect(page).toHaveURL(/\/login/);
  174 |         const err = page.locator('.el-form-item__error').first();
  175 |         await expect(err).toBeVisible({ timeout: 15_000 });
  176 |     });
  177 | 
  178 |     test('Scenario 12 — slow login response: UI waits then redirects', async ({ page }) => {
  179 |         const cred = getTestUser();
  180 |         test.skip(!cred, 'Set TEST_USER_EMAIL and TEST_USER_PASSWORD in .env');
  181 | 
  182 |         await page.route('**/api/auth/login', async (route) => {
  183 |             await new Promise((r) => setTimeout(r, 2800));
  184 |             await route.continue();
  185 |         });
  186 | 
  187 |         const login = new LoginPage(page);
  188 |         await login.goto();
  189 |         await login.fillCredentials(cred!.email, cred!.password);
  190 | 
  191 |         const started = Date.now();
  192 |         await login.submit();
  193 |         await expect(page).not.toHaveURL(/\/login$/, { timeout: 60_000 });
  194 |         expect(Date.now() - started).toBeGreaterThan(2000);
  195 |     });
  196 | 
  197 |     test('Scenario 13 — password visibility toggle (eye icon)', async ({ page }) => {
  198 |         const login = new LoginPage(page);
  199 |         await login.goto();
  200 |         await login.passwordInput.fill('ToggleMe123');
  201 | 
  202 |         await expect(login.passwordInput).toHaveAttribute('type', 'password');
  203 |         await login.togglePasswordVisibility();
  204 |         await expect(login.passwordInput).toHaveAttribute('type', 'text');
  205 |         await login.togglePasswordVisibility();
  206 |         await expect(login.passwordInput).toHaveAttribute('type', 'password');
  207 |     });
  208 | });
  209 | 
```