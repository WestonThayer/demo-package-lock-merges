# demo-package-lock-merges

Demonstrates that it's unsafe to trust Git's auto merge of `package-lock.json` files.

1. In the [starting state](https://github.com/WestonThayer/demo-package-lock-merges/commit/887fa5dacb4055ec2b8c90289f61c695d234c129), `stripe@10.13.0` and `express@4.18.2` are installed. I choose those packages because they both share `qs` as a dependency, but that might not matter
2. Then I branched and switched express versions [express@3.19.0 #1](https://github.com/WestonThayer/demo-package-lock-merges/pull/1)
3. Then on a separate branch [stripe@7.4.0 #2](https://github.com/WestonThayer/demo-package-lock-merges/pull/2)
4. Merge PR #1
5. Resolve merge conflicts in PR #2, then merge

At this point `npm ci` fails: https://github.com/WestonThayer/demo-package-lock-merges/commit/945c0f05ccd8e46db7c1d756a3519a1c6ee957d7

I [fixed it](https://github.com/WestonThayer/demo-package-lock-merges/commit/8d6b944fe088aaca41fb4b28248de401bd609264) via

```
rm package-lock.json
npm install
```
