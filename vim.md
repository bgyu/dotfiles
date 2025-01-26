## **buffers**, **windows**, and **tabs** in Vim:

| **Action**                        | **Buffers**                             | **Windows**                               | **Tabs**                                  |
|------------------------------------|-----------------------------------------|------------------------------------------|------------------------------------------|
| **List**                          | `:ls` or `:buffers`                     | Not applicable                           | `:tabs`                                  |
| **Switch**                        | `:b <buffer_number>`                    | `Ctrl-w h/j/k/l` (move left/right/up/down) | `gt` (next tab), `gT` (previous tab)     |
| **Open New**                      | `:e <file>` or `:new`                   | `:split` (horizontal), `:vsplit` (vertical) | `:tabnew` or `:tabe <file>`             |
| **Close/Delete**                  | `:bd` (delete current buffer)           | `:close` or `Ctrl-w q`                   | `:tabclose`                              |
| **Show Current**                  | `:echo bufnr('%')`                      | `Ctrl-w w` (cycle through windows)       | `:echo tabpagenr()` (show current tab number) |
| **Save**                          | `:w` (saves the current buffer)         | Not applicable                           | Not applicable                           |
| **Resize**                        | Not applicable                          | `Ctrl-w +` / `Ctrl-w -` (height)         | Not applicable                           |
| **Split**                         | Not applicable                          | `:split` (horizontal), `:vsplit` (vertical) | Not directly split; use multiple tabs   |
| **Run Command on All**            | `:bufdo <command>`                      | `:windo <command>`                       | `:tabdo <command>`                       |
| **Navigate Next**                 | `:bnext` or `:bn`                       | `Ctrl-w w` or `Ctrl-w Ctrl-w`            | `gt`                                     |
| **Navigate Previous**             | `:bprev` or `:bp`                       | `Ctrl-w W` (reverse cycle through windows) | `gT`                                     |
| **Navigate First**                | `:bfirst` or `:bf`                      | Not applicable                           | `:tabfirst`                              |
| **Navigate Last**                 | `:blast` or `:bl`                       | Not applicable                           | `:tablast`                               |
| **Equalize Sizes**                | Not applicable                          | `Ctrl-w =`                               | Not applicable                           |
| **Open Buffer in Split**          | `:sb <buffer_number>`                   | `:split <file>`                          | `:tab sb <buffer_number>`                |
| **Open All Buffers**              | `:sball`                                | `:sball` (in multiple splits)            | Not applicable                           |
| **Close Others**                  | Not applicable                          | `:only` (close all other windows)        | `:tabonly`                               |
| **Display Info**                  | `:ls` to list buffers                   | `Ctrl-w t` (top-left window), `Ctrl-w b` (bottom-right window) | `:tabs`                                  |

---

### Highlights of Operations:
- **Buffers**:
  - Focused on managing the files in memory (create, delete, switch).
- **Windows**:
  - Used for organizing views of buffers in splits for simultaneous editing.
- **Tabs**:
  - Group windows into layouts for high-level workspace organization.

---


### **Vim Configuration Language**

The Vim configuration file (`.vimrc`) uses a **domain-specific language (DSL)** designed specifically for Vim. It’s not a general-purpose programming language but rather a simple scripting syntax that allows you to:
- Set options (`set` command)
- Define key mappings (`map`, `noremap`, etc.)
- Create custom commands (`command!`)
- Write conditional logic (`if`, `else`, etc.)
- Automate tasks with loops (`while`, `for`, etc.)

The syntax is lightweight and geared toward manipulating Vim's behavior and environment.

---

### **Breaking Down `nnoremap <leader>n :bnext<CR>`**

This command is a **key mapping** in Vim, and here’s what each part means:

#### **1. `nnoremap`**
- **`n`**: Specifies that this mapping is for **Normal mode** (Vim has different modes: Normal, Insert, Visual, etc.).
- **`noremap`**: Ensures that the mapping is **non-recursive**. This means if the mapped key (`<leader>n`) is bound to another command elsewhere, Vim won't recursively expand it.
  - For example, if `:map n` were mapped to something else, `noremap` ensures the mapping stays to `:bnext<CR>` only.

