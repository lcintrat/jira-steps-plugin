+++
title = "UserSearch"
description = "More about jiraUserSearch step."
tags = ["steps", "user"]
weight = 1
date = "2017-11-12"
lastmodifierdisplayname = "Naresh Rayapati"
+++

### jiraUserSearch

This step searches users by name, username or email address form the JIRA SITE.

#### Input

* **queryStr** - name, username or email address. (partial string are allowed)
* **site** - Optional, default: `JIRA_SITE` environment variable.
* **failOnError** - Optional. default: `true`.

{{% notice note %}}
It supports all the fields that any jira instance supports including custom fields. For more information about all available input fields, please refer to the [JIRA API documentation](https://docs.atlassian.com/jira/REST/) depending on your JIRA version.
{{% /notice %}}

#### Output

* Each step generates generic output, please refer to this [link]({{%relref "getting-started/config/common.md"%}}) for more information.
* The api response of this jira_user_search step can be reused later in your script by doing `response.data.required_field_name`.
* You can see some example scenarios [here]({{%relref "getting-started/examples"%}})
* All the available fields for a jira response can be found in [JIRA API documentation](https://docs.atlassian.com/jira/REST/) depending on your JIRA version.

{{% notice note %}}
`response.data` returns all the fields returned by JIRA API.
{{% /notice %}}

#### Examples

* With default [site]({{%relref "getting-started/config/common.md#global-environment-variables"%}}) from global variables.

    ```groovy
    node {
      stage('JIRA') {
        // where jenkins is actual username
        def users = jiraUserSearch queryStr: 'jenk'
        echo users.data.toString()
      }
    }
    ```
* `withEnv` to override the default site (or if there is not global site)

    ```groovy
    node {
      stage('JIRA') {
        withEnv(['JIRA_SITE=LOCAL']) {
          // where Naresh Rayapati is actual name.
          def users = jiraUserSearch queryStr: 'Nare'
          echo users.data.toString()
        }
      }
    }
    ```
* Without environment variables.

    ```groovy
    def users = jiraUserSearch queryStr: 'jenkins@thoughtslive.org', site: 'LOCAL', failOnError: true
    echo users.data.toString()
    ```
