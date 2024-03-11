---
slug: connect-scm 
title: Connect a source code manager
hide_title: true
description: Connect a GitHub or GitLab organization to manage user authentication.
tags:
  - Semgrep Cloud Platform
  - Team & Enterprise Tier
  - Deployment
---

# Connect a source code manager

:::note Your deployment journey
- You have gained the necessary [resource access and permissions](/deployment/checklist) required for deployment.
- You have [created a Semgrep account and organization](/deployment/create-account-and-orgs). 
:::

Linking a source code manager provides the following benefits:

- Allows the Semgrep org membership to be managed by GitHub or GitLab.
- For GitHub users:
    - Provides Semgrep access to post PR or MR comments.
    - For GitHub Actions users: Enables you to add a Semgrep CI job to repositories in bulk.

You can only connect your Semgrep organization to the source code manager that you originally logged in with. If your organization uses both GitHub and GitLab to manage source code, log in with the source code manager that you would prefer to use to manage Semgrep org membership. You can still scan repositories from other sources.

The process to connect a source code manager depends on whether your SCM tool is cloud-hosted by the service provider, hosted on-premise, or hosted as a single-tenant by the service provider.

## Connect to cloud-hosted orgs

### GitHub Cloud

1. Sign in to Semgrep Cloud Platform.
1. On the sidebar, click **the organization account** you want to make a connection for.
1. Click **Settings** > **Source Code Managers**.
![Source code manager tab](/img/source-code-manager.png#md-width)
1. Click **Connect to GitHub**.
1. Review the permissions requested by Semgrep, then click **Continue**.
1. Click the organization you want to install Semgrep on.
1. Choose to authorize and install Semgrep for **<i class="fa-regular fa-circle-dot"></i> All repositories** or **<i class="fa-regular fa-circle-dot"></i> Only select repositories**.
1. Click **Install and authorize**.
1. After a successful link, you are signed out of Semgrep Cloud Platform automatically, as your credentials have changed after linking an organization.
1. Sign back in to Semgrep Cloud Platform.

<!-- Steps reverted to old flow and checked on Feb 21 2024
NOTE. As of Feb 21, the SCM steps don't always match what is in the docs. I got both old and new flows as of Feb
21, 2024, depending on the age of my org. Fortunately the "old" flow successfully went through Install and Authorize.
-->


<!-- removed temporarily because we're using the "old flow"
:::tip
- Getting Assistant recommendations grants Semgrep **code access**.
- **Leave PR comments** refers to Semgrep's capability to post findings to developers in PRs.
:::

-->

You have successfully connected an org in Semgrep Cloud Platform with an organization in your source code management tool.

### GitLab Cloud

For users of GitLab cloud-hosted plans, a connection to GitLab is created automatically after [adding a Semgrep job to GitLab CI/CD](/deployment/add-semgrep-to-ci/). No other steps are needed.

## Connect to on-premise GitHub or GitLab orgs

### Applicable plans

| GitHub | GitLab |
| ------ | ------ |
| GitHub Enterprise Server       | Any GitLab Self Managed plan        |

### Table of required scopes for PATs

Semgrep Cloud Platform requires personal access tokens (PATs) with assigned scopes. These scopes grant necessary permissions to the PAT and vary depending on the user's plan.

| GitHub Enterprise Server          | GitLab Self-Managed        |
|:---------------------------|:---------------------------|
| <ul><li>`public_repo`</li> <li>`repo:status`</li> <li>`user:email`</li> <li>`write:discussion`</li></ul> | `api` |

### Make the connection

Integrate Semgrep into these custom source code management (SCM) tools by following the steps below:

1. Sign in to [Semgrep Cloud Platform](https://semgrep.dev/login).
2. Click **Settings** > **Source Code Managers**.
![Source code manager tab](/img/source-code-manager.png#md-width)
3. Select your source code manager.
4. For **GitHub Enterprise Server**, follow these steps:
    1. Create a PAT by following the steps outlined in this [guide to creating a PAT](https://docs.github.com/en/enterprise-server@3.1/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). Ensure that the PAT is **[created with the required scopes](#table-of-required-scopes-for-pats)**.
    2. Return to Semgrep Cloud Platform and enter the personal access token generated into the **Access token** field.
    3. Enter your GHE Server base URL into the **URL** field.
    4. Ensure that your SCM integration successfully detects repositories by setting up a CI job for any repository you want to scan:
        1. Commit a `semgrep.yml` configuration file into the `.github/workflows` folder. Refer to [Sample CI configurations](/docs/semgrep-ci/sample-ci-configs#github-actions) for a template you can copy and customize. 
        2. The CI job starts automatically to establish a connection with Semgrep Cloud Platform. Upon establishing a connection, your repository appears in **Semgrep Cloud Platform > [Projects](https://semgrep.dev/orgs/-/projects)** page.
5. For **GitLab Self Managed**, follow these steps:
    1. Create a PAT by following the steps outlined in this [guide to creating a PAT](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html). Ensure that the PAT is **[created with the required scopes](../scm/#table-of-required-scopes-for-pats)**.
    2. Return to Semgrep Cloud Platform and enter the personal access token generated into the **Access token** field.
    3. Enter your GLSM base URL into the **URL** field.
    4. Ensure that your SCM integration successfully detects repositories by setting up a CI job for any repository you want to scan:
        1. Create or edit your `.gitlab-ci.yml` configuration file to add Semgrep as part of your GitLab CI/CD pipeline. Refer to [Sample CI configurations](/docs/semgrep-ci/sample-ci-configs#gitlab-cicd) for a template you can copy and customize.
        2. Commit the updated `.gitlab-ci.yml` file.
        3. The CI job starts automatically to establish a connection with Semgrep Cloud Platform. Alternatively, if it does not start automatically, start the job from the GitLab CI/CD interface. Upon establishing a connection, your repository appears in **Semgrep Cloud Platform > [Projects](https://semgrep.dev/orgs/-/projects)** page.

## Connect to GitHub Enterprise orgs

The Semgrep App for GitHub Enterprise (GHE) creates a connection between Semgrep
and orgs in your GHE deployment. It allows you to get Semgrep results as PR
comments, add Semgrep to your projects with one click, and manage rules and
results across multiple projects from one centralized place.

This article walks you through installing the Semgrep App for use with GHE
deployments. There are two primary installation steps:

1. Install the Semgrep App for the first time using the GHE organization (org)
   that "owns" the app.
2. Install the app for additional GHE orgs.

<!-->Using HTML headers instead of MD headers because I don't want them in the right-side nav<-->
<h3>Install the Semgrep App for the first time using the organization that "owns" the app</h3>

When you install the Semgrep App for GHE for the first time in your GHE
instance, you must choose the organization within your deployment to act as the
owner of the app. As the owner, this GHE org controls the settings and
permissions granted to the app.

1. Log in to [Semgrep Cloud Platform](https://semgrep.dev/login/).
2. Go to **Settings** > **Source Code Managers**, and click **Add GitHub
   Enterprise**.
   ![Semgrep Cloud Platform's Source code managers page](/img/ghe-1.png#md-width)
3. In the popup window, provide:
   - The **Name of your GitHub Organization**
   - The **URL** to access your deployment
   - A random string in the **Access token** field; this field will be optional in the future
    Click **Connect** to save your changes.
   ![Connect your GitHub Organization popup window](/img/ghe-2.png#md-width)
4. Refresh your browser. You should see a new entry under **Source code
   managers** that displays the GHE org and instance URL you entered. Click
   **Create App**.
   ![Semgrep Cloud Platform's Source code managers page with new GHE instance](/img/ghe-3.png#md-width)
5. In the popup window:
   1. Ensure that:
      - You've selected **Organization**
      - The **GitHub Organization name** is populated (if not, enter the name of
        your org)
      - You've selected the **Use for multiple GitHub orgs (Enterprise-public
        app)** checkbox
      ![Popup window to provide GitHub org information](/img/ghe-4.png#md-width)
   2. Review the permissions for the app; as the app owner, note that you can
   change these permissions later. Click **Create GitHub App** to proceed.
   3. Click **Create GitHub App** to proceed.
      ![Create private Semgrep GitHub App popup with option to create app](/img/ghe-5.png#md-width)
      If this step is successful, the blue **Create GitHub App** button turns into a gray **Created** button.
      ![Create private Semgrep GitHub App popup showing that an app has been created](/img/ghe-6.png#md-width)
6. Click **Install** under **Step 4**. You'll be taken to your GHE instance and
   asked to name your app. You can choose whatever name you'd like, but Semgrep
   recommends that you name it something that indicates that this is the Semgrep
   GHE app.
7. After you name your app, choose the GHE org to which you want it installed.
   Select the org that you want to act as the owner of the app, and click
   **Install**.
   ![List of orgs to which the Semgrep app can be installed](/img/ghe-7.png#md-width)
8. Wait for the installation to complete. When done, you will be redirected to
   Semgrep.
9. Verify the installation by navigating to **Settings** > **Source Code
   Managers**. Ensure that the entry for your SCM shows a gray **Installed**
   button.
   ![Semgrep Cloud Platform's Source code managers list showing GHE instance](/img/ghe-8.png#md-width)
10. In GHE, you should see the app listed as installed on the **GitHub Apps**
   page.
   ![GHE showing installed Semgrep App](/img/ghe-9.png#md-width)
   You can click **Configure** to choose the repositories to which the app
   has access. Additionally, you can go to **App settings** to customize the
   permissions granted to the app.
   ![GitHub Apps page showing App settings link](/img/ghe-10.png#md-width)

At this point, you've successfully installed the GHE Semgrep App on the owner GHE org. In the future, other members of your GHE instance can install the app on their GHE orgs using the public link if they have the proper permissions. You can get the public link from GHE by going to **GitHub Apps** > **App settings**.

![App installation page](/img/ghe-11.png#md-width)

<!-->Using HTML headers instead of MD headers because I don't want them in the right-side nav<-->
<h3>Install the app for subsequent GHE org</h3>

You can install the Semgrep app onto additional GHE orgs at any time. To do so:

1. Go to the public link for the app shared with you by your admin. Click **Install**.
   ![App installation page](/img/ghe-12.png#md-width)
2. Choose the GHE org to which you want the app installed, and click **Install**.
   ![Org list](/img/ghe-13.png#md-width)
3. In the popup confirmation message, click **Install**.
   ![GitHub installation prompt](/img/ghe-14.png#md-width)
4. The GHE org should now be listed under **Source code organizations**.
    ![Source code organizations list](/img/ghe-15.png#md-width)

## Next steps

- Optional: If you want to set up SSO to manage your users, see [<i class="fa-regular fa-file-lines"></i> SSO authentication](/deployment/sso).
- You are ready to start your first remote scan.


<!--

New workflow steps

1. For GitHub users, click **Connect to GitHub**. You are taken to the connection page. Enter the following information:
    1. Click the **Install on** drop-down box and select the account type you are connecting to, either a GitHub **personal account** or **organization account**.
    1. Under **Organization name**, enter the name of the GitHub account to link to. The name must be an exact match.
    1. Choose to **<i class="fa-regular fa-circle-dot"></i> Leave PR comments and get Assistant recommendations** or **<i class="fa-regular fa-circle-dot"></i> Leave PR comments**.
    1. Optional: Click Review permissions to view the permissions granted to Semgrep.
    1. Click **Create GitHub App**.
    1. Click **Install**. 

-->    
