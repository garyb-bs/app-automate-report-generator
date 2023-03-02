![BrowserStack Logo](https://d98b8t1nnulk5.cloudfront.net/production/images/layout/logo-header.png?1469004780)

# BrowserStack App Automate - Custom Report Generator

Custom HTML report generator for App Automate that will generate reports for builds run on the BrowserStack App Automate platform using the REST API.

## Prerequisites

-   Linux or MacOS operating system.
-   Ability to run bash scripts and `curl` command.
-   Permission to download and save logs.

## Setup

-   Download the script relevant to your operating system from the GitHub release section.
-   Run the following command to make sure you can run the scripts

    ```sh
    chmod +x ./reporter-app.sh
    # or
    chmod +x ./reporter-jenkins.sh
    ```

## How to find Build ID

On the BrowserStack App Automate [dashboard](https://app-automate.browserstack.com/dashboard/v2), click on your latest build and you can copy the build id from here:

![BuildID](https://i.imgur.com/tZ3FkY2.png)

## Input

1. Expected predefined Environment Variables

    ```sh
    export BROWSERSTACK_USERNAME=<username>
    export BROWSERSTACK_ACCESS_KEY=<access-key>
    ```

2. Command line arguments

    ```sh
    # when running locally
    BROWSERSTACK_BUILD_NAME="<build id that you used on BrowserStack>" ./reporter-linux.sh /report/path/you/want
    ```

## Jenkins Setup

To setup the report to be generated as part of a Jenkins pipeline, there are some extra steps required.

### Prerequisites

-   Access to a Jenkins setup
-   Permission to configure the pipeline that the report will be added to.
-   HTML Publisher [plugin](https://plugins.jenkins.io/htmlpublisher)

### Setup

You need to set up the HTML Publisher as a "Post build action" in your pipeline. This will make the report display as an item in the left navigation bar giving you easy access to it. It will look like this:

![HTML Publisher Plugin](https://i.imgur.com/DvfQqPK.png)

This is only one piece of it though. We still need to generate the report. For this we will add a build step. This <strong>must</strong> be done <strong>after</strong> the tests have been run so will likely always be your final build step. Example:

![Execute Shell](https://i.imgur.com/79UIG8t.png)

Once this is set up and you run a build, you should see a new item in your pipeline:

![Report](https://i.imgur.com/5vH3sZI.png)

This gives you easy access to the latest report from the root of your pipeline. The report should look like this:

![Report](https://i.imgur.com/PmbpiE6.png)