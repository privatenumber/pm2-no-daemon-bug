# pm2-no-daemon-bug

> This repro documents a bug in pm2 that adds the pm2 args to the script when using --no-daemon and clustering only at first run

### Two things that fixes it:
- Remove clustering (`instances: 1`)
- Not using `--no-daemon`
- Second `pm2 start` after `pm2 stop` (However, we can reproduce the first run by deleting `~/.pm2` -- behind `npm run stop-reset`)

### First run:
```
19:37:22 0|project  | [ '/Users/user_name/.nvm/versions/node/v8.12.0/bin/node',
19:37:22 0|project  |   '/Users/user_name/Documents/Gits/privatenumber/pm2-no-daemon-bug/node_modules/pm2/lib/ProcessContainerLegacy.js',
19:37:22 0|project  |   'start',
19:37:22 0|project  |   'ecosystem.config.js',
19:37:22 0|project  |   '--no-daemon',
19:37:22 0|project  |   'start' ]
```

### Second run:
```
19:38:00 0|project  | [ '/Users/osame/.nvm/versions/node/v8.12.0/bin/node',
19:38:00 0|project  |   '/Users/osame/Documents/Gits/privatenumber/pm2-no-daemon-bug/node_modules/pm2/lib/ProcessContainerLegacy.js',
19:38:00 0|project  |   'start' ]
```