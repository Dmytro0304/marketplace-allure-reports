# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: api/auth.login.spec.ts >> WC Sign In — API @api >> WC-001: valid credentials return access_token and user
- Location: e2e/tests/api/auth.login.spec.ts:10:9

# Error details

```
SyntaxError: Unexpected token '<', "<!DOCTYPE "... is not valid JSON
```

# Test source

```ts
  1  | import { APIRequestContext } from '@playwright/test';
  2  | import { getApiBaseUrl, getDeviceType } from './env';
  3  | import { expectJsonSuccess } from './validators';
  4  | 
  5  | export type LoginResponse = {
  6  |     result: boolean;
  7  |     access_token?: string;
  8  |     user?: { id: number; email?: string };
  9  |     message?: string;
  10 | };
  11 | 
  12 | /**
  13 |  * Performs marketplace web login against POST /api/auth/login (same contract as Postman "Log In").
  14 |  */
  15 | export async function loginMarketplaceWeb(
  16 |     request: APIRequestContext,
  17 |     email: string,
  18 |     password: string
  19 | ): Promise<{ token: string; body: LoginResponse }> {
  20 |     const res = await request.post(`${getApiBaseUrl()}/auth/login`, {
  21 |         headers: {
  22 |             Accept: 'application/json',
  23 |             'Content-Type': 'application/json',
  24 |             'Device-Type': getDeviceType(),
  25 |         },
  26 |         data: {
  27 |             email,
  28 |             password,
  29 |         },
  30 |     });
  31 | 
  32 |     const status = res.status();
> 33 |     const body = (await res.json()) as LoginResponse;
     |                   ^ SyntaxError: Unexpected token '<', "<!DOCTYPE "... is not valid JSON
  34 | 
  35 |     if (status >= 400) {
  36 |         throw new Error(`login failed: HTTP ${status} ${JSON.stringify(body)}`);
  37 |     }
  38 | 
  39 |     expectJsonSuccess(body);
  40 | 
  41 |     const token = body.access_token;
  42 |     if (!token) {
  43 |         throw new Error('login response missing access_token');
  44 |     }
  45 | 
  46 |     return { token, body };
  47 | }
  48 | 
  49 | export function authHeaders(token: string): Record<string, string> {
  50 |     return {
  51 |         Accept: 'application/json',
  52 |         'Device-Type': getDeviceType(),
  53 |         Authorization: `Bearer ${token}`,
  54 |     };
  55 | }
  56 | 
```