# Fractionalized

This project was created for the Klaytn Covalent Unified Hackathon ’22 

https://www.covalenthq.com/blog/klaytn-unified-hackathon-winners/

~ demo UI has since been disabled, contracts remain available to use ~

## Background: 

Fractionalizing an NFT involves placing it inside a vault, where an arbitrary number of tokens are minted as a pegged 'fraction' representing it. This allows for shared ownership between multiple parties and a lower barrier to entry for high-value NFTs.

## Contracts:  

### Fractionalized.sol - main vault contract  

Mint a brand new KIP-37 (ERC1155) NFT to be fractionalized in the contract
```
function fractionalizeNative(string memory uri, uint256 supply, uint256 price)

uri - nft metadata 
supply - total number of fractions to be created from NFT
price - price per single fraction
```
Allow for an existing KIP-17 (ERC721) to be fractionalized
```
function fractionalizeImport(address nftAddress, uint256 supply, uint256 price)

nftAddress - the NFT address sent to the contract 
supply - total number of fractions to be created from NFT
price - price per single fraction
```
Vault Configuration Functions
```
function changeVaultName(string memory name)
function changeVaultInfo(string memory info)
function changeFractionPrice(uint256 price)
```
Burn unsold fractions inside vault 
```
function burnFractions(uint256 amount)
```
Withdraw NFT inside vault, only works if all existing fractions have been burned!
```
function withdrawNative(address to, uint256 id, uint256 amount)
function withdrawImported(address nft, address to, uint256 id)
```
Collect all revenue generated from fraction sales
```
function collectFunds() 
```
Purchase a number of available fractions from vault 
```
function buyFractions(uint256 amount) 
```

### Factory.sol - used in conjunction with the vault contract, can serve as a registry for deploying vaults and keeping track of them 

Create a new vault contract
```
function createFractionVault(string memory name, string memory description)
```
Check vaults deployed from factory  
```
function getAllUserVaults(address user) public view returns (FractionVault[] memory)
function getAllVaults() public view returns (FractionVault[] memory)
```
