This repository contains google `repo` manifest files for the
verification repository collection.

To use, install the google `repo` tool from http://source.android.com/source/downloading.html#installing-repo

Then run the following commands:

    mkdir verification
    cd verification
    repo init -u https://github.com/seL4/verification-manifest.git
    repo sync
