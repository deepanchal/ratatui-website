---
title: Spawn External Editor (Vim)
sidebar:
  order: 9
  label: Spawn External Editor (Vim)
---

You can spawn an external editor like Vim, Neovim, or Nano using the following code. We will be
using Ratatui's [`component`](https://github.com/ratatui-org/templates/tree/main/component) template
as the starter code.

## Add a New Action

First, add a new action `EditFile` to the `action.rs` file:

```rust
// action.rs
{{ #include @code/how-to-spawn-vim/src/action.rs:action }}
```

## Add Action Handler

Next, we will add the `EditFile` action handler in `app.rs`. This handler performs the following
steps to spawn Vim:

1. Disables raw mode and exits the alternate screen by calling `tui.exit()`.
2. The `tui.exit()` call also pauses the event loop that handles any key or mouse events.
3. Spawns Vim using `std::process::Command`.
4. Waits for Vim to exit.
5. Re-enables raw mode and enters the alternate screen again.

```rust
// app.rs
{{ #include @code/how-to-spawn-vim/src/app.rs:run__action_EditFile }}
```

## Add Key Binding

Next, we will add a simple `v` key binding to `components/home.rs` to trigger the `EditFile` action
and spawn Vim. When you press `v` in your app, it will launch Vim to edit the `/tmp/a.txt` file. You
can choose an editor of your choice by replacing `std::process::Command::new("vim")` with
`std::process::Command::new("nvim")` or `std::process::Command::new("nano")`.

```rust
// components/home.rs
{{ #include @code/how-to-spawn-vim/src/components/home.rs:handle_key_events }}
```

## Result Files

The full code for this tutorial is available to view at
<https://github.com/ratatui-org/ratatui-website/tree/main/code/how-to-spawn-vim>

```rust collapsed title="tui.rs (click to expand)"
// tui.rs
{{ #include @code/how-to-spawn-vim/src/tui.rs }}
```

```rust collapsed title="action.rs (click to expand)"
// action.rs
{{ #include @code/how-to-spawn-vim/src/action.rs }}
```

```rust collapsed title="app.rs (click to expand)"
// app.rs
{{ #include @code/how-to-spawn-vim/src/app.rs }}
```

```rust collapsed title="components/home.rs (click to expand)"
// components/home.rs
{{ #include @code/how-to-spawn-vim/src/components/home.rs }}
```
