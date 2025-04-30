# azureml-components-mono
This mono repo is meant to contain Azure ML components. Each component is located in its own directory under the `components` directory. Each component has its own README file that describes the component and how to use it. The components are meant to be used in Azure ML pipelines.

# Directory Structure
The directory structure is as follows:
```
components/
├── my_eval
│   ├── my_eval.py
│   ├── my_eval.yaml
│   ├── README.md
│   └── requirements.txt
├── my_train
│   ├── my_train.py
│   ├── my_train.yaml
│   ├── README.md
│   └── requirements.txt


# Branching Strategy
This repository uses the trunk-based development branching strategy. The main branch is `main` and all development is done in feature branches. When a feature is complete, it is merged into the main branch. The main branch is always in a releasable state.

# Versioning
All components are versioned using semantic versioning. The version number is in the format `MAJOR.MINOR.PATCH`. The MAJOR version is incremented for breaking changes, the MINOR version is incremented for new features, and the PATCH version is incremented for bug fixes. The version number is stored in the `version` file in each component directory. 

# Conventional Commits
All commits must follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification. This means that all commit messages must be in the format `type(scope): subject`. The type can be one of the following:
- feat: A new feature
- fix: A bug fix
- feat: change input parameter format to JSON

BREAKING CHANGE: A breaking change
```

# Release pipeline
We are using release-please to automate the release process. As a contributor, you need to branch off the main branch and create a new feature branch. Once you have made your changes, you need to commit them and push them to the remote repository. You can then create a pull request (PR) from your feature branch to the main branch. The PR will be automatically built and tested using GitHub Actions.

The PR builds will lint the commits, runs the dummy tests and deploys the component to a specific Azure ML workspace. The version string corresponds to commit hash of the latest commit in the source branch. The version string is used to tag the release in the Azure ML workspace.

Once the checks are green, the PR can be merged to main. The release-please action is triggered on every push to the main branch. It will create a new release PR if there are any changes that need to be released. Once the release PR is merged to main, the release-please action will also create a new release on GitHub with the new version number. The workflow also has a job to publish the component on the shared registry ub Azure ML.