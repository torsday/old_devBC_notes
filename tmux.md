# Tmux

## Session Management

>Sessions are useful for completely separating work environments. I have a ‘Work’ session and a ‘Play’ session; in ‘Work’ I keep everything open that I need during my day-to-day development while in ‘Play’ I keep open current open-source gems or other work I hack on at home.

### create a new session

```
tmux new -s session_name
```

### attach to an existing session

```
tmux attach -t session_name
```

### switch to an existing session

```
tmux switch -t session_name
```

### list existing sessions

```
tmux list-sessions
```

### detach the current session

```
tmux detach (prefix + d)
```

## Windows

>Tmux has a tabbed interface but it calls its tabs “Windows”. To stay organized I rename all the windows I use; if I’m hacking on a gem I’ll name the window that gem’s name. The same thing goes for client applications. That way I can recognize windows by context and not what application it’s running.

### create

```
tmux new-window (prefix + c)
```

### move to widnow based on index

```
tmux select-window -t :0-9 (prefix + 0-9)
```

### rename current

```
tmux rename-window (prefix + ,)
```

## Panes

>Panes take my development time from bland to awesome. They’re the reason I was able to uninstall MacVim and develop solely in iTerm2. I don’t have to switch applications to switch contexts (editing, reading logs, IRB, etc.) - everything I do, I do in a terminal now. People argue that OS X’s Cmd+Tab is just as fast, but I don’t think so.

### vertical two

```
tmux split-window (prefix + ")
```

### horizontal two

```
tmux split-window -h (prefix + %)
```

### swap pane with another in specified direction

```
tmux swap-pane -[UDLR] (prefix + { or })
```

### select pane in specified direction

```
tmux select-pane -[UDLR]
```

### select next pane (numerical order)

```
tmux select-pane -t :.+
```

## Helpful Commands

### list every bound key and it's tmux command

```
tmux list-keys
```

### list out every tmux command and it's arguments

```
tmux list-commands
```

### list every session, window, pane...

```
tmux info
```

### reload current tmux config

```
tmux source-file ~/.tmux.conf
```

## Must have in tmux config

```
# remap prefix to Control + a
set -g prefix C-a
unbind C-b
bind C-a send-prefix

# force a reload of the config file
unbind r
bind r source-file ~/.tmux.conf

# quick pane cycling
unbind ^A
bind ^A select-pane -t :.+
```

## Workflow

>During the day, I’ll work on one or two Rails apps, work on my dotfiles, run irssi, and maybe run vim in another window to take notes for myself. As I mentioned, I run all of this inside one tmux session (named work) and switch between the different windows throughout the day.

>When I’m working on any Ruby work specifically, I’ll have a 75%/25% vertical split for vim and a terminal so I can run tests, interact with git, and code. If I run tests or ‘git diff’ and want to see more output than the 25% allots me, I’ll use tmux to swap the panes and then move into copy mode to see whatever I need to see.

>Finally, I run iTerm2 in full-screen mode. Switching between OS X apps for an editor and a terminal is for chumps!


## References

- [A Tmux Crash Course](http://robots.thoughtbot.com/post/2641409235/a-tmux-crash-course)
