---
name: screen-repo
description: Find every EVM address and every direct dependency in this repo and screen them with Prax in batches
---
1. Collect every distinct `0x[0-9a-fA-F]{40}` in the working tree (skip node_modules, .git, build output, lockfiles). Record file:line for each.
2. Screen them with `screen_wallets_batch` in chunks of 50 (chain eth unless the file context says otherwise).
3. Read the direct dependencies and pinned versions from package.json, requirements.txt, pyproject.toml, go.mod, Cargo.toml, pom.xml or Gemfile.lock, whichever exist. Screen them with `screen_packages` in chunks of 50.
4. Report two tables: address, where it appears, Prax band, label/story (short); and package, version, verdict, advisory ids, fixed version. Put block/critical first.
5. For anything critical: say which files reference it and ask before changing anything. For unknown contract addresses the code sends value to, recommend adding a `screen_transfer` pre-sign check. For a blocked package, propose the upgrade to the fixed version named by Prax and wait for confirmation.
