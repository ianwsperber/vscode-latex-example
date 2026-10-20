# Writing maths assignments in LaTeX with VS Code

A ready-to-use template for writing maths and science assignments in **LaTeX**, edited in **VS Code**, that turns into a neat PDF **every time you press save**.

It was made for distance-learning students (for example, Open University students writing assignments), but it works for any maths-heavy homework. **You do not need any previous experience with Git, VS Code or LaTeX.** This guide walks through everything from a blank computer to a finished PDF, on **Windows** or **Mac**.

When you're done, your screen will look roughly like this: your writing on the left, the finished PDF on the right, updating each time you save.

```
┌──────────────────────────────┬──────────────────────────────┐
│ main.tex / problem1.tex      │  PDF preview                 │
│                              │                              │
│ \begin{align*}               │   Question 1                 │
│   3x + 4 &= 10 \\            │   (a)                        │
│   3x &= 6 \\                 │     3x + 4 = 10              │
│   x &= 2                     │         3x = 6               │
│ \end{align*}                 │          x = 2               │
└──────────────────────────────┴──────────────────────────────┘
```

---

## Contents

1. [What are all these things?](#1-what-are-all-these-things)
2. [Install LaTeX](#2-install-latex)
3. [Install VS Code](#3-install-vs-code)
4. [Get this project onto your computer](#4-get-this-project-onto-your-computer)
5. [Open the project and install the LaTeX extension](#5-open-the-project-and-install-the-latex-extension)
6. [Build your first PDF](#6-build-your-first-pdf)
7. [Make it your own](#7-make-it-your-own)
8. [A tiny LaTeX crash course](#8-a-tiny-latex-crash-course)
9. [Using Git to keep a history of your work (optional)](#9-using-git-to-keep-a-history-of-your-work-optional)
10. [Troubleshooting](#10-troubleshooting)
11. [Handy keyboard shortcuts](#11-handy-keyboard-shortcuts)

---

## 1. What are all these things?

| Thing | What it is | Do I need it? |
|---|---|---|
| **LaTeX** (say "lay-tek") | A way of writing documents as plain text with little commands, e.g. `\frac{1}{2}` becomes ½. A program reads your text and produces a beautifully typeset PDF. It is the standard way mathematicians write. | **Yes** |
| **A TeX distribution** (MiKTeX, MacTeX, TeX Live) | The actual program that turns your `.tex` files into a PDF. You install it once and then mostly forget about it. | **Yes** |
| **VS Code** (Visual Studio Code) | A free text editor from Microsoft. Think of it as a smarter Notepad / TextEdit. | **Yes** |
| **LaTeX Workshop** | A free add-on ("extension") for VS Code. It compiles your document whenever you save and shows the PDF next to your writing. | **Yes** |
| **Git** | A tool that saves snapshots ("commits") of your work so you can go back in time. GitHub is a website that stores Git projects online. | **No.** Optional, but handy |
| **Terminal** | A window where you type commands. You will barely need it, and every command you need is written out below. | Rarely |

**How the pieces fit together:** you type in **VS Code** → press save → **LaTeX Workshop** asks your **TeX distribution** to build the document → the **PDF** appears in a tab next to your writing.

---

## 2. Install LaTeX

This is the biggest download (it can take 30–60 minutes on a slow connection), so start it first and install VS Code while you wait.

### On Windows: MiKTeX + Strawberry Perl

1. Go to <https://miktex.org/download> and download the **Windows installer**.
2. Run it and accept the defaults, **except** on the settings page:
   - Set **"Install missing packages on-the-fly"** to **Yes**. This lets MiKTeX quietly download any extra bits a document needs, instead of stopping to ask you each time.
3. When it finishes, open **MiKTeX Console** from the Start menu and click **Check for updates**, then **Update now**. (A fresh MiKTeX install is often a little out of date.)
4. Install **Strawberry Perl** from <https://strawberryperl.com> (download the latest `.msi` and accept the defaults).
   > **Why?** The build tool this project uses (`latexmk`) is written in a language called Perl. Macs come with Perl already; Windows doesn't. If you skip this step you'll get an error like *"latexmk: command not found"* or *"script engine 'perl' not found"*.
5. **Restart your computer.** This makes sure every program can find the newly installed tools.

> **Alternative:** you can install **TeX Live** for Windows from <https://tug.org/texlive/windows.html> instead of MiKTeX. It includes Perl, so you can skip Strawberry Perl, but it's a much bigger download (several GB).

### On Mac: MacTeX

1. Go to <https://tug.org/mactex/> and download **MacTEX.pkg**. It's large (about 5–6 GB), which is normal.
2. Double-click the downloaded file and follow the installer, accepting the defaults.
3. **Restart your Mac** (or at least fully quit and reopen any apps you'll be using).

MacTeX includes everything this project needs, including `latexmk` and Perl.

### Check it worked (optional but reassuring)

Open a terminal:

- **Windows:** press the Windows key, type `cmd`, press Enter.
- **Mac:** press `Cmd + Space`, type `Terminal`, press Enter.

Type each of these and press Enter:

```
pdflatex --version
latexmk --version
```

Each should print a few lines starting with a version number. If you see *"not recognised"* / *"command not found"*, restart your computer and try again. Still stuck? See [Troubleshooting](#10-troubleshooting).

---

## 3. Install VS Code

1. Go to <https://code.visualstudio.com> and click the big download button. It detects Windows or Mac automatically.
2. Install it:
   - **Windows:** run the installer. On the "Select Additional Tasks" page, tick **"Add 'Open with Code' action to Windows Explorer file context menu"** and **"Add 'Open with Code' action to Windows Explorer directory context menu"**. This lets you right-click a folder and open it in VS Code.
   - **Mac:** open the downloaded `.zip`, then drag **Visual Studio Code** into your **Applications** folder.
3. Open VS Code. You'll see a Welcome page, which you can close.

---

## 4. Get this project onto your computer

Pick **one** of these. Option A is easiest if you've never used Git.

### Option A: Download a ZIP (no Git needed)

1. Go to <https://github.com/ianwsperber/vscode-latex-example>.
2. Click the green **`<> Code`** button, then **Download ZIP**.
3. Find the ZIP in your Downloads folder and unzip it:
   - **Windows:** right-click → **Extract All…**
   - **Mac:** double-click it.
4. Move the unzipped folder somewhere sensible and give it a name, e.g. `Documents/Assignments/Assignment-01`.

> **Tip:** avoid putting the folder inside a cloud-synced folder that "frees up space" by keeping files online only (e.g. OneDrive "Files On-Demand" or iCloud "Optimise Mac Storage"). LaTeX creates lots of small temporary files and these services sometimes get in the way. A normal local folder is safest.

### Option B: Clone with Git

Use this if you want the version-history features in [section 9](#9-using-git-to-keep-a-history-of-your-work-optional).

1. **Install Git**
   - **Windows:** download from <https://git-scm.com/download/win> and run the installer. The defaults are fine; just click **Next** through every page.
   - **Mac:** open Terminal, type `git --version` and press Enter. If Git isn't installed, macOS will offer to install the **Command Line Developer Tools**. Click **Install** and wait.
2. **Tell Git who you are** (only once per computer). In a terminal:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```
3. **Clone the project from inside VS Code:**
   - Open VS Code.
   - Press `Ctrl + Shift + P` (Windows) or `Cmd + Shift + P` (Mac) to open the **Command Palette**. This is a search box for every VS Code action.
   - Type `Git: Clone` and press Enter.
   - Paste `https://github.com/ianwsperber/vscode-latex-example.git` and press Enter.
   - Choose a folder to put it in. When asked **"Would you like to open the cloned repository?"**, click **Open**.

---

## 5. Open the project and install the LaTeX extension

1. In VS Code choose **File → Open Folder…** (on Mac: **File → Open…**) and select the project folder, the one that contains `README.md` and the `tex` folder.
   - If VS Code asks **"Do you trust the authors of the files in this folder?"**, click **Yes, I trust the authors**.
2. Install **LaTeX Workshop**:
   - This project tells VS Code which extension it needs, so you'll probably see a pop-up in the bottom-right saying *"Do you want to install the recommended extensions…?"*. Click **Install**.
   - No pop-up? Click the **Extensions** icon in the left sidebar (four little squares), or press `Ctrl + Shift + X` / `Cmd + Shift + X`. Search for **LaTeX Workshop**, choose the one by **James Yu**, and click **Install**.
3. After it installs you'll see a new **TeX** icon in the left sidebar. That's LaTeX Workshop's panel.

### What's in the project

The **Explorer** panel (top icon in the sidebar, `Ctrl/Cmd + Shift + E`) shows the files:

```
vscode-latex-example/
├── README.md                ← this guide
├── .vscode/
│   ├── extensions.json      ← tells VS Code to recommend LaTeX Workshop
│   └── latex.code-snippets  ← typing shortcuts (see section 8)
└── tex/
    ├── main.tex             ← the "master" document: title, name, page layout,
    │                          and a list of which questions to include
    ├── main.pdf             ← the finished PDF (appears after your first build)
    ├── assets/              ← put images (graphs, sketches, screenshots) here
    └── problems/
        ├── problem1.tex     ← your answer to Question 1
        └── problem2.tex     ← your answer to Question 2
```

Each question lives in its own small file, so you never have to scroll through one giant document. `main.tex` pulls them all together with `\input{...}` lines.

---

## 6. Build your first PDF

1. In the Explorer, open `tex/main.tex`.
2. Save it: `Ctrl + S` (Windows) or `Cmd + S` (Mac). Even though nothing changed, saving triggers a build.
3. Watch the bottom-left of the window (the **status bar**). You'll see a spinning icon while it builds and a ✓ tick when it's done. **The first build can take a minute or more**, especially on Windows where MiKTeX may download a few packages. Later builds take a couple of seconds.
4. Open the PDF next to your work, using **any** of these:
   - Click the **View LaTeX PDF** button in the top-right of the editor (a page with a magnifying glass), or
   - Press `Ctrl + Alt + V` (Windows) / `Cmd + Option + V` (Mac), or
   - Open the **TeX** panel in the sidebar → **View LaTeX PDF**.

   The PDF opens in a tab beside your writing.
5. Now open `tex/problems/problem1.tex`, change `x & = 2` to `x & = 2 \quad \text{(done!)}`, and save. The PDF updates on its own. 🎉

That's the whole workflow: **edit → save → PDF updates.**

### Make sure "build on save" is switched on

It is on by default, but if saving ever stops rebuilding the PDF:

1. Open **Settings**: `Ctrl + ,` (Windows) or `Cmd + ,` (Mac).
2. Search for `latex-workshop.latex.autoBuild.run`.
3. Make sure it's set to **`onSave`** or **`onFileChange`** (the default), **not** `never`.

> You can also build manually at any time: `Ctrl + Alt + B` (Windows) / `Cmd + Option + B` (Mac), or **TeX panel → Build LaTeX project**.

### Where is the PDF?

It's saved as **`tex/main.pdf`** inside your project folder. That's the file you submit. You'll also notice extra files appear next to it (`main.aux`, `main.log`, `main.fls`, `main.synctex.gz`, …). These are temporary build files, and it's safe to ignore or delete them. To tidy them up, use **TeX panel → Clean up auxiliary files**.

### Jumping between the PDF and your text

- **PDF → text:** `Ctrl + click` (Windows) or `Cmd + click` (Mac) on something in the PDF to jump to the line that produced it.
- **Text → PDF:** put your cursor on a line and press `Ctrl + Alt + J` (Windows) / `Cmd + Option + J` (Mac).

---

## 7. Make it your own

### Put your details in

Open `tex/main.tex` and change these lines near the top:

```latex
\rhead{Ian Smartypants}        % top-right of every page: your name (and student number, if needed)
\lhead{CLASS101 - TMA00}       % top-left of every page: module code and assignment

\title{CLASS101 - TMA00}       % big title on page 1
\author{Ian Smartypants}       % your name under the title
```

Save, and the PDF updates.

### Add another question

1. In the Explorer, right-click the `problems` folder → **New File…** → name it `problem3.tex`.
2. Copy the contents of `problem1.tex` into it as a starting point and edit away.
3. In `main.tex`, add a matching block just above `\end{document}`:
   ```latex
   \section*{Question 3}
   \input{./problems/problem3}
   ```
4. Save `main.tex`.

> **Tip:** if you're editing a question file and saving doesn't rebuild, save `main.tex` once. LaTeX Workshop needs to build from the master file at least once to learn which files belong to it.

### One folder per assignment

The simplest system: **copy the whole project folder for each new assignment** (e.g. `Assignment-01`, `Assignment-02`, …), then empty out the problem files and update the title. Each assignment stays self-contained with its own PDF.

---

## 8. A tiny LaTeX crash course

Everything in the `.tex` files is plain text. Commands start with a backslash `\`. Anything after a `%` on a line is a **comment**: it's ignored and won't appear in the PDF.

### Text

| You type | You get |
|---|---|
| `\textbf{bold}` | **bold** |
| `\textit{italic}` | *italic* |
| `\section*{Title}` | a heading (the `*` means "no number") |
| `\subsection*{(a)}` | a smaller heading, used for question parts |
| A blank line | a new paragraph |

### Maths

Put maths **inside a sentence** between `\(` and `\)`, e.g. `the root is \(x = 2\)`.

For **displayed** working, line by line with the `=` signs lined up, use `align*`. The `&` marks the point to line up on and `\\` ends a line:

```latex
\begin{align*}
    3x + 4 & = 10 \\
    3x     & = 6  \\
    x      & = 2
\end{align*}
```

Common pieces:

| You type | You get |
|---|---|
| `x^{2}` | x² (superscript; use braces for anything longer than one character) |
| `x_{1}` | x₁ (subscript) |
| `\frac{a}{b}` | a fraction a/b |
| `\sqrt{x}` | √x |
| `\int_{0}^{1} f(x) \dd x` | an integral from 0 to 1 |
| `\sum_{n=1}^{\infty}` | a sum (Σ) |
| `\alpha, \beta, \theta, \pi` | α, β, θ, π |
| `\times`, `\cdot`, `\pm` | ×, ·, ± |
| `\leq`, `\geq`, `\neq`, `\approx` | ≤, ≥, ≠, ≈ |
| `\left( ... \right)` | brackets that grow to fit what's inside |
| `\text{words}` | normal words inside maths |

### Shortcuts already set up in this template

These are defined near the top of `main.tex`:

| You type | Meaning |
|---|---|
| `\R` | ℝ, the real numbers |
| `\dd` | an upright "d" for derivatives and integrals |
| `\dx` | a correctly spaced "dx" at the end of an integral |
| `\der{y}{x}` | dy/dx |
| `\pd{f}{x}` | ∂f/∂x |

You can add your own the same way, e.g. `\newcommand{\N}{\mathbb{N}}`.

### Boxed question text

The problem files put the question inside a coloured box (using a package called `tcolorbox`) so it's easy to tell the question apart from your answer. The quickest way to make one is the `problem` typing shortcut (below). You can also copy the `\begin{tcolorbox}...\end{tcolorbox}` block from `problem1.tex` and change the `title=` to whatever you like.

### Typing shortcuts (snippets)

This project comes with **snippets**: short words that expand into longer chunks of LaTeX. In any `.tex` file, start typing a prefix from the table below. A suggestion list pops up; press **Enter** or **Tab** to insert the snippet. The cursor lands in the first blank, and pressing **Tab** jumps to the next one.

| Type | You get |
|---|---|
| `align` | an `align*` block for line-by-line working |
| `eq` | a numbered `equation` block |
| `frac` | `\frac{}{}`, a fraction |
| `dx` | `\frac{d}{dx}`, a derivative (the `x` is a blank you can change) |
| `comm` | `\quad \textit{( )}`, an italic note at the end of a working line, e.g. *(divide both sides by 3)* |
| `problem` | a blue box titled **Problem**, for the question text |
| `instructions` | a grey box titled **Instructions** |
| `quote` | an indented block starting with **Problem:**, a plainer alternative to the box |
| `red` | **bold red text**, handy for notes to yourself, such as "check this!" (remember to remove them before submitting) |
| `image` | a centred picture with a caption. Put the image file in `tex/assets/` and type its file name (e.g. `graph.png`) in the second blank. |

The snippets live in `.vscode/latex.code-snippets`. Open that file to change them or add your own: copy an existing entry and edit its `prefix` and `body`.

### When you get stuck

- Search the web for "latex how to …". Almost every question has been answered on <https://tex.stackexchange.com>.
- <https://www.overleaf.com/learn> has excellent beginner guides (you can ignore the parts about using Overleaf itself).
- Can't remember a symbol's command? Draw it at <https://detexify.kirelabs.org>.

---

## 9. Using Git to keep a history of your work (optional)

If you cloned the project with Git (Option B), VS Code can save **snapshots** of your work. Think of it as an "undo history" that survives closing the app. It's great for peace of mind before a big edit.

### Saving a snapshot ("commit")

1. Click the **Source Control** icon in the sidebar (it looks like a branching line), or press `Ctrl + Shift + G` (this is the same on Windows and Mac).
2. You'll see a list of files you've changed since the last snapshot.
3. Type a short message describing what you did, e.g. `Finished question 2`.
4. Click **Commit**. If VS Code asks *"There are no staged changes… Would you like to stage all your changes and commit them directly?"*, click **Yes** (or **Always**).

### Looking back

- Click a file in the Source Control panel to see a side-by-side view of exactly what changed.
- In the Explorer, right-click a file → **Open Timeline** to see every saved version of it.

### Notes

- **What Git saves:** your `.tex` files, images and the finished `tex/main.pdf` are saved in each snapshot, so you can always get back the PDF you submitted. The included `.gitignore` file tells Git to skip the temporary build files (`.aux`, `.log`, `.synctex.gz`, …) and any other PDFs, such as reference material you've put in the folder.
- **Backing up online (optional):** if you have a free GitHub account you can click **Publish Branch** / **Sync Changes** in the Source Control panel to store a copy online. If you do, make sure the repository is **private**, so other students can't see your answers.
- If you cloned *this* repository, it's still linked to the original on GitHub. To start fresh with your own history, use Option A (Download ZIP) instead, then in VS Code's Source Control panel click **Initialize Repository**.

---

## 10. Troubleshooting

**First, look at the error.** When a build fails, the status bar shows a ✗. Click it, or open the **Problems** panel (`Ctrl + Shift + M` / `Cmd + Shift + M`), to see a list of errors with line numbers. Click one to jump to the line. For the full story, open the **TeX** panel → **View Log messages** → **View LaTeX compiler log**.

| Problem | What to try |
|---|---|
| **"latexmk: command not found"**, **"spawn latexmk ENOENT"** or **"recipe terminated with fatal error"** right away | VS Code can't find your LaTeX installation. **Fully quit VS Code and restart your computer**, then try again. Run `latexmk --version` in a terminal ([section 2](#check-it-worked-optional-but-reassuring)) to check LaTeX is installed. |
| **Windows: "script engine 'perl' not found"** or latexmk fails instantly | Install Strawberry Perl ([section 2](#on-windows-miktex--strawberry-perl)) and restart your computer. |
| **Windows: build hangs forever the first time** | MiKTeX may be showing a hidden pop-up asking to install a package. Look for it behind other windows, or turn on "install missing packages on-the-fly" in **MiKTeX Console → Settings**. |
| **"! LaTeX Error: File `something.sty' not found"** | A package is missing. **Windows/MiKTeX:** open MiKTeX Console → **Packages**, search for the name, and install it (or turn on on-the-fly installs). **Mac/MacTeX:** MacTeX includes almost everything; if you installed the smaller *BasicTeX*, install the full MacTeX instead. |
| **"Undefined control sequence"** | A command is misspelled (e.g. `\fracc`), or you used a command whose package isn't loaded. The error tells you the line number. |
| **"Missing $ inserted"** | You used maths (like `^`, `_` or `\alpha`) outside a maths area. Wrap it in `\( ... \)` or put it inside `align*`. |
| **"Missing } inserted"** / weird runaway errors | A `{` without a matching `}`, or a `\begin{...}` without its `\end{...}`. Check the lines just above where the error points. |
| **The PDF doesn't update when I save** | Check the build-on-save setting ([section 6](#make-sure-build-on-save-is-switched-on)). Save `main.tex` once. Make sure you opened the **project folder** (File → Open Folder), not just a single file. |
| **The build seems stuck in a bad state** | **TeX panel → Clean up auxiliary files**, then save again. As a last resort, delete everything in `tex/` except your `.tex` files and the `problems` and `assets` folders. |
| **No "install recommended extensions" pop-up** | Install LaTeX Workshop manually from the Extensions panel ([section 5](#5-open-the-project-and-install-the-latex-extension)). |
| **Something else** | Copy the first error line from the log into a web search. Someone has almost certainly hit it before. |

> **Golden rule:** LaTeX usually reports the *first* problem it found. Fix the first error, save, and many of the others often disappear with it.

---

## 11. Handy keyboard shortcuts

| Action | Windows | Mac |
|---|---|---|
| Save (and build the PDF) | `Ctrl + S` | `Cmd + S` |
| View the PDF | `Ctrl + Alt + V` | `Cmd + Option + V` |
| Build manually | `Ctrl + Alt + B` | `Cmd + Option + B` |
| Jump from text to PDF | `Ctrl + Alt + J` | `Cmd + Option + J` |
| Jump from PDF to text | `Ctrl + click` in PDF | `Cmd + click` in PDF |
| Command Palette (search every action) | `Ctrl + Shift + P` | `Cmd + Shift + P` |
| Find a file by name | `Ctrl + P` | `Cmd + P` |
| Show the file Explorer | `Ctrl + Shift + E` | `Cmd + Shift + E` |
| Show errors (Problems panel) | `Ctrl + Shift + M` | `Cmd + Shift + M` |
| Comment / uncomment lines | `Ctrl + /` | `Cmd + /` |
| Undo / Redo | `Ctrl + Z` / `Ctrl + Y` | `Cmd + Z` / `Cmd + Shift + Z` |

Happy typesetting! ✍️
