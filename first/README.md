## Getting started

Clone the Repository.  
Take a brief look at your `Makefile`. It's worthwhile to appreciate what it's actually doing  
Run `forge build` and `make`   
Then you might wanna look at coverage -> `forge coverage`  

By using the command `git checkout <commitHash>` we can assure our local repo is the correct version to be auditing.  

You should make a note of solc version they are using, for example it may be worth notable that why they are using solc version `0.7.6` or any other older.

## Static analysis tools

The most widely used tools for this purpose include [Slither](https://github.com/crytic/slither), developed by the Trail of Bits team, and a Rust-based tool developed by cyfrin known as [Aderyn](https://github.com/Cyfrin/aderyn).

> **_Note_**: It's important to remember that these tools should be run before going for an audit

#### Slither - A Python-Powered Static Analysis Tool
Slither tops the charts as the most popular and potentially the most potent static analysis tool available. Built using Python, it offers compatibility with both Solidity and Vyper developments. An open-source project, Slither allows developers to add plugins via PR.

The Slither repo provides instructions on installation and usage.

Running Slither
The Slither documentation outlines usage for us. Slither will automatically detect if the project is a Hardhat, Foundry, Dapp or Brownie framework and compile things accordingly.

In order to run slither on our current repo we just use the command:
```bash
slither .
```
This execution may take some time, depending on the size of the codebase.  

The output color codes potential issues:

* **Green** - Areas that are probably ok, may be informational findings, we may want to have a look

* **Yellow** - Potential issue detected, we should probably take a closer look

* **Red** - Significant issues detected that should absolutely be addressed.  

There will be times when codebase is large and Slither will output a lot of information, some information may not be relevant or we have already reviewed it, for these cases we can use `// slither-disable-next-line [DETECTOR_NAME]` to disable specific detectors on the next line of code.

```solidity
/// Example of slither disable next line

// slither-disable-next-line arbitrary-send-eth
(bool success,) = feeAddress.call{value: feesToWithdraw}("")

// slither-disable-next-line divide-before-multiply
uint256 fee = (amount * feeBps) / BPS_DENOMINATOR;

/// You can also disable multiple detectors in one line
// slither-disable-next-line reentrancy-no-eth, reentrancy-events
```

#### Aderyn: A Rust Based Static Analysis Tool

[Aderyn](https://github.com/Cyfrin/aderyn) requires `Rust` installed in your system.  
Once Rust has been installed, you can run the command cargo install Aderyn. This will install our tool.  

>**_Note_**: If you've already installed Aderyn, this command will also update you to the current version. Your terminal will advise if the tool is already installed.

Similar to Slither, aderyn can be run in desired directory as:

```bash
aderyn .
```
#### Others:
There are another tools like `Solidity Metrics`, it can be found in VSCode extensions, used to generate Complexity and Risk profile reports for projects written in solidity 

Another is also a VSCode extension `Solidity Visual Developer`, it provides syntax highlighting in your code based on variable types.

![tooling-svd4](images\tooling-svd4.png)

## DoS-Denial of service

This vulnerbaility can be perfectly explained by:

* [Quill Audits](https://www.quillaudits.com/blog/web3-security/denial-of-service-on-smart-contracts)

* [OWASP foundation](https://owasp.org/www-project-smart-contract-top-10/2025/en/src/SC10-denial-of-service.html)

## Reentrancy Attack

* [OWASP foundation](https://scs.owasp.org/sctop10/SC05-Reentrancy/)
* [sc-exploits-minimized](https://github.com/Cyfrin/sc-exploits-minimized/tree/main) for small example, also including how that particular vulnerability can be exploited

There's a [GitHub Repo](https://github.com/pcaversaccio/reentrancy-attacks) maintained by Pascal (legend) that catalogues re-entrancy attacks which have occurred. 

## Weak Randomness Overview

* [Medium Blog](https://medium.com/@ayushman2000/insecure-randomness-in-smart-contracts-7596a38e0624)

* [OWASP foundation](https://scs.owasp.org/SCWE/SCSVS-BLOCK/SCWE-024/)

* [sc-exploit-minimized](https://github.com/Cyfrin/sc-exploits-minimized)

## Arithmetic

* [sc-exploit-minimized](https://github.com/Cyfrin/sc-exploits-minimized)

>**_NOTE_**: In Solidity <0.8.0, ints & uints can overflow/underflow by default.
In 0.8.0+, these checks are automatic. Only when using unchecked can the old vulnerability reappear.

## Mishandling of ETH

* [sc-exploit-minimized](https://github.com/Cyfrin/sc-exploits-minimized)

**This is false:** without a `receive` or `fallback` function, the only way to send value to this contract is through the `deposit function`.


### Report Generating Template

* [audit-report-templating](https://github.com/Cyfrin/audit-report-templating) 

* [Portfolio-Ready-Report-Generator](https://github.com/Cyfrin/audit-repo-cloner)

* [Portfolio-Ready-Report-Generator-by-Spearbit](https://github.com/spearbit-audits/report-generator-template)
