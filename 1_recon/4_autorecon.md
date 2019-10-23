# 3: AutoRecon

## Background

Super automated, full-featured scanner and enumerator that includes a lot of tools within \(like Reconnoitre\).

## Usage

```python
python3 autorecon.py [IP] -vv
```

## Options

* -h, --help 
* --profile PROFILE: The port scanning profile to use \(defined in port scan-profiles.toml\). Default: default 
* -o OUTPUT, --output OUTPUT: Defaults to the "results" directory.
* --nmap NMAP: Override the {nmap\_extra} variable in scans.
* --nmap-append NMAP\_APPEND: Append to the default {nmap\_extra} variable in scans. 
* -v, --verbose 
* \(none\): Minimal output.  AutoRecon will announce when target scans start and finish, as well as which services were identified. 
* --disable-sanity-checks: Disable sanity checks that would otherwise prevent the scans from running. 

