# csswrangler

A css manipulation library for node.js

Based on the CSS parser included with [PEG.js](https://github.com/dmajda/pegjs)

Beware - very rough at the mo, needs work!

## Usage:

    var csswrangler = require('/wherever/csswrangler/csswrangler.js');
    var css = [
        '/* blah */',
        'p {',
        '  text-align: center;',
        '  /* blah */',
        '}',
        '/* blah */',
        'my-div h1 {',
        '  color: red;',
        '}',
       ].join('\n');

    var tree = csswrangler.parse(css);
    console.log(tree.print() === css);

### E.g. adding scoping:

    tree = csswrangler.parse(css);
    var selector = new csswrangler.Selector('.my-class');
    tree.findAll('whole_selector').forEach(function (whole_selector) {
        whole_selector.insertAfterSelectors(['*', 'html', 'body'], selector);
    });
    console.log(tree.print());

### E.g. stripping comments:

    tree = csswrangler.parse(css);
    tree.findAll('comment').forEach(function (n) { n.remove();});
    console.log(tree.print());





