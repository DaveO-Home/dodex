# doDex, a multi-purpose rolodex widget for menuing and other information

## Getting Started

The widget can be attached to any HTML page.

1. Add to your html document using defaults.

```html
    <link rel="stylesheet" href="<location>/dodex.min.css">
    <body>
      <div class="dodex--open">
        <img src="<location>/dodex/images/dodex_g.ico">
      </div>
      <script src="<location>/dodex.min.js" type="text/javascript"></script>
    </body>
 ```

2. Modifying defaults by adding inline javascript to page.

```javascript
    <script>
        var dodex = window.doDex; // global variable

        /* Card content can be customized - returns an object
           This content is used for cards A-Z and static card 27 */
        dodex.setContentFile("<location>/content.js");

        // Change size and or position - returns a Promise
        dodex.init({width:375; height: 200; top: "100px"; left: "50%"})

        // Add up to 26 additional cards. Card # must start at 28.
        .then(function () {
            for (var i = 0; i < 3; i++) {
              dodex.addCard({/*see custom content section*/});
            }
            /* Auto display of widget */
            dodex.openDodex();
        });
    </script>
```

3. Loading as a module.

      Using es6 syntax

```javascript
       import dodex from "dodex";
```

      Using commonjs syntax

```javascript
       var dodex = require("dodex").default;
```

      Changing default behavior in an application module

```javascript

       import dodex from "dodex";
       /* This content is used for cards A-Z and static card 27 */
       dodex.setContentFile("<location>/content.js");

       dodex.init({
          width: 375,
          height: 200,
          left: "50%",
          top: "100px"
       })
       .then(function () {
           /* Add up to 26 additional cards. */
           for(var i = 0; i < 1; i++) {
               dodex.addCard(content);
           }
           /* Auto display of widget */
           dodex.openDodex();
      });

      var content = {
          cards: {
             card28: {     // Notice, card # starts at 28
               tab: "Me1", // Maximum 3 characters
               front: {
                  content: `<h1>My Personal Stuff</h1>`
               },
               back: {
                  content: `<h1>More personal Stuff</h1>`
               }
          }}}

```

4. Adding content to the dodex cards(content can be from a javascript or JSON file).

       Use the following as a javascript template. You only need to include cards with content. See node_modules/dodex/data for examples.

```javascript
        dodexContent = {
          cards: {
             card1: {
               tab: "A",
               front: {
                  content: ""
               },
               back: {
                  content: ""
               }
             },
             card2: {
                tab: "B",
                front: {
                   content: ""
                },
                back: {
                   content: ""
                }
             },
             card3: {
                tab: "C",
                front: {
                   content: `<h1>Best's Contact Form</h1><a href="#!contact"><i class="fa fa-fw fa-phone"></i>Contact</a>`
                },
                back: {
                   content: `<h1>Lorem Ipsum</h1><a href="https://www.yahoo.com" target="_">Yahoo</a>`
                }
             },
             card27: {
                tab: "",
                front: {
                   content: ""
                },
                back: {
                   content: `<h1 style="font-size: 14px;">
                      <svg height="18" width="17" style="font-family: 'Open Sans', sans-serif;">
                      <text x="3" y="18" fill="#059">O</text><text x="0" y="15" fill="#059">D</text></svg> doDex</h1>`
                }
             }
          }
        }
```

### Operation

1. Clicking on the dodex icon will toggle the widget's visibility.
1. Click a tab to page to desired card.
1. Click the face or back of a card to flip current cards.
1. Enter a dial with mouse and with mouse down slowly move up or down to flip cards.

__Note;__ Firefox works best by only clicking the tabs.

### Prerequisites

An Npm based javascript project.

### Installing

1. `npm install dodex`
2. Optionally copy `node_modules/dodex/` javascript, css and images to appropriate directories; If using a bundler like browserify, you may only need to copy the content.js(or create your own) and images.  
__Note;__ Content can also be loaded from a `JSON` file.

Here's an example of dodex loaded in a `bootstrap` environment

![dodex](./images/dodex.png?raw=true)

## Deployment

See getting started.

## Test

1. Start a server where node_modules directory is visible.
1. Load `node_modules/dodex/test/index.html`

## Built With

* [SASS](https://sass-lang.com/) - css build
* [Javascript](https://www.javascript.com//) - language
* [Parcel](https://parceljs.org/) - bundler

## Authors

* *Initial work* - [DaveO-Home](https://github.com/DaveO-Home)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
