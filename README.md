# Okta SSO / MFA Lifecycle Lab

Hands-on lab, Sep 2026.

Ticket-style access lifecycle in **Okta Integrator Free**: create a test user, put them in an app group, require MFA for the SAML app, prove SSO into a demo SP, then revoke by removing group membership so the tile disappears.

This is **not** Entra ID, Windows AD, or CyberKy/LLDAP. Those live in other repos.

## Scope

| # | Item | Dump |
| --- | --- | --- |
| 1 | Okta org + admin console (Integrator Free) | Done (24 Sep 2026) |
| 2 | Test user **testuser@salamiam.com** created | Done (24 Sep 2026) |
| 3 | Group **SSO-App-Users** (“Users allowed to sign in to the lab SSO app”) | Done (24 Sep 2026) |
| 4 | **Lab SAML App** (SAML 2.0) → ACS `https://sptest.iamshowcase.com/acs`; Audience/SP Entity ID `IAMShowcase`; Name ID EmailAddress | Done (24 Sep 2026) |
| 5 | App assigned to **SSO-App-Users**; Sign On policy **Any two factors** | Done (24 Sep 2026) |
| 6 | End-user dashboard shows Lab SAML App tile | Done (24 Sep 2026) |
| 7 | SSO proof: Hello **testuser@salamiam.com** on protected SP; Status Success; Issuer Okta; Audience IAMShowcase | Done (24 Sep 2026) |
| 8 | Revoke: remove from group → dashboard empty (“Add apps to your launcher”) | Done (24 Sep 2026) |

## Environment

| Object | Value |
| --- | --- |
| Org | Okta Integrator Free `salamiam-integrator-9306838` |
| Admin | `abdisalam@salamiam.com` (Cloudflare Email Routing on salamiam.com → Gmail) |
| End-user URL | `https://integrator-9306838.okta.com` |
| Test User | `testuser@salamiam.com` (Okta Verify enrolled) |
| Group | **SSO-App-Users** — member for grant; removed for revoke proof |
| App | **Lab SAML App** (SAML 2.0) |
| ACS | `https://sptest.iamshowcase.com/acs` |
| Audience / SP Entity ID | `IAMShowcase` |
| Name ID | EmailAddress |
| Sign On policy | Any two factors |

## Screenshots (24 Sep 2026 dump)

- [Okta admin console](screenshots/01-okta-admin-console.png)
- [Add Person: testuser@salamiam.com](screenshots/02-add-person-testuser.png)
- [People: Test User created](screenshots/03-people-testuser-created.png)
- [Group SSO-App-Users](screenshots/04-group-sso-app-users.png)
- [SAML settings: ACS + Audience IAMShowcase](screenshots/05-saml-settings.png)
- [Lab SAML App active](screenshots/06-lab-saml-app-active.png)
- [App auth policy: Any two factors](screenshots/07-app-auth-policy-any-two-factors.png)
- [App assigned to SSO-App-Users](screenshots/08-app-assigned-to-group.png)
- [Test User dashboard: Lab SAML App tile](screenshots/09-testuser-dashboard-tile.png)
- [SSO success: Hello testuser@salamiam.com](screenshots/10-sso-success-hello-testuser.png)
- [SSO AuthN details](screenshots/11-sso-authn-details.png)
- [SSO assertion: Status Success + Issuer Okta](screenshots/12-sso-assertion-success-issuer.png)
- [SSO Audience IAMShowcase](screenshots/13-sso-audience-iamshowcase.png)
- [SSO-App-Users: Test User removed](screenshots/14-sso-app-users-testuser-removed.png)
- [Dashboard tile gone — Add apps to your launcher](screenshots/15-testuser-dashboard-tile-gone.png)

## What was built

- Stood up an Okta Integrator Free org and created test user **testuser@salamiam.com**.
- Created group **SSO-App-Users** for who is allowed into the lab SSO app.
- Configured **Lab SAML App** (SAML 2.0) against IAMShowcase (ACS + Audience), Name ID EmailAddress.
- Assigned the app to the group and set Sign On to **Any two factors** (Okta Verify on the test user).
- Proved grant: tile on the end-user dashboard, then successful federation to the protected SP.
- Proved revoke: removed the user from the group; dashboard shows no app tile.

## How to redo it

1. Open the Okta Admin Console for the Integrator Free org.
2. Directory → People → Add Person: **testuser@salamiam.com**; activate; enroll Okta Verify.
3. Directory → Groups → create **SSO-App-Users**; add the test user.
4. Applications → Create App Integration → SAML 2.0: ACS `https://sptest.iamshowcase.com/acs`, Audience `IAMShowcase`, Name ID EmailAddress.
5. Assign **Lab SAML App** to **SSO-App-Users**; set app Sign On policy to Any two factors.
6. As the test user, open the end-user home and launch the tile; complete MFA; land on the protected SP and capture assertion details.
7. Remove the test user from **SSO-App-Users**; refresh the end-user home and confirm the tile is gone.

## What broke / notes

- Desktop / OS panel clocks may appear in some shots; screenshots were not watermark-edited.
- No temporary-password dialogs were committed (Add Person used activation without “I will set password”).
- Admin email routes via Cloudflare Email Routing on salamiam.com into Gmail.

## Demo walkthrough

1. Show the admin console and the created test user.
2. Show **SSO-App-Users** and the SAML app settings (ACS + Audience).
3. Show assignment + **Any two factors** policy.
4. Show the end-user dashboard with the Lab SAML App tile.
5. Show SSO success (Hello testuser) and assertion slices (Success, Issuer Okta, Audience IAMShowcase).
6. Show remove-from-group success, then the empty launcher (“Add apps to your launcher”).
7. Explain in ticket language: group membership grants the app; MFA protects the sign-in; removing membership revokes the tile without deleting the person.

## Own words (from the sitting)

I've built test users and groups and assigned applications to show how to move someone through what's asked of me if they need to be added to things and building protections in having them sign into app access having them verify through Okta Verify authenticator and giving them Single Sign Option and putting through them life cycle changes and removing them when they are done with project or said assignment so keeping them secure and having it where they're the only have access to something and that they can't get breached and if a breach happened most likely its because they gave someone access because i closed all doors.

## Stop there

Entra, AD lifecycle, CyberKy/LLDAP, and CyberArk are other sittings / other repos. Do not invent those stacks into this package.
