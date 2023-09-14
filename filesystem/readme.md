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
  
![alt text](https://github.com/graphs4value/refinery-tutorials/blob/main/filesystem/fig1.png)

- Add some statements about a partial model:

```
class FileSystem {
    contains File[1] root
}
class File.
class Dir extends File {
    contains File[] element
}

Dir(resources).
element(resources,img).
File(img).

scope node = 10.
```

![alt text](https://github.com/graphs4value/refinery-tutorials/blob/main/filesystem/fig2.png)

### Partial models
- Notice that the instance model elements are coexisting with ```<type>::new``` nodes representing the prototypes of newly created objects.

- Check the disabled `equals` and `exist` predicates. check the visual annotation of those predicates in the visualization (dashed line, shadow).

![alt text](https://github.com/graphs4value/refinery-tutorials/blob/main/filesystem/fig3.png)

### Information merging

- for the object `img`, we did not specified if it is a directory or not. Therefore, it will be typically a folder.

- If we want to state that img is not a directory, we need to a negative statement:
```
!Dir(img).
```
- Statements are merged with respect to the refinement relation of 4-valued logic.
  
- If we add, a statement both negatively and positively, it will create an inconsistency:

```
 element(resources,img).
!element(resources,img).
```

- Inconsistent models parts in a partial model typically make the problem trivially unsatisfiable.
![alt text](https://github.com/graphs4value/refinery-tutorials/blob/main/filesystem/fig4.png)
- However, the model can be saved if the inconsistent part may not exist...

```
!File(File::new).
```

### Default values

- a large amount of statements can be expressed by using ```*```.
- the ```default``` keyword defines lower priority satements that need to be considered unless other statement specifies otherwise. No information merging is happening. 

## Scopes

## Metamodels

```
class FileSystem {
    contains File[1] root
}
class File.
class Dir extends File {
    contains File[0..10] element
}
class Symlink extends File {
    File[1] target
}

Dir(resources).
element(resources,img).
element(resources,link).
target(link,img).


scope node = 10.
```

## Constraints
