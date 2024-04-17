# Opening a pull request

*(for contributors)*

To add software to EESSI, you should go through the semi-automatic software installation procedure by:

* 1) Making a pull request to the [software-layer](https://github.com/EESSI/software-layer) repository
     to (add or) update an [easystack file](https://docs.easybuild.io/easystack-files) :books: that is used by
     [EasyBuild](https://docs.easybuild.io/) to install software;
* 2) Instructing the [bot :robot:](../bot.md) to build the software on all [supported CPU microarchitectures](../software_layer/cpu_targets.md);
* 3) Instructing the [bot :robot:](../bot.md) to deploy the built software for ingestion into the EESSI repository;
* 4) Merging the pull request once CI indicates that the software has been ingested. :white_check_mark:

!!! warning

    Make sure you are also aware of our [contribution policy](contribution_policy.md) when adding software to EESSI.

### Preparation

Before you can make a pull request to the [software-layer](https://github.com/EESSI/software-layer),
you should [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) the repository in your GitHub account.

For the remainder of these instructions, we assume that your GitHub account is `@koala` :koala:.

!!! note
    Don't forget to replace `koala` :koala: with the name of your GitHub account in the commands below!

1) Clone the [EESSI/software-layer](https://github.com/EESSI/software-layer) repository:

```
mkdir EESSI
cd EESSI
git clone https://github.com/EESSI/software-layer
cd software-layer
```

2) Add your fork :koala: as a [remote](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories)

```
git remote add koala git@github.com:koala/software-layer.git
```

3) Check out the branch that corresponds to the version of EESSI repository you want to add software to,
   for example `2023.06-software.eessi.io`:

```
git checkout 2023.06-software.eessi.io
```

!!! note
    The commands above only need to be run once, to prepare your setup for making pull requests.

### Creating a pull request {: #software_layer_pull_request }

1) Make sure that your `2023.06-software.eessi.io` branch in the checkout of the
  [`EESSI/software-layer`](https://github.com/EESSI/software-layer) repository is up-to-date

```
cd EESSI/software-layer
git checkout 2023.06-software.eessi.io 
git pull origin 2023.06-software.eessi.io 
```

2) Create a new branch (use a sensible name, not `example_branch` as below), and check it out

```shell
git checkout -b example_branch
```

3) Determine the correct easystack file to change, and add one or more lines to it that specify which
   easyconfigs should be installed

```shell
echo '  - example-1.2.3-GCC-12.3.0.eb' >> easystacks/software.eessi.io/2023.06/eessi-2023.06-eb-4.8.2-2023a.yml
```

4) Stage and commit the changes into your your branch with a sensible message

```shell
git add easystacks/software.eessi.io/2023.06/eessi-2023.06-eb-4.8.2-2023a.yml
git commit -m "{2023.06}[GCC/12.3.0] example 1.2.3"
```

5) Push your branch to your fork :koala: of the [software-layer](https://github.com/EESSI/software-layer) repository

```shell
git push koala example_branch
```

6) Go to the [GitHub web interface](https://github.com/EESSI/software-layer) to open your pull request,
   or use the helpful link that should show up in the output of the `git push` command.

   **Make sure you target the correct branch**: the one that corresponds to the version of EESSI you want to add
   software to (like `2023.06-software.eessi.io`).

   If all goes well, one or more bots :robot: should almost instantly create a comment in your pull request
   with an overview of how it is configured - you will need this information when providing build instructions.
