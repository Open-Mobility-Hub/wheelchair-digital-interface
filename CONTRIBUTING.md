# How to Contribute

This project welcomes third-party contributions via pull requests.

You are welcome to propose and discuss enhancements using project issues.

Branching Policy: The latest tag on the main branch is considered stable. The main branch is the one where all contributions must be merged before being promoted to a tagged release. If you plan to propose a patch, please commit into its own feature branch.

All contributions must comply with the project's standards:

Every example / source file must refer to LICENSE
Every example / source file must include correct copyright notice

Depending on your language used it is expected you follow one of two syling guides
-
- Python use [PEP8](https://peps.python.org/pep-0008/) Standard
- C++ use [clang](https://clang.llvm.org/docs/ClangFormat.html) formatting 

Please familiarize yourself with the Apache License 2.0 before contributing.

## Adding additional features
If there are features you would like to see addressed / added to the WDI, please setup an issue in the [wheelchair-digital-interface repo](https://github.com/lucimobility/wheelchair-digital-interface) so that the proposal can be discussed.

## Fixes, clarifications, and cleanup
For changes that are in reference to examples or general information about how to use the API make a PRs directly in the [wheelchair-digital-interface repo](https://github.com/lucimobility/wheelchair-digital-interface).

To create a PR: 
- Fork the Project
- Create your Feature Branch (git checkout -b feature/AmazingUpdate)
- Commit your Changes (git commit -m 'Add some AmazingUpdate')
- Push to the Branch (git push origin feature/AmazingUpdate)
- Open a Pull Request

## Guidelines for Pull Requests
How to get your contributions merged smoothly and quickly.

- Create small PRs that are narrowly focused on addressing a single concern. Create multiple PRs to address different concerns.

- For speculative changes, consider opening an issue and discussing it first.

- Provide a good PR description as a record of what change is being made and why it was made. Link to a GitHub issue if it exists.

- If you are adding a new file, make sure it has the copyright message template at the top as a comment. You can copy over the message from an existing file and update the year.

- Unless your PR is trivial, you should expect there will be reviewer comments that you'll need to address before merging. We expect you to be reasonably responsive to those comments, otherwise the PR will be closed after 2-3 weeks of inactivity.

- Maintain clean commit history and use meaningful commit messages. PRs with messy commit history are difficult to review and won't be merged. Use rebase -i to curate your commit history.

- Keep your PR up to date with upstream/main (if there are merge conflicts, we can't really merge your change).

- Depending on the aggressiveness of a change reviewers may ask that you include unit tests to make sure there is a proper level of code coverage.

- Exceptions to the rules can be made if there's a compelling reason for doing so.
