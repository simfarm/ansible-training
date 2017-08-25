### Ansible Tower

What is Ansible Tower?
* Enterprise Ansible: Ansible with added features.

Major features include:
* API (extensible, what the UI actually interfaces with).
* RBAC and delegated controls.
* Enterprise scalling (multiple job runners working in parallel).
* Logging: stored job event data and integration with external loggers.
* Scheduled jobs and workflows: a Jenkins alternative.
* Security (credentials obfuscation).

---

#### Lab

Create Tower resources:
* Authenticate to Tower. For username put `admin`; for password put `fo0m4nchU`.
* Create organizations: sales and engineering.
* Create users: Danielle Blount, Joe Costigan. For password, put `test`.
* Create users: Aaron Withrow, Christian Adams. For password, put `test`.
* Create James Laska as system administrator (can do anything).
* Create Timothy Cramer as system auditor (can see Tower resources only).
* Create project of type `Git` with the engineering organization. For `SCM URL` put `https://github.com/jlaska/ansible-playbooks`.
* Create an inventory with the engineering organization.
* Create a host for this inventory. Call it localhost and in the `VARIABLES` section, put:
```
ansible_connection: local
```
* Create a machine credential. For `USERNAME` put `root` and for `SSH PRIVATE KEY` put:
```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAqjjjvyrlHnhQG4xyR95562HqbQXE+n/kuWriipaKRGSw+h8H
AdG4mhxPZ5pNWMwOf1x0hn7l6JY8tqM5wPrWYEyIJMyO6cU3DfqKyWlSaRctkaLI
0Kah92Q1pplvOoFxxebhzIOTZAa12uzV9lEpOBUpePe16DffxsP5NpA2UgAifWBX
dZMyLRHW9Kd36mDb7Qjd9y5vFv2wcKHo6ditVONYNhVKNG7bo6Pi9zxh1PNYBULa
zZJHv8h+77EZevHeaujyz5AHg4btup/E6HKKlpsoVpucO8W+Af5VNnB+UhXkQruV
SiobG1qmapO50cBhb8KZSciBSWUhEyib8sFv7QIDAQABAoIBAFRz4zKeUox6fqwc
Uzqq+2w36Tnr6d2qhE0l5X2C0Ni76D5AFJbneSIkt5ScLpHGs86mjT2JSgHKQBcR
Bn9jM+cVMVqojqMW8Iij7CWfdn6jPD2MOPukIKl/80pTx6aMQGlCcnaoNQEkfyc9
563MeJnVjfzxUTQEPKb95fAXPowRq9sDdwhi4ReFiqAlxXHZmTFC25S8Pwiydy6r
21EVC6pG736DXKwG2N7xWANGOi8D+xf4t9ZflDe940xdfTfk00K4u6XogIFTfXUP
PlDeGLVnSflCBVLdt+BOSSuJ4WO8UNBfDCVjyDY9vH3dotOVF5shYLaQTkVlZUeM
drACgJUCgYEA1Uzvq5waAd/I03Er9jk4HjlE5gh2bebKxblCm9lPPOdfvgY6DGgC
7pKGlx9PInAaNy9Ajub7XkN3fuHAbUOcoiIq/YCwjDQBVXBUIFwqTkCqKU2ynSMi
nNFMNcA9AVUP5Mt21mzR8Ca0Ga+GNNiYKjBikHkMIWYjnt/SH1S7Zz8CgYEAzExP
HW5FeSBtFIGxLJWyX6go7c2CtlBRZzct11Px84H0zmYo3NoFxVsK/cBWI83UTROM
TxKtOGWl+/NSfGIFhmwwCAqeRZewPwbCwTrAQmr2jULvsy7Q4iQGwctp0ILhKY8Y
HZ3AnjRmqPuxBsVF02WRjwQb4P0HHW5FfIrt6dMCgYAKoF+cXBWLnFuD9TJsfONH
1jCRiUBlL0dQ3G7uFsB0104UyHih35itzAz6gGvP2mfj8e20cNt7Eb9lSdftWZ33
Ed60bHHfOkQKvqLiTdUputz/W8iXPYXe7Cpwzxf69gLpsh1Eh31aCoOUeAMmpNfH
2ks+yVkKXO1PX/U27GC9vwKBgDtpmbxyXCvcnTxQdykDI8ujyLtXf8LrWrEMn/02
AXAShBIeLZYEpZb+YhTngWWKL0p2+9/nC48SKJI78eoQS5ELF3DPPbX5Zhz+J1cw
ccce+jKcm77dR4vsdDaZpF0qIrcGUToTrXeUv6I3CAVzC1pt+EXCKSVmEFKjxftx
H71XAoGAX9G6y+DeRqR1hSI7kWjliauCNodMAE+ZVN0lokyIzYYgtst1pepqnxaB
VKtigWdGGLCXBQDmW+HgiNMJnwNjAovYm9q74JcskRCXUi/x0PYKJB2zBRk7eTfT
Tb1IZLuerrbt/cVaXBoB4M/Vd50arOHTkiVJ5cimY99Wd34nU+E=
-----END RSA PRIVATE KEY-----
```
* Create a job template with our created inventory, project, and machine credential. Call it "Sales Demo." For its playbook, pick `dynamic_inventory.yml`.
* Create a job template with our created inventory, project, and machine credential. Call it "Check Network Connectivity." For its playbook, pick `ping-20.yml`.
* Run both job templates.

Implement and verify RBAC:
* Give Danielle Blount and Joe Costigan the "member" permission of the "Sales" organization.
* Give Aaron Withrow and Christian Adams the "member" permission of the "Engineering" organization.
* Give all sales users the "execute" permission of the "Sales Demo" job template.
* Give all engineering users the "admin" permission of both job templates.
* Authenticate as Joe Costigan.
* Verify that he cannot see "Check Network Connectivity" job template. Verify that he cannot edit the "Sales Demo" job template. Verify that he can only see members of his own organization.
* Launch "Sales Demo" job template as Joe Costigan.
* Authenticate as Aaron Withrow.
* Verify that he can see both job templates. Verify that he can edit both job templates. Verify that he can only see members of his own organization.
* Launch both job templates as Aaron Withrow.
* Verify that James Laska can do anything.
* Verify that Timothy Cramer can see all resources but cannot create/modify/delete resources.

Advanced:
* Authenticate as admin user again.
* Run an ad hoc command. To do this navigate to the "INVENTORIES" tab and then pick your inventory. Then go to the "HOSTS" tab. Then check off the host that you want and then click "RUN COMMANDS."
* Invoke the ping module. Use the credential that you already created.
* Create an hourly scheduled job for our "Check Network Connectivity" job template. Set it to run indefinitely.
* Verify stored job standard output under the entries under `/#/jobs/N/stdout/`.
* Create an organization via `/api/v2/organizations/`. As a payload, supply:
```
{
    "name": "Test",
    "description": ""
}
```
* Verify your created organization under `/#/organizations/.`
* Verify that our credential information gets obfuscated: revisit our created credential and attempt to view our `SSH PRIVATE KEY`.
