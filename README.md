# jade-injected

These mixins are for injecting child blocks in the parent mixin. Please, mind that this solution is temporary and I'm really looking forward to the Jade's 2.x.x release with a support for Multiple Blocks in Mixins.


## Installation
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

## Warnings

Since it's a temporary fix, there are some limitations.

### Do not use a `block` if `+injected` called in mixin

```jade
mixin parrent()
    +injected: block
```

### Do not use data cycles (hopefully will be fixed soon)
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

### Initializing the inject into mixin
```jade
+injected: block
```

### Use block
Insert the block. Mind that if you call use mixin, you need to check if there is a block.
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
Injected blocks into parrent mixin
```jade
+parrent
    +inject('box')
        | content

```
