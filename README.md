# doDex, a multi-purpose rolodex widget for menuing and other information

## Getting Started

The widget can be attached to any HTML page.

1. Add to your html document using defaults.

```html
    <link rel="stylesheet" href="(location)/dodex.min.css">

    <!-- JSONEditor is optional - JSONEditor css for editing private content in JSON files -->
    <link href="(location)/jsoneditor/dist/jsoneditor.min.css" rel="stylesheet" type="text/css">
    <style>
      /* Size and location of JSONEditor window */
      .editor {
         width: 80%; height: 400px; position: fixed; bottom: 0; left: 0;
      }
    </style>

    <body>
      <div class="dodex--open">
        <img src="(location)/dodex/images/dodex_g.ico">
      </div>

      <!-- JSONEditor is Optional - container for the frontend JSON editor - will be positioned based on .editor class -->
      <div id="jsoneditor" class="editor"></div>
      <!-- Note; dodex-input will handle the implementation - see the input popup -->
      <script src="(location)/jsoneditor/dist/jsoneditor.min.js"></script>

      <script src="(location)/dodex.min.js" type="text/javascript"></script>
      <script src="(location)/dodex-input.min.js" type="text/javascript"></script>
      <script src="(location)/dodex-mess.min.js" type="text/javascript"></script>
      <script>
            doDex.init({
               input: doDexInput, // "private: none" is default so no popup input form
               mess: doDexMess    // defaults to "server: localhost:3087" for websockets
            });
      </script>
    </body>
 ```

2. Modifying defaults by adding inline javascript to page.

```html
    <script>
         var dodex = window.doDex;      // global variable
         var input = window.doDexInput; // global variable
         var mess = window.doDexMess; // global variable

         /* Card content can be customized - returns an object
           This content is used for cards A-Z and static card 27
         */
         dodex.setContentFile("(location)/content.js");

         // Change size and or position - returns a Promise
         dodex.init({
            width:375,
            height: 200,
            top: "100px",
            left: "50%",
            input: input,        // required if using frontend content load
            private: "partial",  // frontend load of private content, "none", "full", "partial"(only cards 28-52) - default none
            replace: true,       // append to or replace default content - default false(append only)
            mess: mess,          // required for dodex messaging client
            server: "localhost:3087" // see node_modules/dodex-mess/server for details on demo server
            })

         // Add up to 24 additional cards. Card # must start at 28.
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

* Using es6 syntax

```javascript
       import dodex from "dodex";
```

* Using commonjs syntax

```javascript
       var dodex = require("dodex").default;
```

* Changing default behavior in an application module

```javascript

       import dodex from "dodex";
       import input from "dodex-input"
       import mess from "dodex-mess"
       import jsonEditor from "jsoneditor"
       window.JSONEditor = jsonEditor;

       /* This content is used for cards A-Z and static card 27 */
       dodex.setContentFile("<location>/content.js");

       dodex.init({
          width: 375,
          height: 200,
          left: "50%",
          top: "100px",
          input: input,        // required if using frontend content load
          private: "partial",  // frontend load of private content, "none", "full", "partial"(only cards 28-52) - default none
          replace: true,       // append to or replace default content - default false(append only)
          mess: mess,          // requireed if using messaging client.
          server: "localhost:3087"  // default demo server - see node_modules/dodex-mess/server
       })
       .then(function () {
           /* Add up to 24 additional cards. */
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

   __Note;__ The window scoped "dodexContent" is required to load content at initialization. This allows content without using a module.(dodex.setContentFile). The additional card content as well as content loaded from the front-end Input module, use plain objects.

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
1. Double-Click on bottom static card or dials to popup the front-end load file form.
1. Double-Click again to close or click close button.

__Note;__ Firefox works best by only clicking the tabs.

### Prerequisites

If using dodex-input, browser must support the "indexedDB" storage feature. To clear content from indexedDB, execute from your browser's dev-tools console; `indexedDB.deleteDatabase("dodex")`. Or use the dodex-input popup to remove personal content stored in "indexedDB".

### Installing

1. `npm install dodex --save` or download from <https://github.com/DaveO-Home/dodex>.
1. `npm install dodex-input --save` or download from <https://github.com/DaveO-Home/dodex-input>.
1. `npm install dodex-mess --save` or download from <https://github.com/DaveO-Home/dodex-mess>.
1. `npm install jsoneditor --save` or download from <https://github.com/josdejong/jsoneditor>(this is optional).
1. Optionally copy `node_modules/dodex/` javascript, css and images to appropriate directories; If using a bundler like browserify, you may only need to copy the content.js(or create your own) and images.
1. You can use the Java/rxJava asynchronous server ```dodex-vertx``` to serve dodex.
1. Also, dodex-mess has a node/koa javascript server ```node_modules/dodex-mess/server``` to serve dodex.

__Note;__ Content can also be loaded from a `JSON` file. See dodex-input README for details on the frontend JSON editor.

Here's an example of dodex loaded in a `bootstrap` environment (view on GitHub <https://github.com/DaveO-Home/dodex>).

![dodex](./images/dodex.png?raw=true)

## Deployment

See getting started.

## Test

1. Open in any browser or start a server where node_modules directory is visible.
1. Load `node_modules/dodex/test/index.html`

## Built With

* [SASS](https://sass-lang.com/) - css build
* [Javascript](https://www.javascript.com//) - language
* [Rollup](https://rollupjs.org/) - bundler

## Authors

* *Initial work* - [DaveO-Home](https://github.com/DaveO-Home)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
