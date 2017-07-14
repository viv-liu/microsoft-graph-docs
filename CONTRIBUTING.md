# Contribute to Microsoft Graph documentation

Thank you for your interest in the Microsoft Graph documentation! Because the documentation is open source, anyone can contribute to help make our content better. Here are a few ways that you can help out:

* Fix bugs, grammar, or typos you find in the docs and submit a pull request.
* Fix open issues on our backlog from the [issues][] list by submitting a pull request.
* Report doc bugs by creating new [issues][].
* Request new documentation by describing what is needed in new [issues][].

## Doc repo structure

Before you contribute to the documentation, you'll need to understand how the repo folders are structured.

The docs are included in two folders: concepts, and API reference. The API reference folder includes subfolders for the beta and v1.0 reference content. 

```
root
--api-reference
  --beta
  --v1.0
--concepts
```

>**Important:** If you are making a change to a topic in the beta or v1.0 folder, determine wheter that change applies to the counterpart topic in the other folder, and update both topics if so.

If you're making changes to content in the api-reference folder, note that those topics follow a specific structure. In general, do not update the topic structure, but feel free to contribute to the content itself. 

## How do I contribute?

Follow these steps to make a change and submit a contribution to the docs.
1. **Fork the repo**. https://help.github.com/articles/fork-a-repo/
2. **[Clone the forked repo](https://help.github.com/articles/cloning-a-repository/)** to your computer. Note: You can actually [edit files directly on GitHub](https://help.github.com/articles/editing-files-in-your-repository/) and avoid cloning. But cloning makes edits easier if you are making large changes or changes to multiple files.
4. **Make your changes**. You can use any editor you choose. We like to use [Visual Studio Code](https://code.visualstudio.com/download). We use Markdown syntax; for more information, see [Markdown Home][].
5. **[Create a pull request (PR)](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)** from your fork to our original doc repo. 

## I created the PR, what happens next?

If the change is significant (more than just a typo fix), you'll be asked to sign a Contribution License Agreement (CLA). You only need to sign the CLA once; you won't be asked to sign again on future contributions. Please carefully review the document; you may also need to have your employer sign the document. After you sign, your PR will be reviewed by the docs team. We may ask you to make a few changes before we accept the PR. After we accept, we'll merge and publish your change.

We do our best to review pull requests within 10 business days.

## More resources

* If you are new to Markdown, see [Markdown Home][].
* If you get stuck using GitHub, see [GitHub Help][].

[GitHub Help]: http://help.github.com/
[Markdown Home]: http://daringfireball.net/projects/markdown/
[issues]: https://github.com/microsoftgraph/microsoft-graph-docs/issues
