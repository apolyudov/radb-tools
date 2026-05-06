# radb-tools

Tools for IP-ASN-Country mapping.

- The ip-country script generates an ip-\<country code\>.lst file which contains all the IPv4 prefixes announced by the country's ASNs.
- The asn-country script generates an asn-\<country code\>.lst file which contains all the autonomous system numbers by the country.
  
## Installation

```bash
git clone --depth=1 git@github.com:furriest/radb-tools.git
cd ./radb-tools
./dbctl install
```

## Usage

Update databases
```bash
./dbctl pull_db
./dbctl update_ip
```

## License
[MIT](https://choosealicense.com/licenses/mit/)
