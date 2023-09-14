# Filesystem tutorial

The goal of this tutorial is to give a brief overview of the partial modeling and model generation features of the Refinery framework. The running example will be the modeling of files, directories, and repositories.

## Partial models

### Types and Relations

- First, let us itroduce some basic types: `Dir`,  `File` and `FileSystem`, there are relation between them `element` and `root`. There is a `there is a scope expression at the end, let us ignore it for now.

```
class FileSystem {
    contains File[1] root
}
class File {}
class Dir extends File {
    contains File[] element
}

scope node = 10.
```

- Notice that the syntax is essentially identical to XCore.
- Review the partial model visualization. You should get something like this:



## Scopes

## Metamodels

## Instance models

## Constraints
