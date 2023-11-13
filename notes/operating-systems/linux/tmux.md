# Tmux
- https://www.howtogeek.com/671422/how-to-use-tmux-on-linux-and-why-its-better-than-screen/
- `ctrl + B` - bind key (BK)
- `bind key + ?` - help

## Sessions
- `tmux` - new session
- `tmux new -s name1` - new named session
- `tmux ls` - list sessions
- `BK, S` - list session (interactive)
- `BK, D` - detach session
- `tmux attach-session` - attach last session
- `tmux attach-session -t name1` - attach named session
- `BK, X` or `ctrl + D` - exit session
- `tmux kill-server` - gracefully kill all sessions

## Windows
..

## Panes
- `BK, %` - vertical split
- `BK, "` - horizontal split
- `BK, arrows` - move between panes
- `BK, Q` - show window panes
- `BK, X` or `ctrl + D` - close pane
- `BK, Z` - toggle zoom pane