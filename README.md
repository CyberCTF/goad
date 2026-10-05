# GOAD (Game of Active Directory)

The full GOAD lab by [Orange Cyberdefense](https://github.com/Orange-Cyberdefense/GOAD): two
forests, three domains, five Windows servers, with the vulnerabilities GOAD sets up. This
repository runs it with [Isoloom](https://www.isoloom.com): [`isoloom.yml`](isoloom.yml) describes
the machines, and GOAD's own Ansible playbooks build the lab from a controller.

| Machine | Name | Domain | Windows |
| --- | --- | --- | --- |
| dc01 | KINGSLANDING | sevenkingdoms.local | Server 2019 |
| dc02 | WINTERFELL | north.sevenkingdoms.local | Server 2019 |
| dc03 | MEEREEN | essos.local | Server 2016 |
| srv02 | CASTELBLACK | north.sevenkingdoms.local | Server 2019 |
| srv03 | BRAAVOS | essos.local | Server 2016 |

## Run it

```bash
isoloom generate
cd .isoloom/vagrant && vagrant up
```

About 20 GB of memory (`isoloom resources`) plus 1 GB for the controller. Lab guide and
walkthroughs: the [GOAD documentation](https://orange-cyberdefense.github.io/GOAD/).

**Tested:** built end to end on VirtualBox (five Windows servers plus the controller), 0 failed
tasks across every play: the two forests, the child domain, the trusts, ACLs, IIS, MSSQL and SSMS
on both servers, and GOAD's vulnerabilities (including ADCS ESC roles).

## Changes from upstream GOAD

Fixes to GOAD's roles, found building it through Isoloom (see
[isoloom/goad](https://github.com/isoloom/goad)): the child domain promotion (error handling,
stale NTDS cleanup, DNS through the parent DC), Microsoft's permanent links for SQL Server 2019
Express, and SSMS 20 (the SSMS link now serves SSMS 21, which fails on Windows Server 2019).

## Licence

GPL-3.0, as GOAD ([LICENSE](LICENSE)). This lab is deliberately vulnerable: keep it isolated.
