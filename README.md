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

### Download and convert_rib databases

```bash
./dbctl pull_db              # Download ASN database + RIB archive and convert_rib (all three phases)
./dbctl pull_db --force      # Same, but re-download/re-convert_rib even if files are current

./dbctl pull_asn             # Download ASN database from RIPE (wget -N, skips if unchanged)
./dbctl pull_rib             # Download latest RIB archive from RouteViews (resumes partial downloads)
./dbctl convert_rib              # Convert RIB archive to ipasn.dat format
```

Each phase is idempotent:
- `pull_asn` uses `wget -N` (timestamping) — only downloads if server file is newer
- `pull_rib` keeps partial files on interrupt; resumes with `wget -c` on re-run; skips if local file passes `bzip2 -t`
- `convert_rib` skips if ipasn.dat header already references the local rib file

Add `--force` or `-f` to any phase to bypass skip logic.

### Generate country IP/ASN lists

```bash
./dbctl update_ip            # Generate ip_RU.lst and asn_RU.lst
./dbctl update_ip CN         # Generate ip_CN.lst and asn_CN.lst
./dbctl merge_ip RU CN       # Merge into ip_allow.lst (sorted, aggregated)
```

### Cleanup

```bash
./dbctl clean                # Remove all generated files, backups, and rib archives
```

## License
[MIT](https://choosealicense.com/licenses/mit/)
