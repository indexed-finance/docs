# `DelegateCallProxyOneToOne`

Upgradeable delegatecall proxy for a single contract.
This proxy stores an implementation address which can be
upgraded by the proxy manager.

# Controls

## `setImplementationAddress` 

```
function setImplementationAddress(
  address implementationAddress
)
```



Sets the implementation address the proxy should use. Must be called by the owner.

## `setOwnerAddress` 

```
function setOwnerAddress(address owner)
```

Sets the owner address.


