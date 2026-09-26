**This is the Mac version.** On Windows, use [outliers-seven-ratings](https://github.com/OUTLIERS-ai/outliers-seven-ratings).

# The Seven Ratings

This repository holds one file: the seven ratings and the seventy-seven criteria underneath them, written as instructions a machine can follow.

You install Claude Code, copy this folder down, and paste one line. It reads the work already sitting on your own computer and reports how well you and your machine work together.

Nothing is asked of you while it runs, and nothing turns on the result.

---

## You do not have to type any of this

**Give this whole file to Claude Code and tell it to follow it.** Save it somewhere you can find it, start Claude Code, and say: *follow this document and set it up for me.*

It works through the steps below on its own and stops at the points that need you: the login, and the permission questions. Every one of those is listed further down, in order, with the answer, so you know them before they arrive.

The commands are printed here so you can see what is being done on your machine, not because you have to type them. If you would rather type them yourself, they work exactly as printed.

---

## What you need before you start

- A Mac.
- A paid Claude plan: Pro, Max, Team or Enterprise. The free Claude plan does not include Claude Code, and Claude Code is the program that runs this.
- Roughly twenty minutes to install, plus however long the reading takes once it starts.

**Do not tidy anything up first.** A folder that has been prepared for a reading makes the reading less useful, and the parts that matter most cannot be prepared for anyway.

---

## The words used below, defined once

- **Terminal.** A window where you type instructions instead of clicking. On a Mac it is called Terminal.
- **Claude Code.** Claude running inside that window, with permission to open the files on your own machine.
- **Repository.** A folder of files stored on GitHub. This is one.
- **Clone.** Copy a repository from GitHub down onto your own machine.
- **Home folder.** The folder with your name on it, the one holding Documents, Desktop and Downloads.
- **git.** The program that does the copying, and also the program that keeps the history of a folder. That history is part of what the assessment reads.

Every instruction in a grey box is typed or pasted into the terminal, one at a time, each followed by the Return key.

---

## Step 1. Open a terminal

Hold Command and press Space, type `Terminal`, press Return.

Leave that window open. Every step below happens in it.

---

## Step 2. Install git

Paste this and press Return:

```
git --version
```

If a version number prints, git is already installed and you are done with this step. If a box appears offering to install the developer tools, that is **prompt 1** in the list further down.

---

## Step 3. Install Claude Code

```
curl -fsSL https://claude.ai/install.sh | bash
```

Then check it:

```
claude --version
```

A working install prints a version number, such as `2.1.211 (Claude Code)`. If instead you get `command not found`, type this line, then open a new Terminal window and run `claude --version` again:

```
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
```

It adds the folder Claude Code is installed in, `~/.local/bin`, to the list of folders Terminal looks in for programs; the installer prints the same line. A new window is needed because an already-open window does not notice.

---

## Step 4. Log in

Start Claude Code:

```
claude
```

On the very first run it may ask you to pick a colour scheme: that is **prompt 2**, and any answer is fine. Then it opens your browser so you can log in, which is **prompt 3**.

Sign in with the account that carries your paid Claude plan. If your browser shows you a code rather than sending you back automatically, copy that code and paste it into the terminal on the line that says `Paste code here if prompted`. If the browser does not open at all, the terminal tells you to press `c` to copy the login address to your clipboard, and you paste that into a browser yourself.

When the terminal prints `Login successful`, press Return.

Then leave Claude Code for now. Type this and press Return:

```
/exit
```

---

## Step 5. Copy this folder onto your machine

`cd` means change directory: it moves the terminal into a different folder. These three instructions move you into your home folder, copy this repository down, then move into it.

```
cd ~
git clone https://github.com/OUTLIERS-ai/outliers-seven-ratings-mac.git
cd outliers-seven-ratings-mac
```

To confirm it arrived:

```
ls
```

You should see `SEND-AI-Working-Assessment.md` and this `README.md`. That is the whole repository.

---

## Step 6. Start Claude Code in this folder

```
claude --add-dir ~
```

`--add-dir` tells Claude Code that it may look at your home folder as well as this one. That matters because the assessment reads your session history and your other working folders, and both of those live in your home folder rather than in this one. Without it, Claude Code stops and asks you a separate question every time it looks somewhere new, which on a full reading means a great many questions.

It only ever reads. Nothing outside this folder is changed.

The first time Claude Code starts in a folder it asks whether you trust the files in it. That is **prompt 4**.

---

## Step 7. Paste the one line

This is the whole instruction. Paste it exactly as it appears here, and press Return.

```
Read `SEND-AI-Working-Assessment.md` and assess my whole system against it. Follow the instructions in the section headed *For the machine doing the reading*.
```

From here it works on its own. Answer **prompts 5 to 8** as they arrive.

**The first output is a list of the folders it counted and the folders it skipped.** Read that list before you read anything else. If it is wrong, everything after it is wrong, and you say so and have it read again.

---

## Every prompt you will see, in order, and what to answer

The exact wording changes between versions of the software, so match on what each one is asking rather than on the words. The numbers here are referred to from the steps above.

1. **During Step 2. A box offering to install the command line developer tools**, because you asked for git and it is not there yet. Answer **Install**, then **Agree** to the licence. It downloads for a few minutes. This box comes from macOS, not from Claude.

2. **Step 4. A choice of colour scheme**, on the very first run of Claude Code. Pick whichever you prefer and press Return.

3. **Step 4. A browser window asking you to log in.** Sign in with the account carrying your paid Claude plan. If it hands you a code instead of returning you to the terminal, paste that code back into the terminal. Press Return when the terminal says `Login successful`.

4. **Step 6. A question about whether you trust the files in this folder.** You do: they are the files you just copied down, and you can read every one of them yourself. Answer **yes**.

5. **During the run. Permission to read files outside this folder.** This is the important one, and it fires because your session history and your other working folders sit elsewhere on your machine. Answer **yes**. Where the answer includes an option along the lines of not asking again, take that option: it saves you answering the same question for every folder you own.

6. **During the run. Permission to run a command, with the command shown to you.** These are git history commands, such as `git log`, which list the dates on which a folder changed. Answer **yes**, and again take the option that stops it asking each time. This prompt may not appear at all, because commands that only read are often allowed to run without asking.

7. **During the run. Permission to search across a folder outside this one.** Same reason as prompt 5. Answer **yes**.

8. **Any prompt asking to write, edit, delete or move a file. Answer no.** The assessment reads and reports. It has no reason to change a single file on your machine. If you are asked, something has gone off course: answer no, and tell it to read only and carry on.

---

## What this does not do

- **Nothing is asked of you.** Every question in the assessment is answered by looking at what is already on your machine. The moment an assessment asks you whether you keep a test set, it has stopped measuring your setup and started measuring how you describe yourself.
- **Nothing is scored against you.** There is no pass, no rank, no entry, no price, and no total out of a hundred.
- **Nobody is given a five.** Five is where the field goes next. Four is the frontier and almost nothing reaches it. Three is where a good operator sits.
- **It changes nothing.** It reads your folders, your history and your sessions, and reports.

What you get back is a level for each of the seven, the one item blocking your next level, and the move that clears it.

---

## If it goes wrong

**`command not found` after installing.** Type the `echo` line from Step 3, then open a new Terminal window. The window has to be started after that line for it to find the new program.

**It reads only one folder and reports on that.** Tell it: `Read every folder in my session history, not just this one.` The assessment is explicit that the unit is the person rather than the folder, so this is a matter of it having stopped early rather than of the instrument being unclear.

**It asks you questions about your setup instead of looking.** Tell it: `Do not ask me anything. Every criterion is answered by looking at what is on disk.` An assessment that interviews you is measuring how you describe yourself.

**It writes you a report and offers to save it.** That is your choice, and saving it inside this folder is the tidiest place for it.

**It says it cannot find your session history.** The history lives at `~/.claude/projects/`, one folder per working directory. Give it that address. If the folder genuinely holds almost nothing, that is a finding rather than a fault, and the reading will say so.

This repo is made automatically from outliers-seven-ratings@603cf78. To report a problem or suggest a change, use that repo, not this one.
