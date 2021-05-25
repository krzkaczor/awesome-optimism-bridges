# Awesome Optimism Bridges

List of currently developed [optimism](https://optimism.io/) bridges.

**Optimism is an experimental tech and all bridges have some upgradeability patterns for now**

## DAI

[BellwoodStudios/optimism-dai-bridge](https://github.com/BellwoodStudios/optimism-dai-bridge)

### Key contracts

- [L1Gateway](https://github.com/BellwoodStudios/optimism-dai-bridge/blob/master/contracts/l1/L1Gateway.sol)
- [L1Escrow](https://github.com/BellwoodStudios/optimism-dai-bridge/blob/master/contracts/l1/L1Escrow.sol)
- [L2Gateway](https://github.com/BellwoodStudios/optimism-dai-bridge/blob/master/contracts/l2/L2Gateway.sol)
- [DAI](https://github.com/BellwoodStudios/optimism-dai-bridge/blob/master/contracts/l2/dai.sol)
- [L1GovernanceRelay](https://github.com/BellwoodStudios/optimism-dai-bridge/blob/master/contracts/l1/L1GovernanceRelay.sol) & [L2GovernanceRelay](https://github.com/BellwoodStudios/optimism-dai-bridge/blob/master/contracts/l2/L2GovernanceRelay.sol)

### Characteristics

- L2 DAI is separated from the bridge contracts
- On L1, funds are held in a shared escrow to make upgrades easy
- `GovernanceRelay` contract allows executing cross-chain governance spells
- Upgradeability fully controlled by the governance

## SNX

[Synthetixio/synthetix](https://github.com/Synthetixio/synthetix)

### Key contracts

- [SynthetixBridgeToOptimism (L1)](https://github.com/Synthetixio/synthetix/blob/develop/contracts/SynthetixBridgeToOptimism.sol)
- [SynthetixBridgeToBase (L2)](https://github.com/Synthetixio/synthetix/blob/develop/contracts/SynthetixBridgeToBase.sol)
- [SynthetixBridgeEscrow (L1)](https://github.com/Synthetixio/synthetix/blob/develop/contracts/SynthetixBridgeEscrow.sol)

### Characteristics

- L2 SNX is separated from the bridge contracts
- On L1, funds are held in a shared escrow to make upgrades easy
- Allows to [save](https://github.com/Synthetixio/synthetix/blob/develop/contracts/SynthetixBridgeToOptimism.sol#L98) tokens accidentally sent to escrow

## LINK

[smartcontractkit/LinkToken (PR)](https://github.com/smartcontractkit/LinkToken/pull/34/files)

### Key contracts

- [OVM_L1ERC20Gateway](https://github.com/smartcontractkit/LinkToken/pull/34/files#diff-dcbad446399bf9579b7db01cea75c9a48492fe2710f2ea3f7142368d1a397d2c)
- [OVM_L2ERC20Gateway](https://github.com/smartcontractkit/LinkToken/pull/34/files#diff-682db6e60f64f496e1d1b863d63921da1169eb7b5d32a6905da970597c579c1e)
- [OVM_EOACodeHashSet](https://github.com/smartcontractkit/LinkToken/pull/34/files#diff-72ee222f1be88e0683186a97543368a28d53f1fb8cf6943ee1f779c9f6090ec8)

### Characteristics

- L2 LINK is separated from the bridge contracts
- Transparent upgradeable proxy pattern is used for upgradeability
- On L1, funds stored are locked in the token bridge proxy (not in the escrow)
- Prevents withdrawing funds to the contract addresses. Checking for this on Optimism is not [trivial](https://github.com/smartcontractkit/LinkToken/pull/34/files#diff-72ee222f1be88e0683186a97543368a28d53f1fb8cf6943ee1f779c9f6090ec8).

## UniBridge

[Original Optimism PR](https://github.com/ethereum-optimism/contracts/pull/257)  
[Dedicated Repo](https://github.com/dmihal/unibridge)

### Key Contracts

- [L1TokenBridge](https://github.com/dmihal/unibridge/blob/master/contracts/l1/L1TokenBridge.sol)
- [L2TokenBridge](https://github.com/dmihal/unibridge/blob/master/contracts/l2/L2TokenBridge.sol)

### Characteristics

- Deposit any ERC20 token in the L1 bridge to mint on L2, preventing new bridge contract for each token
- Each L1 ERC20 gets a generic ERC20 and ERC777 counterpart. It gets created when a new token is being bridged for the first time
- Supports ERC20 or ERC777 on L2, with simple converstion between the two
- L1 bridge can calculate the address of L2 tokens using Create2

## Other

### Token Standard

Optimism team come up with a [Token Bridge Standard](https://ethereum-magicians.org/t/outlining-a-standard-interface-for-cross-domain-erc20-transfers/6151). Currently, it's still under discussion, and no bridges implement this interface.
