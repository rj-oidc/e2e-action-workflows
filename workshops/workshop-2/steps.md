# Security

## Code scanning

You can set up code scanning in any public repository where you have write access.

1. To the right of "code scanning alerts", click **Set up code scanning**. If code scanning is missing, you need to ask an organization owner or repository administrator to enable {% data variables.product.prodname_GH_advanced_security %}.{% endif %} For more information, see "[Managing security and analysis settings for your organization](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)" or "[Managing security and analysis settings for your repository](/github/administering-a-repository/managing-security-and-analysis-settings-for-your-repository)."
 !["Set up {% data variables.product.prodname_code_scanning %}" button to the right of "{% data variables.product.prodname_code_scanning_capc %}" in the Security Overview](/assets/images/help/security/overview-set-up-code-scanning.png)
4. Under "Get started with code scanning", click **Set up this workflow** on the CodeQL analysis workflow or on a third-party workflow.
 !["Set up this workflow" button under "Get started with {% data variables.product.prodname_code_scanning %}" heading](/assets/images/help/repository/code-scanning-set-up-this-workflow.png)Workflows are only displayed if they are relevant for the programming languages detected in the repository. The {% data variables.product.prodname_codeql_workflow %} is always displayed, but the "Set up this workflow" button is only enabled if {% data variables.product.prodname_codeql %} analysis supports the languages present in the repository.
5. To customize how code scanning scans your code, edit the workflow.

   Generally you can commit the {% data variables.product.prodname_codeql_workflow %} without making any changes to it. However, many of the third-party workflows require additional configuration, so read the comments in the workflow before committing.

   For more information, see "[Configuring {% data variables.product.prodname_code_scanning %}](/code-security/secure-coding/configuring-code-scanning)."
6. Use the **Start commit** drop-down, and type a commit message.
 ![Start commit](/assets/images/help/repository/start-commit-commit-new-file.png)
7. Choose whether you'd like to commit directly to the default branch, or create a new branch and start a pull request.
 ![Choose where to commit](/assets/images/help/repository/start-commit-choose-where-to-commit.png)
8. Click **Commit new file** or **Propose new file**.

In the default {% data variables.product.prodname_codeql_workflow %}, {% data variables.product.prodname_code_scanning %} is configured to analyze your code each time you either push a change to the default branch or any protected branches, or raise a pull request against the default branch. As a result, {% data variables.product.prodname_code_scanning %} will now commence.

The `on:pull_request` and `on:push` triggers for code scanning are each useful for different purposes. For more information, see "[Scanning pull requests](/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/configuring-code-scanning#scanning-pull-requests)" and "[Scanning on push](/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/configuring-code-scanning#scanning-on-push)."

## Container scan



## Secrets management

