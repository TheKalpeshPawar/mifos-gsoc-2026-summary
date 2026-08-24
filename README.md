<a name="readme-top"></a>

<div align="center">

<h1>Google Summer of Code 2026 — Mifos X Open Banking App</h1>

<p>
  This repository documents my GSoC 2026 work with the <a href="https://github.com/openMF">Mifos Initiative</a>: a standalone Open Banking reference app built with <b>Kotlin Multiplatform + Compose Multiplatform</b>, integrating with the <b>HSBC UK Open Banking sandbox</b> (OBIE v4.0 / FAPI).
</p>

<p>
  <img alt="GSoC 2026" src="https://img.shields.io/badge/GSoC-2026-ffa500?logo=google&logoColor=white">
  <img alt="Kotlin Multiplatform" src="https://img.shields.io/badge/Kotlin-Multiplatform-7F52FF?logo=kotlin&logoColor=white">
  <img alt="Compose Multiplatform" src="https://img.shields.io/badge/Compose-Multiplatform-2E7D32?logo=jetpackcompose&logoColor=white">
  <img alt="Ktor" src="https://img.shields.io/badge/Ktor-087CFA?logo=kotlin&logoColor=white">
  <img alt="Koin" src="https://img.shields.io/badge/Koin-DI-000000?logo=kotlin&logoColor=white">
</p>

</div>

## Table of Contents

