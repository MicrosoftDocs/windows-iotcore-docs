# Contributing to the Windows 10 IoT documentation

Thank you for your interest in our documentation. We appreciate your feedback, edits, additions and help with improving our docs. This page covers the basic steps and guidelines for contributing.

## Sign a CLA

If you want to contribute more than a couple lines and you're not a Microsoft employee, you need to [sign a Microsoft Contribution Licensing Agreement (CLA)](https://cla.microsoft.com/). 

## Proposing a change

To suggest a change to the docs, follow these steps:

1. If you're viewing the Docs.microsoft.com page, click the **Edit** button in the upper right of the page.  You will be redirected to the corresponding Markdown source file in the [GitHub repository](https://github.com/MicrosoftDocs/windows-iotcore-docs).  If you are already in the GitHub repo, you can just navigate to the source file that you would like to change.
2. If you don't already have a GitHub account, click **Sign Up** in the upper right and create a new account.
3. From the GitHub page you would like to change, click the pencil icon. 
4. Modify the file and use the preview tab to ensure the changes look good.
5. When you're done, commit your changes and open a pull request.

After you create the pull request, a member of the Windows 10 IoT team will review. If your request is accepted, updates are published to [https://docs.microsoft.com/windows/iot-core](https://docs.microsoft.com/en-us/windows/iot-core).

## Making more substantial changes

To make substantial changes to an existing article, add or change images, or contribute a new article, we recommend forking the repo into your GitHub account (click the "Fork" button in the top-right corner of the [GitHub repo](https://github.com/MicrosoftDocs/windows-iotcore-docs), and then creating a local clone (click the green "Clone or download" button, copy to your clipboard, then in your commandline enter `git clone <paste your repo clone link>`).

We also ask that before contributing a new article, to ask yourself the following questions...
* Have I included one, and only one, #-level title (equivalent to H1 in HTML)? 
* Is the verb tense (if applicable) in the title of my new article in the present tense and consistent with the other documentation?
* Is all of my grammar correct?
* Have I added my article - if contributing a new article - to the appropriate category as well as updated TOC.md?
* Have I properly formatted URLs to [look like this](https://github.com/MicrosoftDocs/windows-iotcore-docs/blob/master/CONTRIBUTING.md) instead of this: https://github.com/MicrosoftDocs/windows-iotcore-docs/blob/master/CONTRIBUTING.md
* Have you had at least two people review your new article?
* Have you contacted Sara (saclayt) or Namrata (namkedia) if you're unsure about anything?

When your new article does get accepted, we recommend the following:
* Share the article with your team! Don't hide your accomplishment - let your peers know.
* Follow the comments for your article by clicking the "Follow" button under the comment box. This way, you will stay updated on the comments your article may receive.

For more info, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/). Please note that we will not merge any PRs that are on the live branch. Please make sure you are submitting a PR to the master branch.

If you are unfamiliar with using Git, try the [Lynda.com Git Essentials training](https://www.lynda.com/Git-tutorials/Git-Essential-Training/100222-2.html).

## Authoring your contribution

Once you have forked and cloned the repo to your local machine, you can begin authoring with the text editor of your choice.  We, of course, recommend [Visual Studio Code](https://code.visualstudio.com/), a free lightweight open source editor from Microsoft. For help with markdown authoring, check out this [Markdown is FUN for Everyone! Poster](windows-iotcore/media/DocsMarkdownPoster.pdf) with all of the basics you need to know. You can even print it and hang it on your wall as a reminder to contribute. 

## Submitting your contribution and filing a Pull Request (PR)

Once you are ready to add your changes to the remote repo so that they will be staged for publishing, enter the following steps in the command line:
- `git status`: This command will show you what files you have changed so that you can confirm that you intended to make those changes. 
- `git add -A`: This command tells git to add ALL of your changes. If you would prefer to only add the changes you have made to one particular file, instead enter the command: `git add <file.md>`, where "file.md" represents the name the file containing your changes.
- `git commit -m “Fixed a few typos”`: This command tells git to commit the changes that you added in the previous step, along with a short message describing the changes that you made.
- `git push origin <yourbranchname>`: This command pushes your changes to the remote repo that you forked on GitHub (the "origin") into the branch that you have specified. Because you have forked the repo to your own GitHub account, you are welcome to do your work in the **Develop** branch. 

When you are happy with your changes and ready to submit a PR:
- Go to your fork of the IoT repo: https://github.com/your-github-alias/windows-iotcore-docs.
- Click the "New pull request" button. (The "base fork:" will be listed as "MicrosoftDocs/windows-iotcore-docs", the "head fork:" should show your fork of the repo and the branch in which you made your changes.) You can review your changes here as well. 
- Click the green "Create pull request" button. You will then be asked to give your Pull Request a title and description, then click the "Create pull request" button once more.

After pushing your contribution to the remote repo, you will be sent an email from *Open Publishing Build Service* informing whether your contribution built successfully and linking to any error warnings such as broken links, click the links to see your content staged on the site.

Once you have reviewed your contribution on the [Windows 10 IoT Docs staging site](https://review.docs.microsoft.com/en-us/windows/iot-core/) and are confident that you would like your changes to be published live, you must file a Pull Request (PR).

Once your PR is submitted, a member of the Windows 10 IoT docs team will review. When it is accepted, you will be able to view your changes on the [staging site](https://review.docs.microsoft.com/en-us/windows/iot-core). These updates will eventually be published live to [https://docs.microsoft.com/windows/iot-core](https://docs.microsoft.com/en-us/windows/iot-core).

## Working with Branches

The [Windows 10 IoT Docs GitHub repository](https://github.com/MicrosoftDocs/windows-iotcore-docs) utilizes two main parent branches: [Develop](https://github.com/MicrosoftDocs/windows-iotcore-docs/tree/develop), this content can be reviewed on the [staging site](https://review.docs.microsoft.com/en-us/windows/iot-core), and [Live](https://github.com/MicrosoftDocs/windows-iotcore-docs/tree/live), for content appearing on the [live site](https://docs.microsoft.com/en-us/windows/iot-core). 

When making contributions, please submit your Pull Request (PR) to the **Develop** branch. This branch can be viewed on the staging site and should only contain contributions that are ready to be published live.

## Using issues to provide feedback on IoT documentation

To provide feedback rather than directly modifying actual documentation pages, [create an issue](https://github.com/MicrosoftDocs/windows-iotcore-docs/issues).

Be sure to include the topic title and the URL for the page.

## Additional resources
- [Getting started with writing and formatting on GitHub](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

## Additional resources for Microsoft employees
- [Connect your GitHub account and MS alias](https://review.docs.microsoft.com/en-us/windows-authoring-guide/github-account#2-connect-your-github-account-and-ms-alias-on-the-microsoft-open-source-portal)
- [Resources for writing Markdown](https://review.docs.microsoft.com/en-us/windows-authoring-guide/writing-guidance/writing-markdown)
