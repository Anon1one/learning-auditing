## Git commands

When you do `git checkout <COMMIT_HASH>`, it takes you to the specified commit in that branch.    

After `git checkout` you can run `git branch` to acquire the ID of the hash commit. By running `git diff <COMMIT_ID> <BRANCH>` you'll receive an output of all the changed between the provided branch and the commit hash!

## Invariants

Most protocols are going to have some type of invariant, even something as simple as an ERC20 will have some condition which must always be true.

There's a great [repo by the Trail of Bits](https://github.com/crytic/properties) team that catalogs invariant/property examples for a number of tokens and Ethereum operations.

When running invariant test, you can edit the configuration in `foundry.toml`, configuration may includes:
```toml
[invariant]
runs = 64
depth = 32
fail_on_revert = true
```

It's important to understand these few settings.

* **runs** - how many fuzz tests will be performed with random data

* **depth** - how many random functions will be called per run

* **fail_on_revert** - this value determines if a test will fail as a product of reverted transactions.

for more configuration you have a reference: [foundry-book](https://getfoundry.sh/config/reference/testing/?highlight=%5Binvariant%5D#invariant).

There is great source for minimized exploits simulation/explanation for introductory purposes: [sc-exploits-minimized](https://github.com/Cyfrin/sc-exploits-minimized).

There's a great article on [Nascent.xyz](https://www.nascent.xyz/idea/youre-writing-require-statements-wrong), it covers the concept of having an invariant baked into the protocol design directly (sometimes called FREI-PI) and is actually something later versions of Uniswap actually do.

## Weird ERC20s
There's a great [GitHub Repo](https://github.com/d-xo/weird-erc20) that's been compiling examples of these types of tokens. 

There's a great [Token Integration Checklist by Trail of Bits](https://secure-contracts.com/development-guidelines/token_integration.html) that can serve has a great guideline for builders looking to avoid these types of exploits. In fact, [secure-contracts.com](https://secure-contracts.com/index.html) as a whole is a really invaluable resource you should check out.