- [Project Overview](#project-overview)
- [Pull Requests](#pull-requests)
- [Demo](#demo)
- [What's Left to Do](#whats-left-to-do)
- [Conclusion](#conclusion)
- [Additional Links](#additional-links)

## Project Overview

The GSoC 2026 project — **Mifos X Open Banking App** — is a reference implementation demonstrating how third-party fintechs can leverage Open Banking standards (PSD2, UK Open Banking) to provide innovative financial services to users of Mifos/Fineract-powered institutions and beyond.

The original project idea targeted the **Open Bank Project (OBP)** sandbox. Over the course of the summer the work pivoted and was **rebuilt on the HSBC UK Open Banking sandbox** — the OBIE v4.0 / FAPI reference the project now targets — culminating in the two halves of Open Banking:

- **AISP — Account Information Services.** Connect a bank and consent to data access, then aggregate accounts, balances, transaction history, statements, standing orders, direct debits, scheduled payments, beneficiaries and product details. Includes a full OAuth consent journey (`private_key_jwt` client auth over mutual TLS) with granular consent management and revoke.
- **PISP — Payment Initiation Services.** Initiate **single**, **scheduled** and **standing-order** payments on both the domestic and international rails, each with Strong Customer Authentication, plus **Variable Recurring Payments (VRP)** — a separate consent/session family for recurring debits.

Built with **Kotlin Multiplatform + Compose Multiplatform** (Android, iOS, desktop and web from one codebase), Ktor, Koin, Store5, Room, and a FAPI-compliant network stack with mutual TLS and detached-JWS message signing.

> **Repo:** [`openMF/mifos-x-open-banking`](https://github.com/openMF/mifos-x-open-banking)

## Pull Requests

All work was merged into [`openMF/mifos-x-open-banking`](https://github.com/openMF/mifos-x-open-banking). Jira tickets were tracked under the [MXOBA project](https://mifosforge.jira.com/browse/MXOBA) on Mifos Forge.

| No. | PR | Jira tickets | Description |
| --- | --- | --- | --- |
| 1 | [#10 — Standing orders and Variable Recurring Payments](https://github.com/openMF/mifos-x-open-banking/pull/10) | [MXOBA-68](https://mifosforge.jira.com/browse/MXOBA-68), [MXOBA-83](https://mifosforge.jira.com/browse/MXOBA-83), [MXOBA-84](https://mifosforge.jira.com/browse/MXOBA-84), [MXOBA-85](https://mifosforge.jira.com/browse/MXOBA-85) | Adds standing orders as the third payment flow (domestic + international rails) — recurring payments with frequency, first/final amounts and optional end date — and **Variable Recurring Payments** end-to-end: one-time consent with per-period control parameters, then single-screen payments checked against the limits. |
| 2 | [#8 — Scheduled payments - International and Domestic](https://github.com/openMF/mifos-x-open-banking/pull/8) | [MXOBA-79](https://mifosforge.jira.com/browse/MXOBA-79), [MXOBA-82](https://mifosforge.jira.com/browse/MXOBA-82) | Schedules a payment for a future date on both OBIE scheduled rails (domestic + international), reached from the Schedule card on the Payments Hub. |
| 3 | [#7 — Domestic and international single payments](https://github.com/openMF/mifos-x-open-banking/pull/7) | [MXOBA-78](https://mifosforge.jira.com/browse/MXOBA-78), [MXOBA-80](https://mifosforge.jira.com/browse/MXOBA-80), [MXOBA-81](https://mifosforge.jira.com/browse/MXOBA-81) | PISP single payments (domestic + international): four new modules — `send-money`, `payment-consent`, `payment-status`, `payments-hub` — over a new PISP network/data layer (FAPI headers + detached JWS). |
| 4 | [#6 — Rebuild the app on the HSBC UK Open Banking sandbox](https://github.com/openMF/mifos-x-open-banking/pull/6) | [MXOBA-56](https://mifosforge.jira.com/browse/MXOBA-56), [MXOBA-58](https://mifosforge.jira.com/browse/MXOBA-58), [MXOBA-59](https://mifosforge.jira.com/browse/MXOBA-59), [MXOBA-60](https://mifosforge.jira.com/browse/MXOBA-60), [MXOBA-61](https://mifosforge.jira.com/browse/MXOBA-61), [MXOBA-62](https://mifosforge.jira.com/browse/MXOBA-62), [MXOBA-63](https://mifosforge.jira.com/browse/MXOBA-63), [MXOBA-64](https://mifosforge.jira.com/browse/MXOBA-64), [MXOBA-65](https://mifosforge.jira.com/browse/MXOBA-65), [MXOBA-66](https://mifosforge.jira.com/browse/MXOBA-66), [MXOBA-67](https://mifosforge.jira.com/browse/MXOBA-67), [MXOBA-69](https://mifosforge.jira.com/browse/MXOBA-69), [MXOBA-70](https://mifosforge.jira.com/browse/MXOBA-70), [MXOBA-71](https://mifosforge.jira.com/browse/MXOBA-71), [MXOBA-72](https://mifosforge.jira.com/browse/MXOBA-72), [MXOBA-73](https://mifosforge.jira.com/browse/MXOBA-73), [MXOBA-75](https://mifosforge.jira.com/browse/MXOBA-75), [MXOBA-76](https://mifosforge.jira.com/browse/MXOBA-76), [MXOBA-77](https://mifosforge.jira.com/browse/MXOBA-77) | Rebuilds the app on the HSBC UK sandbox: a FAPI-compliant network stack (`private_key_jwt` + mutual TLS), the OAuth consent journey, and 18 feature modules covering the AIS surface (accounts, transactions, statements, standing orders, direct debits, scheduled payments, beneficiaries, product, account-holder, settings, home, login/consent). |
| 5 | [#4 — Build the Mifos X Open Banking app on the OBP sandbox](https://github.com/openMF/mifos-x-open-banking/pull/4) | [MXOBA-15](https://mifosforge.jira.com/browse/MXOBA-15), [MXOBA-16](https://mifosforge.jira.com/browse/MXOBA-16), [MXOBA-17](https://mifosforge.jira.com/browse/MXOBA-17), [MXOBA-18](https://mifosforge.jira.com/browse/MXOBA-18), [MXOBA-19](https://mifosforge.jira.com/browse/MXOBA-19), [MXOBA-20](https://mifosforge.jira.com/browse/MXOBA-20), [MXOBA-21](https://mifosforge.jira.com/browse/MXOBA-21), [MXOBA-22](https://mifosforge.jira.com/browse/MXOBA-22), [MXOBA-23](https://mifosforge.jira.com/browse/MXOBA-23), [MXOBA-24](https://mifosforge.jira.com/browse/MXOBA-24), [MXOBA-25](https://mifosforge.jira.com/browse/MXOBA-25), [MXOBA-26](https://mifosforge.jira.com/browse/MXOBA-26), [MXOBA-27](https://mifosforge.jira.com/browse/MXOBA-27), [MXOBA-28](https://mifosforge.jira.com/browse/MXOBA-28), [MXOBA-29](https://mifosforge.jira.com/browse/MXOBA-29), [MXOBA-30](https://mifosforge.jira.com/browse/MXOBA-30), [MXOBA-31](https://mifosforge.jira.com/browse/MXOBA-31), [MXOBA-32](https://mifosforge.jira.com/browse/MXOBA-32), [MXOBA-33](https://mifosforge.jira.com/browse/MXOBA-33), [MXOBA-34](https://mifosforge.jira.com/browse/MXOBA-34), [MXOBA-35](https://mifosforge.jira.com/browse/MXOBA-35), [MXOBA-38](https://mifosforge.jira.com/browse/MXOBA-38), [MXOBA-39](https://mifosforge.jira.com/browse/MXOBA-39), [MXOBA-40](https://mifosforge.jira.com/browse/MXOBA-40), [MXOBA-41](https://mifosforge.jira.com/browse/MXOBA-41), [MXOBA-42](https://mifosforge.jira.com/browse/MXOBA-42), [MXOBA-43](https://mifosforge.jira.com/browse/MXOBA-43), [MXOBA-44](https://mifosforge.jira.com/browse/MXOBA-44), [MXOBA-45](https://mifosforge.jira.com/browse/MXOBA-45), [MXOBA-46](https://mifosforge.jira.com/browse/MXOBA-46), [MXOBA-47](https://mifosforge.jira.com/browse/MXOBA-47), [MXOBA-48](https://mifosforge.jira.com/browse/MXOBA-48), [MXOBA-50](https://mifosforge.jira.com/browse/MXOBA-50), [MXOBA-51](https://mifosforge.jira.com/browse/MXOBA-51), [MXOBA-52](https://mifosforge.jira.com/browse/MXOBA-52), [MXOBA-53](https://mifosforge.jira.com/browse/MXOBA-53), [MXOBA-54](https://mifosforge.jira.com/browse/MXOBA-54) | The initial app on the Open Bank Project (OBP) sandbox: authentication (DirectLogin + OIDC), accounts, payments, standing orders, transactions, insights, cards, ATM locator and settings. |
| 6 | [#3 — Template sync and Customization](https://github.com/openMF/mifos-x-open-banking/pull/3) | — | Syncs the Kotlin Multiplatform project template and customizes it for the Mifos X Open Banking app. |

## Demo

Demo videos of the main journeys.

### AISP — Account Information Service

<!-- VIDEO_PLACEHOLDER: AISP -->

### PISP — Payment Initiation Service

#### Single Payment

<!-- VIDEO_PLACEHOLDER: PISP - Single Payment -->

#### Standing Orders

<!-- VIDEO_PLACEHOLDER: PISP - Standing Orders -->

#### Scheduled Payments

<!-- VIDEO_PLACEHOLDER: PISP - Scheduled Payments -->

#### Variable Recurring Payments

<!-- VIDEO_PLACEHOLDER: PISP - Variable Recurring Payments -->

## What's Left to Do

The app is functionally complete — AISP, PISP and VRP are all wired end-to-end against the HSBC sandbox. The only remaining work is a **UI rework**: aligning the screens with the shared component library (`Mifos*` / `KptScaffold`) for a consistent look and feel.

## Conclusion

Over the summer I built the Mifos X Open Banking app from the KMP template up: a FAPI-compliant Open Banking client that connects to HSBC, consents to data access, surfaces the full AIS read surface, and then — on the write side — initiates single, scheduled and standing-order payments plus Variable Recurring Payments, each through bank authorisation and back to a settled status. The work closed out Jira tickets spanning **MXOBA-15** through **MXOBA-85** (65 tickets) across **6 merged pull requests**.

## Additional Links

- **[OAuth callback bridge](https://github.com/TheKalpeshPawar/obp-callback)** — a page hosted on my GitHub repo at `https://thekalpeshpawar.github.io/obp-callback/`, used as the app's OAuth consent `redirect_uri`. The HSBC UK Open Banking sandbox (FAPI-compliant) requires the redirect URI to be a registered **HTTPS** URL, which a native app cannot provide without a production domain — so this GitHub-hosted page supplies that HTTPS endpoint, and its JavaScript relays the authorisation response back into the app.
- **[HSBC Open Banking API catalogue](https://develop.hsbc.com/apis?f%5B0%5D=solutions%3A435)** — the HSBC sandbox's Open Banking API catalogue.
- **[HSBC UK Open Banking Implementation Guide (v4)](https://develop.hsbc.com/sites/default/files/open_banking/HSBC%20UK%20Open%20Banking%20Implementation%20Guide%20(v4).pdf)** — the official implementation guide.
- **[AISP — Account Information](https://develop.hsbc.com/ob-api-documentation/account-information-uk-hsbc-personal)** — Account Information Service API documentation.
- **[PISP — Payment Initiation (incl. VRP)](https://develop.hsbc.com/ob-api-overview/payment-initiation-uk-hsbc-personal)** — Payment Initiation Service API documentation.

<div align="right">

[![Back To Top](https://img.shields.io/badge/Back%20To%20Top-Blue?style=flat)](#readme-top)

</div>
