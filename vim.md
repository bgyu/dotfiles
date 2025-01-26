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

