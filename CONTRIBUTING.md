# Contributing

Thank you for wanting to help.

1. Fork the repository and branch from `development`.
2. Open your pull request against `development`, never `main`. `main` holds releases only.
3. Run `bash check.sh` before you push. It is the only definition of green, and CI runs the same
   script. In the engine it asks that:
   - existing tests stay as they are: approved tests are locked. If you think one is wrong, open
     an issue naming the test and the line it proves, and say why. A changed test is made by the
     maintainer in a QA commit, and your pull request builds on it.
   - no comment carries a line or step number;
   - the code builds and passes `go vet`, the linter, the tests and `govulncheck`.
4. The files listed in `developer-owned-paths` are changed by the maintainer only.
5. Write your contribution from documentation and observed behavior. Do not copy code or text
   from other BBS software or its companions (transfer programs, door kits, terminals), and do not
   read their source to write a contribution.

Contributions are accepted under the repository's license.
