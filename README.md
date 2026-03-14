# Suricata basic reports and ip filtering
This assumes suricata is setup to allow what is needed, block what is not and alert everything else which can get noisy. 

## Reports
The reporting truncates fast log and cross checks dns requests from dns log in case of caching.

/etc/suricata/suricata.yaml
```
outputs:
  - fast:
      enabled: yes

  - dns-log:
      enabled: yes
```

## Rules
The rules also build ips to reduce logging

/etc/suricata/suricata.yaml
```
rule-files:
 - /var/lib/suricata-allowed-ips.rules
```

To auto generate variables for host, docker and containers etc
```
vars:
  address-groups: !include /var/lib/suricata-variables-docker.yaml
```

Run one of or on schedule via ./suricata-dns or to daemonise and update every approx 6 seconds (dependent on processing duration) via ./suricata-dns -d
