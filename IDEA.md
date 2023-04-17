# Collective AI
🦾 An AI developer that evolves to fit your needs

# Goals

## ⚡ Fast

- 99% of the work is not novel
    - Allow Collective to do non-novel work 
- Turn 10x developers into 1,000x developers

## 🎨 Artistic

- Treat code as an art
- Developer has personal preferences/biases
- Collective is an interface to communicate with the developer not fully automatic like AutoGPT

## 🧠 Learned

- Continuously learn about developer preferences.
- Over time, Collective will need to ask fewer questions as it becomes a compressed version of the essence of the user
    - Allow basing your preferences on other, good programmers who program idiomatically.

# Tentative Workflow

## 1. Instruction

- Give initial instruction to Collective

## 2. Q & A

- Collective asks clarifying questions, user answers
    - relevant user answers are stored to be used for future projects

## 3. Planning

- When the user is satisfied that Collective has asked enough questions, they can press [TAB] to go to the planning stage
- Planning includes a NL representation of tasks needed to complete
- 🤔 Future: potentially have GPT4 calculate dependency tree so steps can be executed in parallel
    - This would be useful for larger projects that have many sub components.

## 4. Adding Detail

- For each step user can edit/add more detail. 
    - This mapping is cached (in db) for future projects

## 5. Execution

- Comes up with low level natural language for how to complete each step
- Convert natural language to actual command
  - For instance "Install Rust" might become `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
  - At any time user can edit the transformation and this will be saved in a db so collective knows the user preferences
  - At any time user can add extra step
- After completing each step can revise steps (similar to AutoGPT)
- At any point user can pause execution and redirect with NL

# Architecture

## Execution

- All execution occurs in a docker container
- Can execute arbitrary bash/zsh commands
- mount docker folder working in to local fs

## Interface

- start with a CLI interface that communicates with executor
    - vim-like bindings (in the future will not need to be vim)

## Services

- Define a protocol communicating between executor and interface.
- allow for custom interface. In the future will probably have a dedicated GUI that will not necessarily need vim bindings

## Db

- Communicate to db-service with protocol
- Focus on making this really easy to install. For this reason, probably start with SQLite but consider in the future users might connect to a remote Db to have their data synced with OAuth

