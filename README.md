# OverTheWire Writeups

This repository contains my notes, solutions, and command references for the **OverTheWire** wargames. The goal is to document my learning process while practicing Linux, networking, shell scripting, Git, cryptography, and binary exploitation.

## Repository Structure

```text
.
├── README.md
├── bandit/
│   ├── README.md
│   ├── 0
│   ├── 1
│   ├── 2
│   ├── ...
│   └── 33
├── natas/
├── krypton/
├── leviathan/
├── narnia/
├── behemoth/
├── utumno/
├── maze/
├── vortex/
├── manpage/
├── drifter/
└──formulaone/
```

### Password Files

The `bandit/` directory contains numbered files (`0`, `1`, `2`, …, `33`) storing the password for each Bandit level. This allows logging in with `sshpass` without manually entering passwords.

Example:

```bash
sshpass -p "$(cat 17)" ssh bandit17@bandit.labs.overthewire.org -p 2220
```

These files are intended for local practice and **should not be committed to a public repository**.

## Wargames

| Wargame   |    Status   | Notes                                                                                                 |
| --------- | :---------: | ----------------------------------------------------------------------------------------------------- |
| Bandit    |x | Linux fundamentals, SSH, file permissions, cron, networking, OpenSSL, Git, shell scripting, and more. |
| Natas     |  * | Web security.|
| Krypton   |  x  | Cryptography.                                                                  |
| Leviathan |  -- | Privilege escalation and basic binary exploitation.                                                   |
| Narnia    |  -- | Buffer overflows and memory corruption.                                                               |
| Behemoth  |  -- | Reverse engineering and exploitation.                                                                 |
| Utumno    |  -- | Advanced exploitation challenges.                                                                     |
| Maze      |  -- | Miscellaneous Linux and security challenges.                                                          |
| Vortex    |  -- |                                                                              |
| Manpage   |  -- | Man pages.                                                                                            |
| Drifter   |  -- |                                                                              |
| FormulaOne|  -- |                                                                              |

**Note:**

-- : Planned

x : Completed

\* : In progress

## Usage

Clone the repository:

```bash
git clone <repository-url>
cd OverTheWire
```

Navigate to the desired wargame:

```bash
cd bandit
```

Follow the instructions in that directory's `README.md`.

## Resources

* https://overthewire.org/wargames/
* https://overthewire.org/wargames/bandit/

## Disclaimer

These writeups are for educational purposes only. All solutions were developed while working through the OverTheWire wargames, which are intentionally designed as legal practice environments.
