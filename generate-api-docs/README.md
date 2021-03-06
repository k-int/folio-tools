# Generate static API documentation from RAML files

## Prerequisites

- python (version 3 or higher)
- pip3 install pyyaml
- pip3 install requests
- pip3 install sh
- git
- yarn
- [raml2html v3](https://github.com/raml2html/raml2html) (old version 3, for RAML-0.8)
- [raml2html](https://github.com/raml2html/raml2html) (current version, for RAML-1.0)
- [raml2html-plain-theme](https://github.com/a7b0/raml2html-plain-theme) (for RAML-1.0 view-2) using our fork see package.json

See below for notes about installing those for [local use](#local-use).

## Method

This script is used by FOLIO CI infrastructure to generate [API documentation](https://dev.folio.org/reference/api/) for each [RAML-using](https://dev.folio.org/guides/commence-a-module/#back-end-ramls) back-end module.
(It is also available for [local use](#local-use)).

- On merge to master, Jenkins calls 'generate_api_docs.py -r repo_name'.
- Loads configuration data.
- For each RAML file, determine input RAML version,
  call the relevant version of 'raml2html'
  and generate html to output_directory.
- Deploy to AWS.

## Local use

Clone the folio-tools repository parallel to your back-end module repository and keep it up-to-date.

Install the prerequisites and keep them up-to-date by occasionally doing this:

```shell
cd $GH_FOLIO/folio-tools/generate-api-docs
rm yarn.lock
yarn install
pip3 install -r requirements.txt
```

From the top-level directory of your back-end module, run this script to generate local documentation.

```shell
cd $GH_FOLIO/mod-courses
python3 ../folio-tools/generate-api-docs/generate_api_docs.py -r mod-courses -l info
```

As the log messages indicate, the script discovered and processed RAML files from the "./ramls" directory.

Output files were generated to the default output directory.

There is also a version-numbered copy of the output files, mainly done for CI purposes
(see further [usage notes](https://dev.folio.org/reference/api/#usage-notes)).

See also [lint-raml](../lint-raml) for assessing your RAML and Schema files.

# Some relevant issues

[FOLIO-1253](https://issues.folio.org/browse/FOLIO-1253)
[FOLIO-589](https://issues.folio.org/browse/FOLIO-589)
[DMOD-88](https://issues.folio.org/browse/DMOD-88)
