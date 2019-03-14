---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-13"

keywords: functions cli, serverless, bluemix cli, install, functions plug-in

subcollection: cloud-functions-cli-plugin

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# {{site.data.keyword.openwhisk_short}} CLI plug-in
{: #cloudfunctions_cli}


{{site.data.keyword.openwhisk}} offers a powerful plug-in for the {{site.data.keyword.Bluemix_notm}} CLI that allows complete management of the {{site.data.keyword.openwhisk_short}} system. You can use {{site.data.keyword.openwhisk_short}} CLI plug-in to manage your code snippets in actions, create triggers and rules to enable your actions to respond to events, and bundle actions into packages. For more information about {{site.data.keyword.openwhisk_short}}, see the [documentation](/docs/openwhisk?topic=cloud-functions-cloudfunctions_cli).
{:shortdesc}

You can now use the alias `fn` in your {{site.data.keyword.openwhisk_short}} plug-in commands: `ibmcloud fn <command>`
{: tip}

## Setting up the {{site.data.keyword.openwhisk_short}} plug-in
{: #plugin_setup}

Download and install the {{site.data.keyword.openwhisk_short}} plug-in.
{: shortdesc}

1. Log in to the {{site.data.keyword.Bluemix_notm}} CLI. {{site.data.keyword.openwhisk_short}} is available in the US South, US East, Germany, and United Kingdom {{site.data.keyword.Bluemix_notm}} regions. If the {{site.data.keyword.Bluemix_notm}} API endpoint is not specified, specify one with the `-a` flag.

    * To log in to the US South region:
      ```
      ibmcloud login -a api.ng.bluemix.net
      ```
      {: pre}

    * To log in to the US East region:
      ```
      ibmcloud login -a api.us-east.bluemix.net
      ```
      {: pre}

    * To log in to the United Kingdom region:
      ```
      ibmcloud login -a api.eu-gb.bluemix.net
      ```
      {: pre}

    * To log in to the Germany region:
      ```
      ibmcloud login -a api.eu-de.bluemix.net
      ```
      {: pre}

2. Install the {{site.data.keyword.openwhisk_short}} plug-in.
    ```
    ibmcloud plugin install cloud-functions
    ```
    {: pre}

3. Verify that the plug-in is installed.
    ```
    ibmcloud plugin list cloud-functions
    ```
    {: pre}

    Output:
    ```
    Plugin Name          Version
    Cloud-Functions      1.0.16
    ```
    {: screen}

4. You can upgrade the {{site.data.keyword.openwhisk_short}} plug-in by running the following command:
    ```
    ibmcloud plugin update cloud-functions
    ```
    {: pre}

5. Before you can start working with {{site.data.keyword.openwhisk_short}} entities, you must [target a namespace](#target).

You can use the {{site.data.keyword.openwhisk_short}} CLI plug-in to:

* Run your code snippets, or actions, on {{site.data.keyword.openwhisk_short}}. See [Creating and invoking actions](/docs/openwhisk?topic=cloud-functions-openwhisk_actions).
* Use triggers and rules to enable your actions to respond to events. See [Creating triggers and rules](/docs/openwhisk?topic=cloud-functions-openwhisk_triggers).
* Learn how packages bundle actions and configure external events sources. See [Create and use packages](/docs/openwhisk?topic=cloud-functions-openwhisk_packages).
* Explore the catalog of packages and enhance your applications with external services, such as a [{{site.data.keyword.cloudant}} event source](/docs/openwhisk?topic=cloud-functions-openwhisk_cloudant).

To list of commands for the {{site.data.keyword.openwhisk_short}} plug-in, run `ibmcloud fn` with no arguments.
{: tip}

## Targeting a namespace
{: #target}

Before you can run commands by using the {{site.data.keyword.openwhisk_short}} CLI plug-in, you must target a namespace.

### Targeting an IAM-based namespace
{: #target_iam}

Target the resource group where you want to create the namespace. For example, target the `default` resource group.
```
ibmcloud target -g default
```
{: pre}

Then you can set your CLI context to an IAM-based namespace in that resource group.
```
ibmcloud fn property set --namespace <namespace_name_or_id>
```
{: pre}

### Targeting a Cloud Foundry-based namespace
{: #target_cf}

The default namespace, which can be denoted by an underscore (`_`) in some situations, corresponds to the Cloud Foundry-based namespace that is currently targeted.

When you log in to IBM Cloud, you can target a Cloud Foundry-based namespace by specifying the org and spaces in flags:
```
ibmcloud login -o <ORG> -s <SPACE>
```
{: pre}

If you are already logged in, you can run the `ibmcloud target` command in the {{site.data.keyword.Bluemix_notm}} CLI to switch organization and spaces. For example, to switch to the Cloud Foundry-based namespace `user@email.com_staging`:
```
ibmcloud target -r eu-gb -s staging
```
{: pre}

If an IAM-based namespace is targeted, first target a Cloud Foundry-based namespace by running the following command:
```
ibmcloud target -o <org> -s <space>
```
{: pre}

Then, you can unset the IAM-based namespaces by running the following command:
```
ibmcloud fn property unset --namespace
```
{: pre}

## Switching to different regions
{: #region_info}

If you are already logged in, you can run the `ibmcloud target` command in the {{site.data.keyword.Bluemix_notm}} CLI to switch regions.

{{site.data.keyword.openwhisk_short}} is available in the US South, US East, Germany, and United Kingdom {{site.data.keyword.Bluemix_notm}} regions. For example, to switch to the United Kingdom region:
```
ibmcloud target -r eu-gb
```
{: pre}

## Configuring the {{site.data.keyword.openwhisk_short}} CLI to use an HTTPS proxy
{: #cli_https_proxy}

The {{site.data.keyword.openwhisk_short}} CLI can be set  up to use an HTTPS proxy. To set up an HTTPS proxy, an environment variable that is called `HTTPS_PROXY` must be created. The variable must be set to the address of the HTTPS proxy, and its port by using the following format:
`{PROXY IP}:{PROXY PORT}`.

## Migrating from OpenWhisk CLI to {{site.data.keyword.openwhisk_short}} CLI plug-in
{: #cli_migration}

The {{site.data.keyword.openwhisk_short}} CLI plug-in replaces the OpenWhisk stand-alone CLI (`wsk`) for interacting with {{site.data.keyword.openwhisk_short}} entities in IBM Cloud. The `wsk` stand-alone CLI does not have the latest features supported by {{site.data.keyword.openwhisk_short}}, such as IAM-based namespace support and `service bind` support.

### Command Syntax
{: #command_syntax}

All `wsk` commands, except the `wsk bluemix login` command that is no longer needed, work the same way by using the command `ibmcloud fn`. All command options and arguments for commands in the Cloud Functions CLI plug-in are the same as the commands for the OpenWhisk stand-alone CLI. For more information, see the [Apache OpenWhisk CLI project ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/apache/incubator-openwhisk-cli).

### API Authentication and Host
{: #api_authentication}

The OpenWhisk CLI required you to configure the authentication API key and the API host. With the {{site.data.keyword.openwhisk_short}} CLI plug-in, you don't need to explicitly configure the API key and API host. Instead, you can log in and target your region with `ibmcloud login -a <region_api_endpoint>`. You can target an IAM-enabled namespace by running `ibmcloud fn property set --namespace NAME` or a Cloud Foundry-based namespace by running `ibmcloud target -o ORG -s SPACE`. After logging in, all commands begin with `ibmcloud fn`.

If you need to use the authentication API key for {{site.data.keyword.openwhisk_short}} in an external HTTP client such as cURL or Postman, you can retrieve it with the following commands:

To get the current API key:
```
ibmcloud fn property get --auth
```
{: pre}

To get the current API host:
```
ibmcloud fn property get --apihost
```
{: pre}

The API key is specific per region, organization, and space targeted by the {{site.data.keyword.openwhisk_short}} CLI plug-in.
{: tip}

### API Gateway authentication
{: #apigw_authentication}

The OpenWhisk CLI required you to run the `wsk bluemix login` to be able to configure the API Gateway authorization for management of your APIs by using the `wsk api` command. With the {{site.data.keyword.openwhisk_short}} CLI plug-in, you don't need to run `wsk bluemix login`. Instead, when you use the `ibmcloud login` command to log in to {{site.data.keyword.Bluemix_notm}}, the {{site.data.keyword.openwhisk}} plug-in automatically utilizes your current login and target information. Now you can manage your APIs by using the `ibmcloud fn api` command.

### Migrating deployment scripts
{: #migrating_deploy_scripts}

If you have scripts that use the OpenWhisk CLI with the `wsk` binary, all commands work the same way by using the command `ibmcloud fn`. You can modify your scripts to use the {{site.data.keyword.Bluemix_notm}} CLI plug-in, or create an alias or wrapper so that current commands using `wsk` are translated to `ibmcloud fn`. The `ibmcloud login` and `ibmcloud target` commands in the {{site.data.keyword.Bluemix_notm}} CLI work in unattended mode. With unattended mode, you can configure your environment before you run `ibmcloud fn` commands to deploy and manage your {{site.data.keyword.openwhisk_short}} entities.
