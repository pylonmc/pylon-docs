# Contributing to documentation

You would like to contribute to the documentation site? Great!  
We use [MkDocs](https://www.mkdocs.org/) and [GitHub pages](https://pages.github.com/) for the documentation site you're reading right now.

Here is a step-by-step guide on how to create/edit pages.

## Step 0: Prerequisites

Before you start, make sure you have the following installed on your system:

### Git

Git is required to clone the repository and manage your changes.

You can check if Git is already installed by running:

```bash
git --version
```

If Git is not installed, you can download it from the [official Git website](https://git-scm.com/install/).

### GitHub Account

You will need a GitHub account to fork the repository and create pull requests.

If you don't have an account yet, you can [create one for free](https://github.com/signup).

### Python and pip

MkDocs requires a recent version of [Python](https://www.python.org/), and the package manager [pip](https://pip.pypa.io/en/stable/installation/), to be installed on your system.

You can check if you already have these installed from the command line:

```bash
$ python --version
Python 3.13.3
$ pip --version
pip 25.2
```

If Python is not installed, you can download it from the [official Python downloads page](https://www.python.org/downloads/).

!!! note "For Windows users"
    During installation, make sure to check the box that says "Add Python to PATH" if the installer offers such an option (it's usually off by default).

    ![Add Python to PATH](img/python-windows-path.png)

### Text Editor (Optional)

While you can edit Markdown files with any text editor, we recommend using a code editor for a better experience.

We recommend [Visual Studio Code (VS Code)](https://code.visualstudio.com/), a free and powerful code editor that works on Windows, macOS, and Linux.

**Why VS Code?**

- Built-in Markdown preview
- Git integration
- Syntax highlighting
- Extensions for enhanced Markdown editing
- File explorer for easy navigation

**Other alternatives:**

- [Sublime Text](https://www.sublimetext.com/)
- [Atom](https://atom-editor.cc/)
- [Notepad++](https://notepad-plus-plus.org/) (Windows only)
- Any text editor you're comfortable with

## Step 1: Forking the repository

Now head over to the [pylon-docs repository](https://github.com/pylonmc/pylon-docs).  
Click the "Fork" button in the top-right corner of the page to create your own copy of the repository.

![GitHub Fork](img/github-fork.png)

## Step 2: Cloning your fork

You will need to clone your forked repository to your local machine to be able to preview the changes.

First, go to your forked repository on GitHub, click on the green "Code" button, and copy the URL under "HTTPS".

![GitHub Clone URL](img/github-clone.png)

Open your terminal and run the following command (replace `<CLONE_URL_HERE>` with the URL you just copied):

```bash
git clone <CLONE_URL_HERE>
cd pylon-docs
```

## Step 3: Installing dependencies

Now that you have the repository on your local machine, you need to install the required dependencies.

In the `pylon-docs` directory, run:

```bash
pip install -r requirements.txt
```

This will install MkDocs and all other necessary packages.

## Step 4: Making your changes

Now you can start editing the documentation files!

!!! warning
    All changes you make to your fork will NOT affect the official documentation until you submit your changes via a pull request.

The documentation files are written in Markdown, a lightweight markup language. If you need help with the syntax, you can consult [Mastering Markdown](https://guides.github.com/features/mastering-markdown/).

### 4.1 Understanding the documentation structure

The documentation is organized by language in the `docs/` directory:

```text
docs/
├── en/          # English documentation
├── zh-CN/       # Simplified Chinese documentation (if available)
└── ...          # Other languages
```

For English documentation, all pages are located in `docs/en/`. The content is organized into different sections and subdirectories.

!!! danger "Important"
    Currently, we only accept contributions to the English documentation, as we are still actively working on the content of Pylon. Please stay tuned for future updates regarding contributions to other languages.

Each section has its own directory, and images for that section should be placed in an `img/` folder within the same directory.

!!! note "Example"
    If you're editing `docs/en/installation/installing-pylon.md`, place images in `docs/en/installation/img/`.

### 4.2 Creating a new page

Open your code editor in the `pylon-docs` directory and follow these steps:

1. Navigate to the appropriate subdirectory in `docs/en/` (e.g., `docs/en/installation/`)
2. Create a new `.md` file with a descriptive name

**File naming rules:**

- File names must end with `.md`
- Use lowercase letters
- Use hyphens `-` instead of spaces
- No special characters
- Examples: `installing-addons.md`, `custom-recipes.md`, `getting-started.md`

Then:

1. Write your content using Markdown syntax
2. Save the file
3. Preview your changes (see [Step 5](#step-5-previewing-your-changes))

### 4.3 Editing an existing page

1. Open the file you want to edit in your code editor
2. Make your changes
3. Save the file
4. Preview your changes (see [Step 5](#step-5-previewing-your-changes))

### 4.4 Adding images

Images help illustrate your documentation and make it easier to understand.

#### Image naming conventions

- Use lowercase letters only
- Use hyphens `-` instead of spaces
- Use descriptive names
- Use PNG format when possible
- Examples: `github-fork.png`, `custom-item-example.png`, `crafting-table.png`

#### Where to place images

Images should be placed in an `img/` folder **in the same directory** as your markdown file.

For example:

- If your page is `docs/en/installation/installing-pylon.md`
- Place images in `docs/en/installation/img/`

If the `img/` folder doesn't exist in that directory, create it first.

#### Using images in your page

To embed an image in your markdown file, use the following syntax:

```markdown
![Image description](img/your-image-name.png)
```

- Replace `Image description` with a short description of what the image shows
- Replace `your-image-name.png` with your actual filename
- The `img/` path is relative to your current markdown file

**Example:**

```markdown
![GitHub Fork button](img/github-fork.png)
```

## Step 5: Previewing your changes

Before submitting your changes, it's a good idea to preview them locally to make sure everything looks correct.

Run the following command in the `pylon-docs` directory:

```bash
mkdocs serve --livereload
```

This will start a local web server. Open your browser and go to `http://127.0.0.1:8000` to see the documentation site with your changes.

The preview will automatically update when you save changes to the files!

## Step 6: Committing and pushing your changes

Once you're happy with your changes, you need to commit and push them to your fork.

Run the following commands in the `pylon-docs` directory:

```bash
git add .
git commit -m "Your commit message describing the changes"
git push
```

!!! tip
    Write a clear and descriptive commit message that explains what you changed and why.

## Step 7: Creating a pull request

Once you pushed your changes to your fork on GitHub, you can create a pull request to submit your changes.

1. Go to your forked repository on GitHub. You can always find your fork on GitHub's dashboard or your profile page.
2. Click on the "Pull requests" tab.  
![GitHub Pull Requests Tab](img/github-pull-requests.png)
3. Click on the green "New pull request" button.
4. Fill in the title and description for your pull request.
5. Click "Create pull request".

That's it! Your changes will be reviewed by the maintainers. If everything looks good, your contribution will be merged. 🎉

## Step 8: Making changes to your Pull Request

If you have already submitted a pull request but need to make changes (for example, if a reviewer requested changes), you can do that easily.

Just repeat [Step 4](#step-4-making-your-changes) and [Step 6](#step-6-committing-and-pushing-your-changes) to make and commit your changes.

The pull request will automatically update to include your new changes until it has been merged or closed.

---

**Thank you for contributing to the Pylon documentation!** 🙏
