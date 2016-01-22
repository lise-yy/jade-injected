# jade-injected

Mixins for inject child blocks in parent mixin. This solution is temporary. I'm really looking forward to the release version 2.x.x jade, which is added support for Multiple Blocks in Mixins. In the meantime, we have to make do with what is.


## Install
Clone jade-injected to your project
```cmd
git clone git://github.com/pavel-yagodin/jade-injected.git
```
Include jade file to your project
```jade
include jade-injected/jade-injected
```

## NPM
### https://www.npmjs.com/package/jade-injected

## Usage
Mixin
```jade
mixin parrent()
    +injected: block
    .parrent
        +if('top')
            .position-top
                +use('top')
        +if('box')
            .position-boxes
                +each('box')
                    .position-box
                        +use('box')
        +else('box')
            .position-empty
                | Box is not inject

```
Usage
```jade
    +parrent()
        +inject('top')
            | Text for top position
        +inject('box')
            | Text for first box
        +inject('box')
            | Text for second box
```
Result
```html
<div class="parrent">
    <div class="position-top">Text for top position</div>
    <div class="position-boxes">
        <div class="position-box">Text for first box</div>
        <div class="position-box">Text for second box</div>
    </div>
</div>
```

## Wraning

Since it's a temporary fix, there are some limitations.

### Do not use a `block` if `+injected` called in mixin.

```jade
mixin parrent()
    +injected: block
```

### Do not use data cycles (hopefully should be fixed soon)
```json
this expamle has error
```
```jade
+parrent()
    +inject('top')
        | Text for top position
    each item in boxes
        +inject('box')
            =item
```


## Mixins

### Initialization inject into mixin
```jade
+injected: block
```

### Use block
Insert block to place. Please, if you call use mixin, check avariable.
```jade
+use(blockName)
```

### If-Else
```jade
+if(blockName)
    +use(blockName)
+else(blockName)
    =blockName + ' is not injected'

```

### Each
Each injected blocks
```jade
+each('box')
    +use('box')


```
### Inject
Injected blocks intro parrent mixin
```jade
+parrent
    +inject('box')
        | content

```
