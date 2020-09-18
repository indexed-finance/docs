# `DelegateCallProxyManyToOne`

Proxy contract which uses an implementation address shared with many
other proxies.

An implementation holder contract stores the upgradeable logic address, and
the proxy contract calls the implementation holder to execute each delegated
transaction.