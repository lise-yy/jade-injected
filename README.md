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
## Usage
Mixin
```jade
mixin parrent()
    +injected: block
    .parrent
        +if('top')
            .position-top
                +use('top')
        .position-boxes
            +each('box')
                .position-box
                    +use('box')
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
