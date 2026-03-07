# Suricata basic reports
This assumes suricata is setup to allow what is needed, block what is not and alert everything else which can get noisy. This is why it truncates fast log and cross checks dns requests from eve log in case of caching.

/etc/suricata/suricata.yaml
```
outputs:
  - fast:
      enabled: yes

  - dns-log:
      enabled: yes
```

/etc/suricata/suricata.yaml
```
vars:
  address-groups:
    allowed_ips: "/var/run/suricata-allowed-ips.list"
```

/etc/suricata/rules/local.rules
```
pass ip any any -> $allowed_ips any ( msg:"Allowed domain via DNS resolution"; sid:9900000; rev:1; )
```

cron
```
* * * * * /usr/sbin/suricata-allowed
```
