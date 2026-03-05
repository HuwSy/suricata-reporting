# Suricata basic reports
This assumes suricata is setup to allow what is needed, block what is not and alert everything else which can get noisy. This is why it truncates fast log and cross checks dns requests from eve log in case of caching.

/etc/suricata/suricata.yaml
```
outputs:
  dns-log:
    enabled: yes
```
