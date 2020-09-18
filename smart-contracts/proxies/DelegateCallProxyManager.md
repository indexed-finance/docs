# `DelegateCallProxyManager`

Contract that manages deployment and upgrades of delegatecall proxies.

# Controls

## `setOwner` 

```
function setOwner(address owner)
```

Sets the owner address.

## `approveDeployer` 

```
function approveDeployer(address deployer)
```


Allows `deployer` to deploy many-to-one proxies.

## `revokeDeployerApproval` 

```
function revokeDeployerApproval(address deployer)
```


Prevents `deployer` from deploying many-to-one proxies.


# Implementation Management

## `createManyToOneProxyRelationship` 

```
function createManyToOneProxyRelationship(
  bytes32 implementationID,
  address implementationAddress
)
```



Creates a many-to-one proxy relationship.
Deploys an implementation holder contract which stores the
implementation address for many proxies. The implementation
address can be updated on the holder to change the runtime
code used by all its proxies.


## `setImplementationAddressManyToOne` 

```
function setImplementationAddressManyToOne(
  bytes32 implementationID,
  address implementationAddress
)
```



Updates the implementation address for a many-to-one
proxy relationship.


## `setImplementationAddressOneToOne` 

```
function setImplementationAddressOneToOne(
  address payable proxyAddress,
  address implementationAddress
)
```



Updates the implementation address for a one-to-one proxy.
Note: This could work for many-to-one as well if the caller
provides the implementation holder address in place of the
proxy address.

# Proxy Deployment

## `deployProxyOneToOne` 

```
function deployProxyOneToOne(
  bytes32 salt,
  address implementationAddress
)
```



Deploy a proxy contract with a one-to-one relationship
with its implementation.
The proxy will have its own implementation address which can
be updated by the proxy manager.


## `deployProxyManyToOne` 

```
function deployProxyManyToOne(
  bytes32 implementationID,
  bytes32 salt
) returns (address proxyAddress)
```

Deploy a proxy with a many-to-one relationship with its implemenation. The proxy will call the implementation holder for every transaction to determine the address to use in calls.

# Queries

## `getImplementationHolder` 

```
function getImplementationHolder() returns (address)
```

Queries the temporary storage value `_implementationHolder`.

This is used in the constructor of the many-to-one proxy contract so that the create2 address is static (adding constructor arguments would change the codehash) and the implementation holder can be stored as a constant.

## `getImplementationHolder` 

```
function getImplementationHolder(
  bytes32 implementationID
) returns (address)
```

Returns the address of the implementation holder contract for `implementationID`.

## `computeProxyAddressOneToOne` 

```
function computeProxyAddressOneToOne(
  bytes32 salt
) returns (address)
```

Computes the create2 address for a one-to-one proxy deployed with `salt` as the create2 address.

## `computeProxyAddressManyToOne` 

```
function computeProxyAddressManyToOne(
  bytes32 salt
) returns (address)
```

Computes the create2 address for a many-to-one proxy deployed with `salt` as the create2 salt.

## `computeHolderAddressManyToOne` 

```
function computeHolderAddressManyToOne(
  bytes32 implementationID
) returns (address)
```

Computes the create2 address of the implementation holder for `implementationID`.