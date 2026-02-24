# Questions for Coppel SSO to On-Prem Proposal
## Audience and use

1. Who is the primary audience for this proposal? Coppel security/identity team and Tec360 the technology partner implementing IAM Governance systems
2. Is this an internal Cerby document It will be shared with Coppel

## Scope and boundaries

3. What is the exact project name to use (e.g. "Coppel SSO to On-Prem", "Coppel Store SSO", or other)? Coppel SSO to on-prem
4. Are there any items that must be explicitly listed as **out of scope**? (e.g. other Coppel applications, other Cerby products, SAML changes on the on-prem app.) At the moment we will target disconnected (non-SAML compliant) on-prem store systems (just one at the moment, I don't have the name of it)
5. Should the proposal mention the ~4k stores and ~50k users, or keep scale generic? It should mention the specifics we are aware of, but also mention once we develop this capabilities other systems can be supported seamlessly

## Timeline and success

6. Do you have target timeframes for Phase 1 and Phase 2 (even approximate), or should the proposal leave dates open? Do not mention times at the moment
7. How should success be described? (e.g. "all store credentials in EPM", "SSO-like login in pilot stores", or no specific success criteria?) Users don't know credentials to access on-prem disconnected applications, they go to Auth0 and trigger an authentication request that logs in for them in the host machine

## Risks and rewards

8. Are there specific risks you want called out? (e.g. rollout across 4k stores, dependency on Auth0, Coppel’s change management.) No, let's not worry about this yet as it is a high-level proposal
9. Should rewards/benefits be kept to the bullets in the context (secure storage, rotation, SSO-like experience) or do you want to add business outcomes (e.g. compliance, reduced help-desk, time-to-access)? let's map both

## Cerby and Coppel specifics

10. Should the proposal include a one-sentence or one-paragraph Cerby platform description (from the context), or assume the reader already knows Cerby? Assume people know what we are talking about
11. Any Coppel-specific constraints to mention? (e.g. network segmentation, no internet on store machines, specific Windows version.) We don't know yet, we just know target machines are in physical stores for employess to login to the system and the credentials are not secured by any system

## Other
12. This proposal assumes there is a screen a desktop automation can access to update the password on behalf of a user