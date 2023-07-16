
Extension over standard wireguard setup tool

Changes:

1. Configuration format extended
wg0.conf format extened, for peer two more keys available:
- configure static routes that should installed instead of Allowed-Ips:
```
    Routes = [<prefix1>[,<prefix2>...]]
```
- routes that should be installed by wg-dynamic-routes scrip if peer available:
```
    DynamicRoutes = [<prefix1>[,<prefix2>...]]
```

2. Update to wg-quick script
   **wg-quick** script will install Routes=  into FIB, if specified, unlike old behaviour
   it is allowed to specify empty list to do not install any routes


3.  Peer status tracking daemon

    **wg-dynamic-routes** daemon tracks peer status, and
    - if peer gets online (latest-handshake <= 180s) - install these routes
    - if peer gets offline (latest-handshake > 180s) - remove these routes