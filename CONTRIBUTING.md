# Contributing Guidelines

Contributions of all kinds are welcome.
By offering a contribution, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md)
and that your work may be made available under the terms of [our license](LICENSE.md).

The main development is done by the core team 
(see [Issue #2](https://github.com/merely-useful/r-rse/issues/2)),
and decisions are done on a mainly "silence is agreement" philosophy for issues
and pull requests.
When a disagreement occurs, the core team will discuss, take any advice,
and decide on how to address it and continue on.

## Workflow for adding content

The main development branch is `main` and the website is built on `gh-pages`.
To add content, create a new branch in the repository and submit a PR.
We suggest using the `pr_*` family of functions from the usethis package.
See the [documentation](https://usethis.r-lib.org/articles/articles/pr-functions.html)
for learning how to use them.
Please only create a PR when you are ready for your change to be reviewed and merged in.
In general, only the `Rmd` files need to be edited.

When reviewing PRs and making changes, it's probably easier to edit the branch 
directly and push the change up. For comments, please use the commenting features
in the PR.

## Setting up and building the book

1. Install R and RStudio
1. Open RStudio by clicking on the `r-rse.Rproj` file 
1. Install the dependencies by typing in the console

    ```r
    # Make sure you have remotes installed
    # install.packages("remotes")
    remotes::install_deps()
    ```

This book is written in [Bookdown](https://bookdown.org/).
If you want to preview builds on your own computer, please:

1. Build the website by using Ctrl-Shift-B when in RStudio or;
1. When in the terminal run `make html` or `make pdf` (the book gets built to
`_book/`)

Please note that Bookdown works best with [TinyTeX](https://yihui.name/tinytex/).
After installing it, you can run `make tex-packages` to install all the packages this book depends on.
You do _not_ need to do this if you are only building and previewing the HTML versions of the books.

## Other considerations when making edits

1.  The ID for each chapter and section heading is set by putting
`{#some-label}` on the heading line. Please use the stem of the file's name in
labels, i.e., start all labels for chapter `stuff.Rmd` with the word `stuff`.
Also include the course type to the beginning (e.g. "r-", "py-", and "rse-").

1.  Each chapter starts with a list of questions and a list of learning
objectives and ends with a list of key points. These lists are kept in plain
Markdown files in the `questions`, `objectives`, and `keypoints` folders
respectively so that they can be included in both the chapters and the
`objectives.Rmd` and `keypoints.Rmd` appendices.

1. Please always use `[text][label]` to refer to links and put the URL itself in
the `links.md` file to ensure consistency between chapters.

1. Please use the free desktop version of [draw.io](https://www.draw.io/) to
draw diagrams. Save the source as `figures/stem/stem.drawio` and export drawings
as all of PDF, PNG, and SVG.

1. Since LaTeX doesn't understand SVG images, hand-drawn diagrams are included as follows:
    -   Create an R code block with the header `{r stem-label, echo=FALSE, fig.cap="Some Caption"}`, which means:
        -   Give this figure the ID `fig:stem-label`.
            (Bookdown automatically puts `fig:` in front of figure labels,
            though it doesn't prefix section labels with anything.)
        -   Don't show the R code used to load the image, just its output (i.e., the image).
        -   Give the figure the specified caption.
    -   Use `insert_graphic("figures/stem/filename.ext")` to include your image. If you are using a `.pdf` image, make sure that you have the same file but as a `.svg` as well. 

1.  Use `@Name1234` or `[@Name1234]` to refer to bibliography entries. These
entries must exist in the `book.bib` file. For multiple entries, separate the
entries with `;`, i.e. `[@Name1234;@Name5678]`.

1.  Use `\@ref(label)` to refer to labels for sections and figures. Note that:
    -   This only inserts the section number, not the words `Chapter`, `Appendix`, `Section`, or `Figure`.
    -   Those are round parentheses, not curly braces.
    -   If the figure's chunk ID is `stem-label`, use `fig:stem-label` to refer to it.

1.  Glossary entries are in `gloss.md`, which is plain Markdown rather than R Markdown.
    -   To refer to a glossary entry, use a direct link of the form `[text]``(glossary.html#term-label)`.
    -   Glossary definitions are set in bold and use an HTML anchor tag to provide the ID.
        We should find a more elegant way to do this.

1. Style guide: We follow the [tidyverse style
guide](https://style.tidyverse.org/). Please read and adhere to those styles.
The styler package can help with that.

1. We use Simplified English rather than Traditional English, i.e., American
rather than British spelling and grammar.

1. The perspective for writing is as if we are the instructor doing
the live coding (or lecture) to the learners. So language might be something like:
    - For live coding:
        - "We will now do this" rather than "You will now do this"
    - For exercises:
        - "You should/will/need to"
    - For reading material or informational sections:
        - "You can/could/might"
    - Pronouns should in general be active and direct, e.g. first or second
    person ("we", "you"), rather than indirect third-person ("they").
      - When third person pronoun is necessary, use either "she" or "they"
      unless talking about e.g. one of the personas.
      - Active and direct in the sense that content is directed about something
      tangible
    
1. Keep code chunks no longer than 70 characters long, since the PDF output 
will be a bit tight.

## Language considerations

- Write in plain, international English.
- Write in the active voice. The assumed reader for "you" refers to:
    - The learner when writing in chapters and learning content.
    - The instructor for instructor sections and appendices.

## Using R packages in the book

GitHub Actions needs to know what packages to install to build the website. To
add an R package dependency, use the command `usethis::use_package()` in the R
Console while in the `r-rse` R project in RStudio. This will add the package
dependency to the `DESCRIPTION` file under the imports section. For example, if
you want to add the package dplyr, you would type out
`usethis::use_package("dplyr")` and hit enter.

**Note**, this section only documents what was done and why. This does not need
to be done, unless others want to clone this repository for their own purposes.
In order for GitHub Actions to build the website to the `gh-pages` branch,
a GitHub Personal Access Token (PAT) must be added. This PAT can be generated
and assigned to the Secrets setting of the project repository, followed by these
steps:

1. Create a [PAT](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line)
for your account on GitHub (make sure to enable the "repo" scope so that using
this token will enable writing to your GitHub repos) and copy the token to your
clipboard.
1. Go to the GitHub repository Settings, then to Secrets.
1. Create a New Secret for `UNIQUE_PAT` and paste the PAT token into the field.
1. Create another New Secret, called `EMAIL` and include your email there.

