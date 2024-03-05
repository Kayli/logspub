# notes about different integrated development environments

## vscode

- history
  - first announced on april 29, 2015, by microsoft at the 2015 build conference. 
  - same year the source was released under the mit license and made available on github
    - extension support was also announced
  - community distribution, called vscodium, is maintained, which provides mit licensed binaries

- shortcuts
  - macos
    - opt + cmd + left/right:   switch between tabs
    - cmd + shift + k:          delete line

- to enable "goto definition" f12 for particular project in vscode
  - press ctrl-shift-p 
  - select OmniSharp: Select Project to select the correct project (or .sln file)

- select interpreter
    - use 'Python: Select Interpreter' command from the command palette (ctrl+shift+p)

- install "code" command in macos terminal
  - open the command pallette with Command + Shift + P (or F1)


## intellij idea

- terminology
  - 'project' is what's called 'solution' in .net
  - 'module' == 'project' in .net
  - 'package' == 'assembly' in .net


## zed

- faster load times
- gpu acceleration
- native integration with copilot
- some other native useful features
  - convert case functionality
  - keymap and palette similar to vscode

- but
  - no plugins
  - wasn't able to open text file from terminal quickly (but haven't checked cli package yet)


## questions

- is there an automatic citation plugin for copy when editing text/markdown files?
  - scenario: i've copied something from the internet and want plugin to generate citation automatically
  - answer: there is something similar in copilot windows app (preview)
    - chat agent is able to give citations to sources for web pages/articles it uses