#### **2. `<leader>`**
- **`<leader>`**: A customizable prefix key used as a shorthand for user-defined shortcuts.
  - You can define your leader key in `.vimrc`:
    ```vim
    let mapleader = ","
    ```
    By default, `<leader>` is `\` (backslash). So if `<leader>` is set to `,`, the mapping becomes `,n`.

#### **3. `n`**
- This is the key that follows the leader key.
- Together, `<leader>n` becomes the shortcut. For example, pressing `,n` (if `<leader>` is set to `,`) triggers this mapping.

#### **4. `:bnext`**
- `:bnext` is a Vim command to **switch to the next buffer** (the next file loaded in memory).
  - If you have multiple files open in Vim, `:bnext` moves to the next one in the buffer list.

#### **5. `<CR>`**
- `<CR>` stands for **Carriage Return**, which is equivalent to pressing the Enter key.
- Since `:bnext` is a command, `<CR>` is needed to execute it.

---

### **Putting It All Together**
This line:
```vim
nnoremap <leader>n :bnext<CR>
```
- **Maps the shortcut `<leader>n`** (e.g., `,n`) in **Normal mode** to run the `:bnext` command.
- When you press `<leader>n`, Vim switches to the next buffer in the list.
- The `<CR>` ensures the command executes when triggered.

---

### **How to Use This in Your `.vimrc`**
1. Add the following to your `.vimrc`:
   ```vim
   let mapleader = ","
   nnoremap <leader>n :bnext<CR>
   ```

2. Restart Vim or reload your configuration with `:source ~/.vimrc`.

3. Now, pressing `,n` will take you to the next buffer.

---

### **Experimentation**
You can modify the key mapping for other buffer commands:
- Go to the previous buffer:
  ```vim
  nnoremap <leader>p :bprev<CR>
  ```
- Close the current buffer:
  ```vim
  nnoremap <leader>d :bd<CR>
  ```
### **Default Key Mappings in Vim**

Vim has a rich set of **default key mappings** across its various modes. Below is a list categorized by mode, along with some advanced tips for custom mappings and leader key usage.

---

### **1. Default Key Mappings by Mode**

#### **Normal Mode (Default Mode)**
| **Key**   | **Action**                                          |
|-----------|-----------------------------------------------------|
| `h`       | Move left.                                          |
| `l`       | Move right.                                         |
| `j`       | Move down.                                          |
| `k`       | Move up.                                            |
| `0`       | Move to the beginning of the current line.          |
| `^`       | Move to the first non-whitespace character.         |
| `$`       | Move to the end of the current line.                |
| `w`       | Move to the start of the next word.                 |
| `e`       | Move to the end of the current/next word.           |
| `b`       | Move to the start of the previous word.             |
| `gg`      | Go to the beginning of the file.                    |
| `G`       | Go to the end of the file.                          |
| `u`       | Undo the last change.                               |
| `Ctrl-r`  | Redo the last undone change.                        |
| `:w`      | Save the file.                                      |
| `:q`      | Quit Vim.                                           |
| `dd`      | Delete the current line.                            |
| `yy`      | Yank (copy) the current line.                       |
| `p`       | Paste after the cursor.                             |
| `P`       | Paste before the cursor.                            |
| `/pattern`| Search forward for `pattern`.                       |
| `?pattern`| Search backward for `pattern`.                      |
| `n`       | Repeat the last search forward.                     |
| `N`       | Repeat the last search backward.                    |
| `.`       | Repeat the last change.                             |
| `x`       | Delete the character under the cursor.              |

---

#### **Insert Mode**
| **Key**     | **Action**                                   |
|-------------|----------------------------------------------|
| `i`         | Enter Insert mode before the cursor.         |
| `I`         | Enter Insert mode at the start of the line.  |
| `a`         | Enter Insert mode after the cursor.          |
| `A`         | Enter Insert mode at the end of the line.    |
| `o`         | Insert a new line below the current line.    |
| `O`         | Insert a new line above the current line.    |
| `Esc`       | Exit Insert mode and return to Normal mode.  |
| `Ctrl-o`    | Temporarily enter Normal mode for one command.|

---

#### **Visual Mode**
| **Key**     | **Action**                                   |
|-------------|----------------------------------------------|
| `v`         | Enter character-wise Visual mode.            |
| `V`         | Enter line-wise Visual mode.                 |
| `Ctrl-v`    | Enter block-wise Visual mode.                |
| `y`         | Yank the selected text.                      |
| `d`         | Delete the selected text.                    |
| `~`         | Toggle case for the selected text.           |
| `>`         | Indent the selected text.                    |
| `<`         | Un-indent the selected text.                 |
| `Esc`       | Exit Visual mode.                            |

---

#### **Command-Line Mode**
| **Key**         | **Action**                                           |
|------------------|------------------------------------------------------|
| `:`             | Enter Command-line mode (e.g., `:w`, `:q`).          |
| `/pattern`      | Search forward for `pattern`.                        |
| `?pattern`      | Search backward for `pattern`.                       |
| `Ctrl-p`        | Cycle backward through command history.              |
| `Ctrl-n`        | Cycle forward through command history.               |
| `Esc` or `Ctrl-c`| Exit Command-line mode without executing a command.  |

---

#### **Ex Mode**
- Ex mode is an advanced command-line mode that allows batch processing of commands.
- **Start Ex Mode**: `Q`
- **Exit Ex Mode**: `:visual`

---

### **2. Advanced Custom Key Mappings**

#### **Leader Key**
The `<leader>` key is a customizable prefix for user-defined shortcuts. By default, `<leader>` is `\`. You can set it to something easier, like `,`:

```vim
let mapleader = ","
```

---

#### **Custom Key Mapping Examples**

**Buffer and Window Management:**
```vim
nnoremap <leader>n :bnext<CR>      " Switch to the next buffer
nnoremap <leader>p :bprev<CR>      " Switch to the previous buffer
nnoremap <leader>hs :split<CR>     " Horizontal split
nnoremap <leader>vs :vsplit<CR>    " Vertical split
```

**Quick Save and Quit:**
```vim
nnoremap <leader>w :w<CR>          " Save file
nnoremap <leader>q :q<CR>          " Quit Vim
nnoremap <leader>x :wq<CR>         " Save and quit
```

**Search Highlight Toggle:**
```vim
nnoremap <leader>h :nohlsearch<CR> " Turn off search highlights
```

**Toggle Relative Line Numbers:**
```vim
nnoremap <leader>r :set relativenumber!<CR>
```

---

### **3. Steps to Customize Key Mappings**

1. **Edit Your `.vimrc` File**
   Open your Vim configuration file:
   ```bash
   vim ~/.vimrc
   ```

2. **Add Custom Mappings**
   Example:
   ```vim
   let mapleader = ","               " Set leader key to comma
   nnoremap <leader>w :w<CR>         " Map <leader>w to save
   nnoremap <leader>q :q<CR>         " Map <leader>q to quit
   ```

3. **Save and Reload Vim**
   Save your `.vimrc` file and reload it in Vim:
   ```vim
   :source ~/.vimrc
   ```

---

### **4. Tips for Mapping Keys**

- Use `noremap` instead of `map` to avoid recursive mappings.
- Use mode-specific mappings:
  - `noremap` for all modes.
  - `nnoremap` for Normal mode.
  - `vnoremap` for Visual mode.
  - `inoremap` for Insert mode.

---

### **5. Full Example `.vimrc`**
Here’s a complete sample `.vimrc` for a beginner-friendly workflow:

```vim
" Set leader key
let mapleader = ","

