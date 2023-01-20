[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)
[![lint](https://github.com/Rosa-Luxemburgstiftung-Berlin/ansible-role-unbound/actions/workflows/lint.yml/badge.svg)](https://github.com/Rosa-Luxemburgstiftung-Berlin/ansible-role-unbound/actions?query=workflow%3Aansible-lint)
[![test](https://github.com/Rosa-Luxemburgstiftung-Berlin/ansible-role-unbound/actions/workflows/molecule.yml/badge.svg)](https://github.com/Rosa-Luxemburgstiftung-Berlin/ansible-role-unbound/actions/workflows/molecule.yml)

# ansible-role-unbound aka. rls.unbound
Install [unbound](https://github.com/NLnetLabs/unbound) on debian based systems
and extend it optionally by using one or more __dnsbl__ lists.

## Role Variables

[defaults/main.yml](defaults/main.yml)

### Example
```yaml
undbound_config:
  server:
    interface-automatic: "yes"
    verbosity: 1
    log-queries: "yes"
    log-replies: "yes"
    log-local-actions: "yes"
    log-servfail: "yes"
    access-control: 0.0.0.0/0 allow
    # can be written too as
    # access-control:
    #   - 0.0.0.0/0 allow
    do-ip6: "no"
    do-udp: "yes"
    do-tcp: "yes"
    so-reuseport: "yes"
    module-config: iterator
    cache-max-ttl: 86400
    cache-min-ttl: 0
    serve-expired: "yes"
    outgoing-num-tcp: 10
    incoming-num-tcp: 10
    root-hints: /usr/share/dns/root.hints
    auto-trust-anchor-file: /usr/share/dns/root.key
    harden-glue: "yes"
    harden-dnssec-stripped: "yes"
    use-caps-for-id: "yes"
    prefetch: "yes"
    local-zone:
      - '"test.github.com" transparent'
    local-data:
      - "'test.github.com A 10.10.10.10'"
    domain-insecure:
      - test.github.com
    private-domain:
      - test.github.com
  forward-zone:
    name: github.com
    forward-addr:
      - 1.1.1.1
      - 9.9.9.9

dnsbl_lists:
  - https://blocklistproject.github.io/Lists/alt-version/abuse-nl.txt
```

### Some Resources Related to DNSBL

  * https://blocklistproject.github.io/Lists/#versions
  * https://justdomains.github.io/blocklists/#using-with-pi-hole
  * https://crazymax.dev/WindowsSpyBlocker/blocking-rules/
  * https://github.com/StevenBlack/hosts
  * https://github.com/AdAway/AdAway/wiki/HostsSources
  * https://oisd.nl/
