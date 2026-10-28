# Test Plan — VPN Kill Switch

## Scope

Authorized testing on the owner's Linux laboratory only.

## Completed observations

- nftables syntax validation succeeded.
- Kill Switch service was active after reboot.
- Firewall table was present after reboot.
- IPv4 and IPv6 routes used the VPN interface.
- Direct IPv4 and IPv6 connection attempts timed out.
- Firewall drop counters increased during direct connection attempts.
- A direct DNS query test timed out.

## Required follow-up

- Capture packets during boot and VPN reconnection.
- Test VPN failure and recovery in a controlled maintenance window.
- Verify DNS behavior with packet capture.
- Review IPv6, interface changes, and routing edge cases.
- Review systemd dependency and failure behavior.

## Evidence handling

Do not store raw command output, real IP addresses, private keys,
tokens, VPN endpoint details, Wi-Fi identifiers, or unredacted logs.
Record only sanitized observations and test conclusions.