" Basic settings
set number                   " Show line numbers
set relativenumber           " Show relative line numbers
set ignorecase               " Ignore case in searches
set smartcase                " Override ignorecase if search contains uppercase

" Key mappings
nnoremap <leader>w :w<CR>    " Save file
nnoremap <leader>q :q<CR>    " Quit Vim
nnoremap <leader>x :wq<CR>   " Save and quit
nnoremap <leader>n :bnext<CR> " Go to the next buffer
nnoremap <leader>p :bprev<CR> " Go to the previous buffer
nnoremap <leader>h :nohlsearch<CR> " Turn off search highlights
nnoremap <leader>r :set relativenumber!<CR> " Toggle relative line numbers

" Window management
nnoremap <leader>hs :split<CR>   " Horizontal split
nnoremap <leader>vs :vsplit<CR>  " Vertical split
```

---

## Vim's **help system**

---

### **How to Access Vim Help**
1. **Basic Command to Open Help**:
   - Use `:help` to access Vim's built-in help.
     ```vim
     :help
     ```
   - This opens the help file, showing an overview of available help topics.

2. **Get Help for a Specific Command**:
   - To learn about a specific Vim command, type `:help` followed by the command name:
     ```vim
     :help <command>
     ```
   - Examples:
     ```vim
     :help :w           " Help for the :w (write) command
     :help i            " Help for the Insert mode command
     :help gg           " Help for the 'gg' navigation command
     ```

3. **Search for Help Topics**:
   - To search for a topic, type `/` in the help window and enter your query.
     Example: `/split` to find all mentions of window splitting.

---

### **Common Help Topics**
Here are some common topics you might look for in Vim help:
- **Basic Usage**: `:help user-manual`
- **Modes**: `:help vim-modes`
- **Buffers, Windows, and Tabs**: `:help windows`, `:help buffers`, `:help tabs`
- **Search and Replace**: `:help search`, `:help substitute`
- **Key Mappings**: `:help map`, `:help keycodes`
- **Options**: `:help options`
- **Regular Expressions**: `:help pattern`

---

### **Navigating the Help System**
1. **Jump to Linked Topics**:
   - Move the cursor over a highlighted topic (looks like `|topic|`) and press `Ctrl-]` to jump to that section.

2. **Go Back**:
   - Press `Ctrl-o` to return to the previous location in the help.

3. **List Help Tags**:
   - Use `:helptags` to generate or regenerate the help tags if custom plugins are installed.

4. **Search Tags**:
   - Use `:help` followed by a keyword:
     ```vim
     :help buffers
     ```

---

### **Help for Plugins**
If you’ve installed plugins, their documentation is usually included in the help system:
1. Open the help for the plugin by typing:
   ```vim
   :help <plugin_name>
   ```
2. If this doesn’t work, you may need to regenerate help tags:
   ```vim
   :helptags ~/.vim/pack/plugins/start/<plugin_directory>/doc
   ```

---

### **Cheat Sheet for Vim Help**
| **Command**                    | **Description**                                   |
|--------------------------------|---------------------------------------------------|
| `:help`                        | Open the general help system.                    |
| `:help <command>`              | Get help for a specific command.                 |
| `:help <topic>`                | Get help for a specific topic.                   |
| `Ctrl-]`                       | Jump to the tag under the cursor.                |
| `Ctrl-o`                       | Jump back to the previous location in help.      |
| `/search_term`                 | Search for a term in the current help file.      |
| `:helptags <directory>`        | Generate help tags for a plugin or directory.    |
| `:help user-manual`            | Open the Vim user manual (great for beginners).  |
| `:help quickref`               | Open the quick reference guide for Vim.          |
| `:help faq`                    | Frequently Asked Questions about Vim.            |

---

### **Difference from Emacs Help**
- **Emacs** has a more interactive help system (e.g., `C-h k` to describe a key).
- **Vim** uses `:help` combined with tags and commands. It's fast but requires learning its structure.

If you’d like an Emacs-like "describe key" feature, plugins like [WhichKey](https://github.com/folke/which-key.nvim) can mimic that behavior in Vim/Neovim.

---

## Vim Plugin
Installing and uninstalling plugins in Vim is relatively straightforward. You can manage plugins manually or use a **plugin manager**, which simplifies the process. Here's a guide to both approaches:

---

### **1. Manual Installation**
In this method, you directly place plugin files in Vim's `~/.vim` directory.

#### **Installing Plugins Manually**
1. **Download the Plugin**:
   - Go to the plugin's GitHub page or website.
   - Download or clone the plugin repository.

   Example for cloning:
   ```bash
   git clone https://github.com/preservim/nerdtree.git ~/.vim/pack/vendor/start/nerdtree
   ```

2. **Place the Files**:
   - Place the plugin files inside `~/.vim/pack/vendor/start/` (or a similar directory structure).

   Example:
   ```
   ~/.vim/pack/vendor/start/nerdtree/
   ```

3. **Restart Vim**:
   - Open Vim and the plugin will load automatically.

#### **Uninstalling Plugins Manually**
1. **Delete the Plugin Directory**:
   ```bash
   rm -rf ~/.vim/pack/vendor/start/<plugin_name>
   ```

2. **Restart Vim**:
   - The plugin will no longer load.

---

### **2. Using a Plugin Manager**
A plugin manager simplifies installation, updates, and uninstallation. Popular plugin managers include **vim-plug**, **Vundle**, and **Pathogen**.

#### **Installing Plugins with vim-plug (Recommended)**
1. **Install vim-plug**:
   - Download the vim-plug script:
     ```bash
     curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
         https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
     ```

2. **Edit `.vimrc` to Include Plugins**:
   - Add the following to your `.vimrc`:
     ```vim
     call plug#begin('~/.vim/plugged')

     " List your plugins here
     Plug 'preservim/nerdtree'          " Example: NERDTree
     Plug 'junegunn/fzf', { 'do': './install --all' } " Example: fzf
     Plug 'tpope/vim-surround'          " Example: Surround

     call plug#end()
     ```

3. **Install Plugins**:
   - Open Vim and run:
     ```vim
     :PlugInstall
     ```

4. **Update Plugins**:
   - Run:
     ```vim
     :PlugUpdate
     ```

5. **Uninstall Plugins**:
   - Remove the plugin entry from your `.vimrc`.
   - Open Vim and run:
     ```vim
     :PlugClean
     ```

---

#### **Installing Plugins with Vundle**
1. **Install Vundle**:
   - Clone the Vundle repository:
     ```bash
     git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
     ```

2. **Edit `.vimrc` to Include Plugins**:
   - Add the following to your `.vimrc`:
     ```vim
     set nocompatible
     filetype off
     set rtp+=~/.vim/bundle/Vundle.vim
     call vundle#begin()

     " List your plugins here
     Plugin 'preservim/nerdtree'
     Plugin 'tpope/vim-surround'

     call vundle#end()
     filetype plugin indent on
     ```

3. **Install Plugins**:
   - Open Vim and run:
     ```vim
     :PluginInstall
     ```

4. **Uninstall Plugins**:
   - Remove the plugin entry from your `.vimrc`.
   - Open Vim and run:
     ```vim
     :PluginClean
     ```

---

### **3. Comparing Plugin Managers**

| Feature         | **vim-plug**                       | **Vundle**                          | **Pathogen**                      |
|------------------|------------------------------------|--------------------------------------|------------------------------------|
| Installation     | Simple and fast                   | Slower and older                    | Minimalistic                      |
| Speed            | Parallel installation/update      | Sequential installation             | No built-in installation mechanism|
| Maintenance      | Actively maintained               | Less active                         | Stable but dated                  |
| Examples         | `Plug 'user/repo'`                | `Plugin 'user/repo'`                | Manually manage plugins           |

**Recommendation**: Use **vim-plug** for modern and efficient plugin management.

---

### **4. Verifying Plugins**
After installing a plugin:
- Use `:scriptnames` to list all scripts/plugins loaded by Vim.
- Search for your plugin in the list to ensure it’s active.

---

### **5. Example: Installing NERDTree with vim-plug**
1. Add this to `.vimrc`:
   ```vim
   call plug#begin('~/.vim/plugged')
   Plug 'preservim/nerdtree'
   call plug#end()
   ```

2. Install NERDTree:
   ```vim
   :PlugInstall
   ```

3. Open NERDTree:
   ```vim
   :NERDTreeToggle
   ```

4. To uninstall:
   - Remove the `Plug 'preservim/nerdtree'` line from `.vimrc`.
   - Run:
     ```vim
     :PlugClean
     ```

---

## Vim Plugin Folder

No, not all plugins are installed to the `~/.vim/pack/vendor/start` folder by default. The location depends on how plugins are managed. Let me explain the different scenarios:

---

### **1. Manual Plugin Installation**
If you install plugins manually without a plugin manager, the recommended directory structure is:
- **`~/.vim/pack/vendor/start/`**: Plugins in this folder are **automatically loaded** when Vim starts.
- **`~/.vim/pack/vendor/opt/`**: Plugins in this folder are **optional** and need to be explicitly loaded using:
  ```vim
  :packadd <plugin_name>
  ```

You can organize plugins into different "packages" by changing `vendor` to a custom name (e.g., `my_plugins`).

---

### **2. Plugin Managers and Installation Locations**

#### **Using `vim-plug`**
- **Default location**: `~/.vim/plugged/`
  - vim-plug installs plugins in the `~/.vim/plugged/` directory.
  - Plugins in this directory are loaded automatically when configured in the `.vimrc` file using `Plug '<repo>'`.
  - For example:
    ```vim
    call plug#begin('~/.vim/plugged')
    Plug 'preservim/nerdtree'
    call plug#end()
    ```

#### **Using Vundle**
- **Default location**: `~/.vim/bundle/`
  - Vundle installs plugins in the `~/.vim/bundle/` directory.
  - For example:
    ```vim
    Plugin 'preservim/nerdtree'
    ```

#### **Using Pathogen**
- **Default location**: `~/.vim/bundle/`
  - Pathogen automatically loads all plugins in the `~/.vim/bundle/` directory.
  - For example:
    ```bash
    git clone https://github.com/preservim/nerdtree.git ~/.vim/bundle/nerdtree
    ```

---

### **3. Recommended Directory Structure**
If you don’t use a plugin manager, the `pack` directory is the modern, built-in way to manage plugins. Here’s the structure:

```plaintext
~/.vim/
├── pack/
│   ├── vendor/
│   │   ├── start/   (Automatically loaded plugins)
│   │   ├── opt/     (Optional plugins)
```

1. **Install plugins into `start/`** if you want them loaded automatically.
2. **Install plugins into `opt/`** if you want to load them manually using `:packadd`.

---

### **4. How to Check Where Plugins Are Installed**
To see where Vim is loading a specific plugin:
1. Open Vim and run:
   ```vim
   :scriptnames
   ```
2. This lists all scripts/plugins loaded by Vim, including their paths.

---

### **5. Does Everyone Use `~/.vim/pack/vendor/start`?**
No. The directory `~/.vim/pack/vendor/start` is just a convention for manual plugin installation. Plugin managers like vim-plug or Vundle use their own directories (e.g., `~/.vim/plugged/` or `~/.vim/bundle/`).

---

### **6. Can Plugin Managers Use `~/.vim/pack/vendor/start`?**
Yes, you can configure plugin managers like `vim-plug` to use `~/.vim/pack/vendor/start`. For example:

- For `vim-plug`, set the directory in `.vimrc`:
  ```vim
  call plug#begin('~/.vim/pack/vendor/start')
  Plug 'preservim/nerdtree'
  call plug#end()
  ```

- This will install plugins directly into `~/.vim/pack/vendor/start`.

---

### **Conclusion**
- **Default Plugin Folder**: `~/.vim/pack/vendor/start` is for manually installed plugins.
- **Plugin Managers**: Each uses its own directory (`~/.vim/plugged/`, `~/.vim/bundle/`, etc.).
- **Flexible Configuration**: Plugin managers like vim-plug can be configured to use the `~/.vim/pack/` structure.


