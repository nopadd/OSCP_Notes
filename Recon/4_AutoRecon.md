# Background
Super automated, full-featured scanner and enumerator that includes a lot of tools within (like Reconnoitre).

#Usage
```
python3 autorecon.py [IP] -vv
```

#Options
  - -h, --help 
  - --profile PROFILE: The port scanning profile to use (defined in port scan-profiles.toml). Default: default 
  - -o OUTPUT, --output OUTPUT: Defaults to the "results" directory.
  - --nmap NMAP: Override the {nmap_extra} variable in scans.
  - --nmap-append NMAP_APPEND: Append to the default {nmap_extra} variable in scans. 
  - -v, --verbose 
  - (none): Minimal output.  AutoRecon will announce when target scans start and finish, as well as which services were identified. 
  - --disable-sanity-checks: Disable sanity checks that would otherwise prevent the scans from running. 
