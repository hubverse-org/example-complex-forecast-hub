# Model metadata

The `model-metadata` folder contains files that describe the models used to 
generate hub submissions.

Every model must have corresponding metadata in this folder. 
The metadata file should be in 
[yaml format](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html). 
Here is an [example of a model metadata file](./MOBS-GLEAM_FLUH.yml).

When creating a new hub, administrators usually seed the `model-metadata` 
folder with a template that submitting teams can copy and update for their 
own models. Because some model metadata fields may be hub-specific, creators 
of the hub are encouraged to create their template by:

- adding the [Hubverse template model metadata file](https://hubverse.io/en/latest/user-guide/model-metadata.html#template-metadata-schema-file) to `model-metadata` 
- modifying the template model metadata file to include any hub-specific fields
- ensuring that the above changes are consistent with [Hubverse model metadata guidelines](https://hubverse.io/en/latest/format/model-metadata.html).


The instructions below provide detail about the [data
format](#Data-format) as well as [validation](#Data-validation) that
you can do prior to a pull request with a metadata file.

# Data format

## Required variables

This section describes each of the variables (keys) in the yaml document.
Please order the variables in this order.

### team_name
The name of your team that is less than 50 characters.

### team_abbr
The name of your team that is less than 16 characters.

### model_name
The name of your model that is less than 50 characters.

### model_abbr
An abbreviated name for your model that is less than 16 alphanumeric characters. 

### model_contributors

A list of all individuals involved in the forecasting effort.
A names, affiliations, and email address is required for each contributor. Individuals may also include an optional orcid identifiers.
All email addresses provided will be added to an email distribution list for model contributors.

The syntax of this field should be 
```
model_contributors: [
  {
    "name": "Modeler Name 1",
    "affiliation": "Institution Name 1",
    "email": "modeler1@example.com",
    "orcid": "1234-1234-1234-1234"
  },
  {
    "name": "Modeler Name 2",
    "affiliation": "Institution Name 2",
    "email": "modeler2@example.com",
    "orcid": "1234-1234-1234-1234"
  }
]
```

### license

We encourage teams to submit as a "cc-by-4.0" to allow the broadest possible uses, including private vaccine production (which would be excluded by the "cc-by-nc-4.0" license).
Otherwise, any one of the following [accepted licenses](https://github.com/cdcepi/FluSight-forecast-hub/blob/673e983fee54f3a21448071ac46a9f78d27dd164/hub-config/model-metadata-schema.json#L69-L75) can be used:
- ["CC0-1.0"](https://creativecommons.org/publicdomain/zero/1.0/deed.en): "The person who associated a work with this deed has dedicated the work to the public domain by waiving all of his or her rights to the work worldwide under copyright law, including all related and neighboring rights, to the extent allowed by law. You can copy, modify, distribute and perform the work, even for commercial purposes, all without asking permission."
- ["CC-BY-4.0"](https://creativecommons.org/licenses/by/4.0/deed.en): "You are free to: Share — copy and redistribute the material in any medium or format for any purpose, even commercially. Adapt — remix, transform, and build upon the material for any purpose, even commercially. The licensor cannot revoke these freedoms as long as you follow the license terms. Under the following terms: Attribution — You must give appropriate credit , provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use. No additional restrictions — You may not apply legal terms or technological measures that legally restrict others from doing anything the license permits."
- ["CC-BY_SA-4.0"](https://creativecommons.org/licenses/by-sa/4.0/deed.en): "You are free to: Share — copy and redistribute the material in any medium or format for any purpose, even commercially. Adapt — remix, transform, and build upon the material for any purpose, even commercially. The licensor cannot revoke these freedoms as long as you follow the license terms. Under the following terms: Attribution — You must give appropriate credit , provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use. ShareAlike — If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original. No additional restrictions — You may not apply legal terms or technological measures that legally restrict others from doing anything the license permits."
- ["PPDL"](https://opendatacommons.org/licenses/pddl/summary/): "You are free: To share: To copy, distribute and use the database. To create: To produce works from the database. To adapt: To modify, transform and build upon the database. The PDDL imposes no restrictions on your use of the PDDL licensed database."
- ["ODC-by"](https://opendatacommons.org/licenses/by/summary/): "You are free: To share: To copy, distribute and use the database. To create: To produce works from the database. To adapt: To modify, transform and build upon the database. As long as you: Attribute: You must attribute any public use of the database, or works produced from the database, in the manner specified in the license. For any use or redistribution of the database, or works produced from it, you must make clear to others the license of the database and keep intact any notices on the original database."
- ["ODbL"](https://opendatacommons.org/licenses/odbl/summary/): "You are free: To share: To copy, distribute and use the database. To create: To produce works from the database. To adapt: To modify, transform and build upon the database. As long as you: Attribute: You must attribute any public use of the database, or works produced from the database, in the manner specified in the ODbL. For any use or redistribution of the database, or works produced from it, you must make clear to others the license of the database and keep intact any notices on the original database. Share-Alike: If you publicly use any adapted version of this database, or works produced from an adapted database, you must also offer that adapted database under the ODbL. Keep open: If you redistribute the database, or an adapted version of it, then you may use technological measures that restrict the work (such as DRM) as long as you also redistribute a version without such measures."
- ["OGL-3.0"](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/): "You are free to: copy, publish, distribute and transmit the Information; adapt the Information; exploit the Information commercially and non-commercially for example, by combining it with other Information, or by including it in your own product or application. You must (where you do any of the above): acknowledge the source of the Information in your product or application by including or linking to any attribution statement specified by the Information Provider(s) and, where possible, provide a link to this licence."

### designated_model 

A team-specified boolean indicator (`true` or `false`) for whether the model should be considered eligible for inclusion in a Hub ensemble and public visualization. A team may specify up to two models as a designated_model for inclusion. Models which have a designated_model value of 'False' will still be included in internal forecasting hub evaluations.

### data_inputs

List or description of the data sources used to inform the model. Particularly those used beyond the target data of confirmed influenza hospital admissions.

### methods

A brief description of your forecasting methodology that is less than 200 
characters.

### methods_long

A full description of the methods used by this model. Among other details, this should include whether spatial correlation is considered and how the model accounts for uncertainty. If the model is modified, this field can also be used to provide the date of the modification and a description of the change.

### ensemble_of_models

A boolean value (`true` or `false`) that indicates whether a model is an ensemble of any separate component models.

### ensemble_of_hub_models

A boolean value (`true` or `false`) that indicates whether a model is an ensemble specifically of other models submited to the FluSight forecasting hub.

## Optional

### model_version
An identifier of the version of the model

### website_url

A url to a website that has additional data about your model. 
We encourage teams to submit the most user-friendly version of your 
model, e.g. a dashboard, or similar, that displays your model forecasts. 

### repo_url

A github (or similar) repository url containing code for the model. 

### citation

One or more citations to manuscripts or preprints with additional model details. For example, "Gibson GC , Reich NG , Sheldon D. Real-time mechanistic bayesian forecasts of Covid-19 mortality. medRxiv. 2020. https://doi.org/10.1101/2020.12.22.20248736".

### team_funding 

Any information about funding source(s) for the team or members of the team that would be natural to include on any resulting FluSight publications. For example, "National Institutes of General Medical Sciences (R01GM123456). The content is solely the responsibility of the authors and does not necessarily represent the official views of NIGMS."

# Data validation

Optionally, you may validate a model metadata file locally before submitting it to the hub in a pull request. Note that this is not required, since the validations will also run on the pull request. To run the validations locally, follow these steps:

1. Create a fork of the `FluSight-forecast-hub` repository and then clone the fork to your computer.
2. Create a draft of the model metadata file for your model and place it in the `model-metadata` folder of this clone.
3. Install the hubValidations package for R by running the following command from within an R session:
``` r
remotes::install_github("Infectious-Disease-Modeling-Hubs/hubValidations")
```
4. Validate your draft metadata file by running the following command in an R session:
``` r
hubValidations::validate_model_metadata(
    hub_path="<path to your clone of the hub repository>",
    file_path="<name of your metadata file>")
```

For example, if your working directory is the root of the hub repository, you can use a command similar to the following:
``` r
hubValidations::validate_model_metadata(hub_path=".", file_path="UMass-trends_ensemble.yml")
```

If all is well, you should see output similar to the following:
```
✔ model-metadata-schema.json: File exists at path hub-config/model-metadata-schema.json.
✔ UMass-trends_ensemble.yml: File exists at path model-metadata/UMass-trends_ensemble.yml.
✔ UMass-trends_ensemble.yml: Metadata file extension is "yml" or "yaml".
✔ UMass-trends_ensemble.yml: Metadata file directory name matches "model-metadata".
✔ UMass-trends_ensemble.yml: Metadata file contents are consistent with schema specifications.
✔ UMass-trends_ensemble.yml: Metadata file name matches the `model_id` specified within the metadata file.
```

If there are any errors, you will see a message describing the problem.
