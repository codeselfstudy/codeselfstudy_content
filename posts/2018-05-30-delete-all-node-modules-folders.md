title: How to Delete All node_modules Directories
date: 2018-05-30 14:58
category: Node.js
slug: how-to-delete-all-node_modules-folders
authors: Josh

I found that deleting all the `node_modules` directories on my computer freed up about 16 GB of space on my hard drive. The following command will recursively delete them:

```
find . -name 'node_modules' -type d -prune -exec rm -rfv '{}' +
```

More info [here](https://stackoverflow.com/a/43561012).
