# Conditional access Baseline

This conditional access baseline is based on the Microsoft Conditional Access Baseline by Claus Jespersen. This one is slightly minimized and less difficult to understand but still protects almost everything you could wish for. Use this baseline to start off with and expend or modify where needed.

> [!TIP]
> This baseline is intended to be deployed through CIPP Conditional Access templates and Standards.


> [!IMPORTANT]
> Do not forget to add your break the glass/emergency access accounts to the exclusion group. When using this baseline that would be **CA-BreakGlassAccounts - Exclude**.

# Table of Contents
- [Conditional access Baseline](#conditional-access-baseline)
- [Table of Contents](#table-of-contents)
  - [Resources](#resources)
  - [Prerequisites](#prerequisites)
  - [Roadmap](#roadmap)
  - [Version history](#version-history)
  - [Changelog](#changelog)
    - [2024.6.1](#202461)
    - [2025.2.1](#202521)
    - [2025.2.2](#202522)
    - [2025.2.3](#202523)
    - [2026.2.1](#202621)
  - [Persona's](#personas)
      - [Global](#global)
      - [Admins](#admins)
      - [Internals](#internals)
      - [Guests](#guests)
  - [Conditional access policies](#conditional-access-policies)
    - [CA000-Global-IdentityProtection-AnyApp-AnyPlatform-MFA](#ca000-global-identityprotection-anyapp-anyplatform-mfa)
    - [CA001-Global-AttackSurfaceReduction-AnyApp-AnyPlatform-BLOCK-CountryWhitelist](#ca001-global-attacksurfacereduction-anyapp-anyplatform-block-countrywhitelist)
    - [CA002-Global-IdentityProtection-AnyApp-AnyPlatform-Block-LegacyAuthentication](#ca002-global-identityprotection-anyapp-anyplatform-block-legacyauthentication)
    - [CA003-Global-BaseProtection-RegisterOrJoin-AnyPlatform-MFA](#ca003-global-baseprotection-registerorjoin-anyplatform-mfa)
    - [CA004-Global-IdentityProtection-AnyApp-AnyPlatform-AuthenticationFlows](#ca004-global-identityprotection-anyapp-anyplatform-authenticationflows)
    - [CA005-Global-DataProtection-Office365-AnyPlatform-Unmanaged-RequireAppProtection](#ca005-global-dataprotection-office365-anyplatform-unmanaged-requireappprotection)
    - [CA006-Global-DataProtection-Office365-iOSenAndroid-RequireAppProtection](#ca006-global-dataprotection-office365-iosenandroid-requireappprotection)
    - [CA100-Admins-IdentityProtection-AdminPortals-AnyPlatform-MFA](#ca100-admins-identityprotection-adminportals-anyplatform-mfa)
    - [CA101-Admins-IdentityProtection-AnyApp-AnyPlatform-MFA](#ca101-admins-identityprotection-anyapp-anyplatform-mfa)
    - [CA102-Admins-IdentityProtection-AllApps-AnyPlatform-SigninFrequency](#ca102-admins-identityprotection-allapps-anyplatform-signinfrequency)
    - [CA103-Admins-IdentityProtection-AllApps-AnyPlatform-PersistentBrowser](#ca103-admins-identityprotection-allapps-anyplatform-persistentbrowser)
    - [CA104-Admins-IdentityProtection-AllApps-AnyPlatform-ContinuousAccessEvaluation](#ca104-admins-identityprotection-allapps-anyplatform-continuousaccessevaluation)
    - [CA105-Admins-IdentityProtection-AnyApp-AnyPlatform-PhishingResistantMFA](#ca105-admins-identityprotection-anyapp-anyplatform-phishingresistantmfa)
    - [CA200-Internals-IdentityProtection-AnyApp-AnyPlatform-MFA](#ca200-internals-identityprotection-anyapp-anyplatform-mfa)
    - [CA202-Internals-IdentityProtection-AllApps-WindowsMacOS-SigninFrequency-UnmanagedDevices](#ca202-internals-identityprotection-allapps-windowsmacos-signinfrequency-unmanageddevices)
    - [CA203-Internals-AppProtection-MicrosoftIntuneEnrollment-AnyPlatform-MFA](#ca203-internals-appprotection-microsoftintuneenrollment-anyplatform-mfa)
    - [CA204-Internals-AttackSurfaceReduction-AllApps-AnyPlatform-BlockUnknownPlatforms](#ca204-internals-attacksurfacereduction-allapps-anyplatform-blockunknownplatforms)
    - [CA205-Internals-BaseProtection-AnyApp-Windows-CompliantorAADHJ](#ca205-internals-baseprotection-anyapp-windows-compliantoraadhj)
    - [CA206-Internals-IdentityProtection-AllApps-AnyPlatform-PersistentBrowser](#ca206-internals-identityprotection-allapps-anyplatform-persistentbrowser)
    - [CA207-Internals-AttackSurfaceReduction-SelectedApps-AnyPlatform-BLOCK](#ca207-internals-attacksurfacereduction-selectedapps-anyplatform-block)
    - [CA208-Internals-BaseProtection-AnyApp-MacOS-Compliant](#ca208-internals-baseprotection-anyapp-macos-compliant)
    - [CA209-Internals-IdentityProtection-AllApps-AnyPlatform-ContinuousAccessEvaluation](#ca209-internals-identityprotection-allapps-anyplatform-continuousaccessevaluation)
    - [CA300-ServiceAccounts-IdentityProtection-AnyApp-AnyPlatform-MFA](#ca300-serviceaccounts-identityprotection-anyapp-anyplatform-mfa)
    - [CA301-ServiceAccounts-AttackSurfaceReduction-AllApps-AnyPlatform-BlockUntrustedLocations](#ca301-serviceaccounts-attacksurfacereduction-allapps-anyplatform-blockuntrustedlocations)
    - [CA400-GuestUsers-IdentityProtection-AnyApp-AnyPlatform-MFA](#ca400-guestusers-identityprotection-anyapp-anyplatform-mfa)
    - [CA401-GuestUsers-AttackSurfaceReduction-AllApps-AnyPlatform-BlockNonGuestAppAccess](#ca401-guestusers-attacksurfacereduction-allapps-anyplatform-blocknonguestappaccess)
    - [CA402-GuestUsers-IdentityProtection-AllApps-AnyPlatform-SigninFrequency](#ca402-guestusers-identityprotection-allapps-anyplatform-signinfrequency)
    - [CA403-Guests-IdentityProtection-AllApps-AnyPlatform-PersistentBrowser](#ca403-guests-identityprotection-allapps-anyplatform-persistentbrowser)
    - [CA404-Guests-AttackSurfaceReduction-SelectedApps-AnyPlatform-BLOCK](#ca404-guests-attacksurfacereduction-selectedapps-anyplatform-block)
  - [Named locations](#named-locations)
  - [Considerations](#considerations)
  - [Troubleshooting](#troubleshooting)
  - [Deploying with CIPP](#deploying-with-cipp)




## Resources
➡ Microsoft Learn: https://learn.microsoft.com/en-us/azure/architecture/guide/security/conditional-access-framework

➡ Framework documentation by Claus Jespersen: https://github.com/microsoft/ConditionalAccessforZeroTrustResources/blob/main/ConditionalAccessGovernanceAndPrinciplesforZeroTrust%20October%202023.pdf

➡ Framework resources: https://github.com/microsoft/ConditionalAccessforZeroTrustResources

➡ idPowerToys for CA documentation: https://idpowertoys.merill.net/

## Prerequisites
* Security Defaults must be disabled before importing Conditional Access policies.
* Make sure **Microsoft Intune Enrollment** (App id: d4ebce55-015a-49b5-a083-c84d1797ae8c) app exists in your tenant. Otherwise, create manually by using `New-MgServicePrincipal -AppId d4ebce55-015a-49b5-a083-c84d1797ae8c`

## Roadmap
* Feedback and enhancement requests can be provided by opening a repository issue.

## Version history
| Version nr | Release date |
| -------- | -------- |
| 2024.4.1 | Released 10-04-2024 |
| 2024.6.1 | Released 26-06-2024 |
| 2025.2.1 | Released 01-02-2025 |
| 2025.2.2 | Released 06-02-2025 |
| 2025.2.3 | Released 13-02-2025 |
| 2026.2.1 | Released 13-02-2026 |


## Changelog
### 2024.6.1
* CA208: Added this policy to require MacOS device compliance 
* CA207: Added this policy to explicitly block certain apps on any platform for the internals persona.
* CA404: Added this policy to explicitly block certain apps on any platform for the guest persona.
* CA103: Added this policy to have never persistent browser sessions on any platform for admins persona
* CA206: Added this policy to have never persistent browser sessions on any platform for internals persona
* CA403: Added this policy to have never persistent browser sessions on any platform for admins persona
* CA006: Added this policy to require App Protection for iOS and Android devices when accessing Exchange Online and SharePoint Online.
* CA100: Added a few Admin roles to require MFA.
* CA101: Added a few Admin roles to require MFA.

### 2025.2.1
* CA104: Added Continuous Access Evaluation for admins
* CA105: Added Phishing Resistant MFA for admins
* CA209: Added Continuous Access Evaluation for internals

### 2025.2.2
* CA206: Wrong exclusion group was assigned. Has been fixed.

### 2025.2.3
* Removed risk-based policies from this baseline because they require Microsoft Entra ID P2.

### 2026.2.1
* Risk-based agent policies are not included because they require Microsoft Entra ID P2.
* CA005: Modified policy from **Require approved client app** to **RequireAppProtection** as this is being retired per March 2026.
  

## Persona's

#### Global
Global is a persona/placeholder for policies that are general 
in nature or do not only apply to one persona. So it is used 
to define policies that apply to all personas or don't apply to 
one specific persona. The reason for having this persona is to 
be able to have a model where we can protect all relevant 
scenarios. It should be used to hold policies that apply to all 
users or policies that enforce protection on scenarios not 
covered by policies for other personas

#### Admins
We define admins in this context as any non-guest identity 
(cloud or synced) that have any Azure AD or other Microsoft 
365 admin Role (like in MDCA, Exchange, Defender for 
Endpoints or Compliance). As guests who have such roles are 
covered in a separate persona, guests are excluded from this 
persona.

#### Internals
Internals cover all users who have an AD account synced to 
Azure AD who are employees of the company and work in a 
standard end-user role.

#### Guests
Guests holds all users who have an Azure AD guest account 
that has been invited into the customer tenant

## Conditional access policies

### CA000-Global-IdentityProtection-AnyApp-AnyPlatform-MFA

This policy requires MFA for all cloud apps, from every platform. It captures all authentications in scope not captured by other MFA policies.

![CA000](./Images/CA000.png)

### CA001-Global-AttackSurfaceReduction-AnyApp-AnyPlatform-BLOCK-CountryWhitelist

This policy blocks all countries, to all cloud apps, from every platform except for the countries configured in the named location **ALLOWED COUNTRIES**. This named location is excluded in this policy.

> [!IMPORTANT]
> Modify the named location with your approved countries. By default only Belgium, Luxembourgh and Netherlands are allowed to have access from.

![CA001](./Images/CA001.png)

### CA002-Global-IdentityProtection-AnyApp-AnyPlatform-Block-LegacyAuthentication

This policy blocks legacy authentication for all users, to all cloud apps, from any platform.

![CA002](./Images/CA002.png)

### CA003-Global-BaseProtection-RegisterOrJoin-AnyPlatform-MFA

This policy requires MFA for all users, to register or join a device to your tenant/environment.

> [!TIP]
> Make sure to disable *Require Multifactor Authentication to register or join devices with Microsoft Entra*. This can be found under https://portal.azure.com -> Entra ID -> Devices -> Device settings.

![CA003](./Images/CA003.png)

### CA004-Global-IdentityProtection-AnyApp-AnyPlatform-AuthenticationFlows

This policy prevents all users from transfering authentication flows from PC to mobile for example. This feature is currently in preview.

![CA004](./Images/CA004.png)

### CA005-Global-DataProtection-Office365-AnyPlatform-Unmanaged-RequireAppProtection

This policyrequires App Protection Policies on unmanaged devices.

![CA005](./Images/CA005.png)

### CA006-Global-DataProtection-Office365-iOSenAndroid-RequireAppProtection

**Note:** This policy will be modified or removed soon as there is some overlap with CA005.

This policy requires App Protection policies for all users when accessing Office 365 data from iOS or Android devices. Admin roles are excluded to make sure the Microsoft 365 App's on the iOS and Android devices do work. This one is designed on the principle that admin roles are only assigned to admin accounts!

![CA006](./Images/CA006.png)

### CA100-Admins-IdentityProtection-AdminPortals-AnyPlatform-MFA

This policy requires MFA for certain admin roles when they access the access Admin Portals. This one is designed on the principle that admin roles are only assigned to admin accounts!

![CA100](./Images/CA100.png)

### CA101-Admins-IdentityProtection-AnyApp-AnyPlatform-MFA

This policy requires MFA for certain admin roles when they access the any cloud app. This one is designed on the principle that admin roles are only assigned to admin accounts!

![CA101](./Images/CA101.png)

### CA102-Admins-IdentityProtection-AllApps-AnyPlatform-SigninFrequency

This policy sets a Sign-in frequency for certain admin roles to a maximum of 12 hours. Admins need to re-authenticate of logon after 12 hours.

> [!NOTE]
> Some organizations assign key roles to their primary identity (which is not ideal), leading to frequent forced sign-ins. It's recommended to assign additional roles based on your personal requirements instead.

![CA102](./Images/CA102.png)

### CA103-Admins-IdentityProtection-AllApps-AnyPlatform-PersistentBrowser

This policy prevents having persistent browser sessions for admins from every device.

![CA103](./Images/CA103.png)

### CA104-Admins-IdentityProtection-AllApps-AnyPlatform-ContinuousAccessEvaluation

This policy allows Microsoft Entra ID to re-evaluate a user's access to resources in near real-time, rather than waiting for the typical token expiration time (which could be up to an hour). Read the Microsoft documentation here: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation#conditional-access-policy-evaluation-preview

> [!IMPORTANT]
> This CA rule cannot be created in Report-only mode. Supported modes are **ON** or **OFF**.

![CA104](./Images/CA104.png)

### CA105-Admins-IdentityProtection-AnyApp-AnyPlatform-PhishingResistantMFA

This policy requires Phishing Resistant MFA for admins. It does exclude Microsoft Graph Command Line Tools (cause i needed it) but you are free to remove it from your policy. It's slightly different from the Template policy. We also include Global Reader and Intune Administrators into the admin role selection.

![CA105](./Images/CA105.png)

### CA200-Internals-IdentityProtection-AnyApp-AnyPlatform-MFA

This policy requires MFA for all internal identities, for all cloud applications, from any platform.


> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA200](./Images/CA200.png)

### CA202-Internals-IdentityProtection-AllApps-WindowsMacOS-SigninFrequency-UnmanagedDevices

This policy sets a Sign-in frequency to a maximum of 12 hours for internals, to all cloud apps, using unmanaged Windows or MacOS devices.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA202](./Images/CA202.png)

### CA203-Internals-AppProtection-MicrosoftIntuneEnrollment-AnyPlatform-MFA

This policy requires MFA for internals when enrolling their devices in Intune.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

> [!IMPORTANT]
> Autopilot Device Preparation (v2) enrollment can fail under this policy, resulting in devices getting stuck during OOBE. This happens because the automated enrollment process is unable to fulfill the MFA requirement. To avoid this issue, add Autopilot Device Preparation users to the exclusion group for this policy.

![CA203](./Images/CA203.png)

### CA204-Internals-AttackSurfaceReduction-AllApps-AnyPlatform-BlockUnknownPlatforms

This policy blocks unknown/unsupported device platforms for internals.

> [!NOTE]
> Currently only Windows, MacOS, Android and iOS are supported. If (for example) Linux or Windows Phone is allowed you need to modify the policy.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA204](./Images/CA204.png)

### CA205-Internals-BaseProtection-AnyApp-Windows-CompliantorAADHJ

This policy requires internals to make use of a Windows device that is compliant or AADHJ (Azure AD Hybrid Joined / Entra ID Hybrid Joined) while accessing any cloud app.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA205](./Images/CA205.png)

### CA206-Internals-IdentityProtection-AllApps-AnyPlatform-PersistentBrowser

This policy prevents having persistent browser sessions for internals from unmanaged devices. Managed and compliant devices are excluded from the policy.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA206](./Images/CA206-new.png)

### CA207-Internals-AttackSurfaceReduction-SelectedApps-AnyPlatform-BLOCK

This policy prevents internals from accessing specific apps. In this example i've blocked a random app. You should review the included and excluded apps. Excluding office 365 is not necessary if its not included. This is just an example. 

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA207](./Images/CA207.png)

### CA208-Internals-BaseProtection-AnyApp-MacOS-Compliant

This policy requires MacOS devices to be compliant for internals.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

![CA208](./Images/CA208.png)

### CA209-Internals-IdentityProtection-AllApps-AnyPlatform-ContinuousAccessEvaluation

This policy allows Microsoft Entra ID to re-evaluate a user's access to resources in near real-time, rather than waiting for the typical token expiration time (which could be up to an hour). Read the Microsoft documentation here: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation#conditional-access-policy-evaluation-preview.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all internals in it. CA-Internals is used as the standard tenant-local target group for internal users.

> [!IMPORTANT]
> This CA rule cannot be created in Report-only mode. Supported modes are **ON** or **OFF**.

![CA209](./Images/CA209.png)

### CA300-ServiceAccounts-IdentityProtection-AnyApp-AnyPlatform-MFA

This policy requires ServiceAccounts to use MFA, from any platform when accessing any cloud app.

> [!IMPORTANT]
> Verify the included group(s) and/or add your custom groups which have all service accounts in it. CA-ServiceAccounts is used as the standard tenant-local target group for service accounts.

![CA300](./Images/CA300.png)

### CA301-ServiceAccounts-AttackSurfaceReduction-AllApps-AnyPlatform-BlockUntrustedLocations

This policy prevents service accounts from logging in from untrusted countries.

> [!IMPORTANT]
> Verify the Named Location which is part of this policy. Add or Remove countries from the imported Named Location.

![CA301](./Images/CA301.png)

### CA400-GuestUsers-IdentityProtection-AnyApp-AnyPlatform-MFA

This policy requires guest to use MFA, from any platform when accessing any cloud app.

![CA400](./Images/CA400.png)

### CA401-GuestUsers-AttackSurfaceReduction-AllApps-AnyPlatform-BlockNonGuestAppAccess

This policy blocks access for guests to all cloud apps (except for those excluded), from any device.

> [!IMPORTANT]
> Make sure to exclude additional cloud apps if any guest needs access to these apps.

> [!NOTE]
> If you're not working with an MSP (Microsoft Partner) that requires access to your tenant, you can also block "Service Provider Users."

![CA401](./Images/CA401.png)

### CA402-GuestUsers-IdentityProtection-AllApps-AnyPlatform-SigninFrequency

This policy sets a Sign-in frequency to a maximum of 12 hours for guests, to all cloud apps, using any device.

![CA402](./Images/CA402.png)

### CA403-Guests-IdentityProtection-AllApps-AnyPlatform-PersistentBrowser

This policy prevents guest from having persistent browser sessions.

![CA403](./Images/CA403.png)

### CA404-Guests-AttackSurfaceReduction-SelectedApps-AnyPlatform-BLOCK

This policy prevents guests from accessing specific apps. In this example i've blocked a random app. You should review the included and excluded apps. Excluding office 365 is not necessary if its not included. This is just an example. 

![CA404](./Images/CA404.png)

## Named locations

| Name | Location type | Assigned to policy |
| -------- | -------- | -------- |
| ALLOWED COUNTRIES | Countries (IP) | CA001-Global-AttackSurfaceReduction-AnyApp-AnyPlatform-BLOCK-CountryWhitelist |
| ALLOWED COUNTRIES - SERVICE ACCOUNTS | Countries (IP) | CA301-ServiceAccounts-AttackSurfaceReduction-AllApps-AnyPlatform-BlockUntr|

## Considerations
1. You might want to remove the "CA - BreakGlassAccounts - Exclude" group from Admin MFA policies (CA101, CA102) if they use MFA and/or only exclude 1 single BreakGlass account.

## Troubleshooting

1. If you encounter an error when importing policies CA203/CA205/CA208, it may be due to the absence of the "Microsoft Intune Enrollment" app in your tenant. To resolve this, recreate it using PowerShell with the following commands:
```
  Connect-MgGraph
  New-MgServicePrincipal -AppId d4ebce55-015a-49b5-a083-c84d1797ae8c
```

2. Error: Policy contains invalid applications: ServicePrincipalNotFound. Some ServicePrincipals might be missing in your tenant. You can manually create these by using `New-MgServicePrincipal -AppId *****-*****-******` |

3. Windows first sign-in restore fails with error _You can’t get there from here. This application contains sensitive information and can only be accessed from devices or client applications that meet management compliance policy._. This is blocked by policy CA205 (CA205-Internals-BaseProtection-AnyApp-Windows-CompliantorAADHJ). Add an exclusion for **Microsoft Activity Feed Service** (d32c68ad-72d2-4acb-a0c7-46bb2cf93873) in this policy.

## Deploying with CIPP

Use CIPP's [CA Templates](https://docs.cipp.app/user-documentation/tenant/conditional/list-template.md) page to browse/import templates, deploy a template, edit a template, save templates to GitHub, or review template sync logs. Use [CA Policies](https://docs.cipp.app/user-documentation/tenant/conditional/list-policies.md) when reviewing a tenant's live policies or when creating a CIPP template from an existing policy.

There are two practical deployment modes:

1. **One-off deployment:** Deploy a template from **Tenant Administration > Conditional Access > CA Templates**. The wizard can set deployment state, exclusions, and replacement behavior. For cross-tenant templates, CIPP calls out `Replace IDs with Display Names` as the safe replacement method so tenant-specific object IDs do not break the deployment.

2. **Standards deployment:** Add the CA template to **Tenant Administration > Standards & Drift**. Standards are for desired-state management: CIPP reapplies the configured standard on a schedule and can overwrite out-of-band admin changes. CIPP's docs describe Standards as reapplying/evaluating every 12 hours in the [Standards & Drift](https://docs.cipp.app/user-documentation/tenant/standards.md) page, while the [Standards Setup](https://docs.cipp.app/setup/implementation-guide/standards-setup.md) guide currently mentions 3 hours. Treat the exact interval as version-dependent and check the live docs or CIPP logs for your instance. In Standards, CIPP always uses `Replace IDs with Display Names`.

Required tenant groups:

Deploy the tenant-local Entra security groups before deploying Conditional Access templates. CIPP can deploy reusable groups from [Group Templates](https://docs.cipp.app/user-documentation/identity/administration/group-templates.md) and [Deploy Group Templates](https://docs.cipp.app/user-documentation/identity/administration/group-templates/deploy.md). Do this as a separate prerequisite step so CA policy deployment can resolve the group display names consistently.

Minimum group structure per tenant:

* `CA-Internals`: include standard internal users who should receive the Internals CA policies. Use dynamic membership if the tenant has a reliable rule; otherwise keep it assigned and managed by onboarding/offboarding.
* `CA-ServiceAccounts`: include only interactive service/shared accounts that cannot yet be replaced with better workload identity patterns. Keep empty if there are none.
* `CA-BreakGlassAccounts - Exclude`: include emergency access accounts before turning policies on.
* Per-policy `... - Exclude` groups: deploy these empty by default. Use them for tenant-specific exceptions instead of editing the CA policy directly.

Recommended order:

1. Create/import CIPP group templates for the required group names.
2. Deploy the group templates to the target tenants.
3. Populate `CA-Internals`, `CA-ServiceAccounts`, and `CA-BreakGlassAccounts - Exclude`.
4. Leave per-policy exclude groups empty unless there is a documented exception.
5. Deploy CA templates in Report-only and confirm CIPP resolves group names as expected.

Recommended CIPP rollout flow:

1. Confirm tenant prerequisites first: Security Defaults off, break-glass account created, emergency exclusions ready, MSP/GDAP access exclusions ready, and the Microsoft Intune Enrollment service principal present if using enrollment/device-compliance policies.
2. Deploy the required tenant groups and populate the target/exclusion groups.
3. Import or create the CA templates in CIPP.
4. Review every template before deployment, especially included users/groups, excluded users/groups, named locations, app targets, authentication strengths, and policy state.
5. Deploy to a pilot tenant or pilot user group in **Report-only** where supported. CIPP's user-level [Conditional Access test](https://docs.cipp.app/user-documentation/identity/administration/users/user/conditional-access.md) page can test application, country, IP address, platform, and client-app scenarios and shows whether a policy applies.
6. Move low-risk controls on first, such as legacy-auth blocking and MFA, then add higher-friction controls like device compliance, location blocks, and strict session controls.
7. After the pilot is clean, either deploy one-off to selected tenants or attach the template to a Standards template for ongoing enforcement.

MSP/GDAP lockout checks:

* **Client tenants:** these templates include the CIPP variable `%msptenantid%` as a **Guest or external users > Service Provider Users > Selected** exclusion. Before deployment, create a CIPP global variable named `msptenantid` with your MSP tenant ID.
* **Direct tenant mode:** exclude the CIPP service account in that tenant instead of the MSP tenant exclusion.
* **Partner tenant:** do not leave the CIPP service account broadly unprotected. CIPP recommends excluding it from other existing CA policies, then protecting it with a dedicated all-cloud-apps MFA policy and sign-in frequency every time.
* **CA401 guest blocking:** verify MSP/GDAP service-provider access still works before enabling tenant-wide. It is intended to block non-approved guest access, and this is exactly the kind of policy that can create partner-admin surprises if exclusions are wrong.
* **Post-deployment proof:** test CIPP actions and GDAP/AOBO portal access after each blocking policy moves from Report-only to On. Do this before adding the policy to a recurring Standard.

Important CIPP gotchas:

* **Standards are enforcement, not just deployment.** If a technician edits a policy directly in Entra, a CIPP Standard can reapply the template later. Deselecting or disabling remediation stops future enforcement but does not undo changes already made.
* **Specific Standards win over broad Standards.** CIPP precedence is individual tenant over tenant group over All Tenants. When two standards conflict at the same specificity, the newer one wins.
* **Named locations travel with templates created from policies.** CIPP says templates include policy settings such as named locations and authentication strengths. Still verify country/IP values in [Named Locations](https://docs.cipp.app/user-documentation/tenant/conditional/list-named-locations.md), especially for CA001 and CA301.
* **CIPP exclusions are not optional hygiene.** Keep break-glass accounts excluded where appropriate. Add service-provider/MSP exceptions only where they are genuinely needed and understood.
* **Continuous Access Evaluation templates are special.** CA104 and CA209 cannot be created in Report-only mode according to this repo's policy notes, so do not include them in a first-pass SMB Standard unless you are ready for direct enable/disable testing.
* **Companion policies matter.** App protection and compliant-device CA policies only work as intended when the matching Intune app protection, enrollment, and compliance policies exist.
* **Back up before broad changes.** CIPP's [Configuration Backup](https://docs.cipp.app/user-documentation/tenant/manage/backup.md) page can schedule or download tenant configuration backups; its restore wizard warns that selected categories are replaced during restore.
* **Use CIPP reports after deployment.** [Policies and Settings Deployed](https://docs.cipp.app/user-documentation/tenant/manage/policies-deployed.md), [Applied Standards Report](https://docs.cipp.app/user-documentation/tenant/manage/applied-standards.md), CA policy logs, and CA template logs are the places to verify what CIPP deployed and what Standards are maintaining.

Current CIPP documentation entry points:

* CIPP documentation index for agents and current page discovery: [llms.txt](https://docs.cipp.app/llms.txt)
* Conditional Access overview: [Tenant Administration > Conditional Access](https://docs.cipp.app/user-documentation/tenant/conditional.md)
* CA policies: [CA Policies](https://docs.cipp.app/user-documentation/tenant/conditional/list-policies.md)
* CA templates: [CA Templates](https://docs.cipp.app/user-documentation/tenant/conditional/list-template.md)
* Named locations: [Named Locations](https://docs.cipp.app/user-documentation/tenant/conditional/list-named-locations.md)
* Standards: [Standards & Drift](https://docs.cipp.app/user-documentation/tenant/standards.md)
* Standards setup: [Standards Setup](https://docs.cipp.app/setup/implementation-guide/standards-setup.md)
* Group templates: [Group Templates](https://docs.cipp.app/user-documentation/identity/administration/group-templates.md)
* Deploy group templates: [Deploy Group Templates](https://docs.cipp.app/user-documentation/identity/administration/group-templates/deploy.md)
* Conditional Access testing: [User Conditional Access test](https://docs.cipp.app/user-documentation/identity/administration/users/user/conditional-access.md)
* CIPP service account and GDAP CA guidance: [Conditional Access Configuration](https://docs.cipp.app/setup/installation/conditionalaccess.md)
* Configuration backup: [Configuration Backup](https://docs.cipp.app/user-documentation/tenant/manage/backup.md)
* Deployed policies report: [Policies and Settings Deployed](https://docs.cipp.app/user-documentation/tenant/manage/policies-deployed.md)
