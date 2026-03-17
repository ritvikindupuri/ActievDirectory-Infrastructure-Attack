# Attack Simulation

This section documents the controlled attack simulation performed after the Nutanix and Active Directory environment was fully operational.

## Initial Foothold

The simulated attack originated from `G13S1WIN11VM`, a domain-joined Windows 11 workstation. This system served as the initial attacker-controlled host inside the domain environment.

## Reconnaissance

The first stage focused on identifying valid users and domain context using native Windows tools.

Commands executed included:

- `whoami`
- `echo %USERDOMAIN%`
- `echo %logonserver%`
- `net user /domain`
- `net group "Domain Admins" /domain`
- `setspn -Q */*`

These outputs confirmed:
- membership in the `GROUP13` domain
- the active logon server
- multiple valid domain users
- the presence of SPNs associated with domain services

## Credential Access

A controlled password spraying test was then performed. This resulted in successful authentication as the domain user `abrown`.

This demonstrated that the environment was vulnerable to a credential attack at the authentication layer.

## Post-Compromise Validation

After compromising `abrown`, the following commands were used to inspect the user’s privilege level:

- `whoami`
- `whoami /groups`
- `whoami /priv`

The outputs showed that the compromised account was a standard domain user with no local administrator or domain administrator privileges.

## Lateral Movement Attempt

A lateral movement attempt was performed against the domain controller using:

- `net view`
- `dir \\G13SRV01VM\C$`

The results showed access failure and denied administrative share access, confirming that the compromised user account could not move laterally into Tier 0 infrastructure.

## Outcome

The simulation produced a realistic result:

- initial compromise succeeded
- privilege escalation did not succeed
- lateral movement to the domain controller failed
- the environment contained the attack

This demonstrates a defense-in-depth scenario where weak authentication practices can still be mitigated by strong authorization and internal access controls.
