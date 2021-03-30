<!--
     Copyright 2018, Data61, CSIRO
     SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Manifest repository

This repository contains google `repo` manifest files for the
verification repository collection.

## Contents

The manifest files stored here come in three categories:

- `default.xml`: this manifest stores the latest tested-as-working combination
  of the seL4 code and proof repositories. It is updated automatically by CI jobs,
  points to specific revision hashes, and should generally not be modified manually.

- development manifests such as `devel.xml` and `mcs.xml`: these are for proof
  development and typically point to branch names of the verification
  repositories in combination with a fixed revision hash of the seL4 code
  repository. The seL4 revision in `devel.xml` is updated automatically by CI
  jobs for code changes in seL4 that are not visible to the proofs. It should be
  updated manually or using the [version bump][] script whenever proofs are
  updated in sync with the code. This will then trigger a CI run and, if
  successful, a corresponding update in `default.xml`.

- release version manifests such as `12.0.0.xml`: these store the repository
  version configuration for official releases of seL4. Use these to check proofs
  for release versions.

[version bump]: https://github.com/seL4/l4v/tree/master/misc/bump

## Use

To use, install the google `repo` tool from
<http://source.android.com/source/downloading.html#installing-repo>

Then, for the latest working version combination, run the following commands:

    mkdir verification
    cd verification
    repo init -u ssh://git@github.com/seL4/verification-manifest.git
    repo sync

If you do not have `ssh` access set up for github, you can also use

    repo init -u https://github.com/seL4/verification-manifest.git

For build instructions for the proofs, see the
[l4v/](https://github.com/seL4/l4v/) repository.

For build instructions for the binary verification, see the
[graph-refine/](https://github.com/seL4/graph-refine/) repository.

To set your repositories up for development, replace the `init` step with:

    repo init -m devel.xml -u ssh://git@github.com/seL4/verification-manifest.git

Similarly, if you are looking to use the proofs for a specific release version
of seL4, use the `-m` option to select the corresponding manifest file.
