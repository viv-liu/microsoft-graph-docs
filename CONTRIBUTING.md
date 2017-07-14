# Contribute to Microsoft Graph documentation

Thank you for your interest in the Microsoft Graph documentation! The documentation is open source and anyone can contribute and help make the docs better and more comprehensive. Here are a few ways you can help out with this repo.

* Fix bugs, grammar, or typos you find in the docs.
* Fix issues other people have logged in the [issues][] list.
* Report doc bugs by creating new [issues][].
* Request new documentation by describing what is needed in new [issues][].

## Doc repo structure
Before you contribute to the documentation, you'll need to understand how the repo folders are structured.

The docs are split into two main sections: concepts, and API reference. There are two main folders that contain these docs. The API reference is further split into beta and v1.0 sections. You can see this breakout on the web site as well.
```
root
--api-reference
  --beta
  --v1.0
--concepts
```

**Important:** If you are making a change to a beta or v1.0 topic, check to see if that same change applies to the counterpart topic as well.

When making changes to API reference, there is a specific structure each article follows with sections for Prerequisites, HTTP request, Request headers, and more. The layout and formatting of these sections cannot change. But you can change the information within the sections.

## How do I contribute?

Follow these steps to make a change and submit a contribution to the docs.
1. **Fork the repo**. https://help.github.com/articles/fork-a-repo/
2. **[Clone the forked repo](https://help.github.com/articles/cloning-a-repository/)** to your computer. Note: You can actually [edit files directly on GitHub](https://help.github.com/articles/editing-files-in-your-repository/) and avoid cloning. But cloning makes edits easier if you are making large changes or changes to multiple files.
3. **Check out the staging branch**. New submissions are always reviewed and tested in the **staging** branch before they can go live.
3. **Make your changes**. You can use any editor of your choice. We like to use [Visual Studio Code](https://code.visualstudio.com/download). We use Markdown to document, and you can find more information at the [Markdown Home][].
4. **[Create a pull request (PR)](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)** from your fork to our original doc repo. 

## I created the PR, so now what happens?

If the change is significant (more than just a typo) you'll be asked to sign a Contribution License Agreement (CLA). You will only be asked to sign the CLA once. If you make future contributions you won't be asked again. Please carefully review the document; you may also need to have your employer sign the document. Once approved your PR can be reviewed by the docs team. You may be asked to make a few changes before the PR can be accepted. Once it is accepted it will be merged and eventually published live.

We do our best to review pull requests within 10 business days.

## More resources

* If you are new to Markdown, check out the [Markdown Home][].
* If you get stuck using GitHub, there is [GitHub Help][].

[GitHub Help]: http://help.github.com/
[Markdown Home]: http://daringfireball.net/projects/markdown/
[issues]: https://github.com/microsoftgraph/microsoft-graph-docs/issues
