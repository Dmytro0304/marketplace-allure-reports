# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: api/my-quotes.spec.ts >> My Quotes — API @api >> GET my-quotes returns paginated list and meta
- Location: e2e/tests/api/my-quotes.spec.ts:10:9

# Error details

```
Error: login: expected JSON from https://v3-marketplace-dev.soilconnect.com/api/auth/login but got 403 text/html (body starts with: <!DOCTYPE html><html lang="en-US"><head><title>Just a moment...</title><meta http-equiv="Content-Type" content="text/htm…). Set API_DEV_URL in .env to the JSON API base (e.g. https://host/api).
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
  33 |     const contentType = res.headers()['content-type'] ?? '';
  34 |     const raw = await res.text();
  35 | 
  36 |     let body: LoginResponse;
  37 |     try {
  38 |         body = JSON.parse(raw) as LoginResponse;
  39 |     } catch {
> 40 |         throw new Error(
     |               ^ Error: login: expected JSON from https://v3-marketplace-dev.soilconnect.com/api/auth/login but got 403 text/html (body starts with: <!DOCTYPE html><html lang="en-US"><head><title>Just a moment...</title><meta http-equiv="Content-Type" content="text/htm…). Set API_DEV_URL in .env to the JSON API base (e.g. https://host/api).
  41 |             `login: expected JSON from ${getApiBaseUrl()}/auth/login but got ${status} ${contentType.split(';')[0]} (body starts with: ${raw.slice(0, 120).replace(/\s+/g, ' ').trim()}…). Set API_DEV_URL in .env to the JSON API base (e.g. https://host/api).`
  42 |         );
  43 |     }
  44 | 
  45 |     if (status >= 400) {
  46 |         throw new Error(`login failed: HTTP ${status} ${JSON.stringify(body)}`);
  47 |     }
  48 | 
  49 |     expectJsonSuccess(body);
  50 | 
  51 |     const token = body.access_token;
  52 |     if (!token) {
  53 |         throw new Error('login response missing access_token');
  54 |     }
  55 | 
  56 |     return { token, body };
  57 | }
  58 | 
  59 | export function authHeaders(token: string): Record<string, string> {
  60 |     return {
  61 |         Accept: 'application/json',
  62 |         'Device-Type': getDeviceType(),
  63 |         Authorization: `Bearer ${token}`,
  64 |     };
  65 | }
  66 | 
```