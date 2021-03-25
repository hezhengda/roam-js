# roam-js
This repository I will document some roam js extensions that I have found useful.

**Disclaimer**: All the codes that I have shown in here, if not stated, are not my work! It is done by the effort amazing Roam community. If I write some code, then I will state that this is my work.

The list of extensions mentioned on this page is shown in below:
* Roam42
* Highlight pathway
* Zotero-Roam extension (with personal adjustments)

## Roam42

Roam42 is a really great extension for Roam Research, and it is really easy to implement, just add the following javascript code to your [[roam/js]] page, and do the following:

* {{[[roam/js]]}}

(indent, cannot do that in github .... but you know ...)

```javascript
var s = document.createElement('script');
	s.type = "text/javascript";
  	s.src =  "https://roam42.glitch.me/main.js";
  	s.async = true;
document.body.appendChild(s);
```

## Highlight pathway

Highlight pathway is a really create way to find how your idea has developed by tracing its all parent nodes. By using the same procedure as before, and add this javascript code:

```javascript
/*
 * credit to Dhrumil Shah (@wandcrafting) and Robert Haisfield (@RobertHaisfield)
 * for the original concept which was part of their RoamGames submission
 * and can be found at: https://www.figma.com/file/5shwLdUCHxSaPNEO7pazbe/
 *
 */

/* ======= OPTIONS ======== */
/* note: if you change these, reload the page to see the effect */

// BULLET
let scale = 2;
let bulletColor = '#009688';

// LINES
let showLines = true;
let lineWidth = 3;
let lineColor = bulletColor;
let borderRadius = 5;

// HIGHLIGHT REFS
let highlightRefs = true;
let refColor = bulletColor;

/* ======= LIBRARIES ======== */

/*
 * arrive.js
 * v2.4.1
 * https://github.com/uzairfarooq/arrive
 * MIT licensed
 *
 * Copyright (c) 2014-2017 Uzair Farooq
 */

var Arrive=function(e,t,n){"use strict";function r(e,t,n){l.addMethod(t,n,e.unbindEvent),l.addMethod(t,n,e.unbindEventWithSelectorOrCallback),l.addMethod(t,n,e.unbindEventWithSelectorAndCallback)}function i(e){e.arrive=f.bindEvent,r(f,e,"unbindArrive"),e.leave=d.bindEvent,r(d,e,"unbindLeave")}if(e.MutationObserver&&"undefined"!=typeof HTMLElement){var o=0,l=function(){var t=HTMLElement.prototype.matches||HTMLElement.prototype.webkitMatchesSelector||HTMLElement.prototype.mozMatchesSelector||HTMLElement.prototype.msMatchesSelector;return{matchesSelector:function(e,n){return e instanceof HTMLElement&&t.call(e,n)},addMethod:function(e,t,r){var i=e[t];e[t]=function(){return r.length==arguments.length?r.apply(this,arguments):"function"==typeof i?i.apply(this,arguments):n}},callCallbacks:function(e,t){t&&t.options.onceOnly&&1==t.firedElems.length&&(e=[e[0]]);for(var n,r=0;n=e[r];r++)n&&n.callback&&n.callback.call(n.elem,n.elem);t&&t.options.onceOnly&&1==t.firedElems.length&&t.me.unbindEventWithSelectorAndCallback.call(t.target,t.selector,t.callback)},checkChildNodesRecursively:function(e,t,n,r){for(var i,o=0;i=e[o];o++)n(i,t,r)&&r.push({callback:t.callback,elem:i}),i.childNodes.length>0&&l.checkChildNodesRecursively(i.childNodes,t,n,r)},mergeArrays:function(e,t){var n,r={};for(n in e)e.hasOwnProperty(n)&&(r[n]=e[n]);for(n in t)t.hasOwnProperty(n)&&(r[n]=t[n]);return r},toElementsArray:function(t){return n===t||"number"==typeof t.length&&t!==e||(t=[t]),t}}}(),c=function(){var e=function(){this._eventsBucket=[],this._beforeAdding=null,this._beforeRemoving=null};return e.prototype.addEvent=function(e,t,n,r){var i={target:e,selector:t,options:n,callback:r,firedElems:[]};return this._beforeAdding&&this._beforeAdding(i),this._eventsBucket.push(i),i},e.prototype.removeEvent=function(e){for(var t,n=this._eventsBucket.length-1;t=this._eventsBucket[n];n--)if(e(t)){this._beforeRemoving&&this._beforeRemoving(t);var r=this._eventsBucket.splice(n,1);r&&r.length&&(r[0].callback=null)}},e.prototype.beforeAdding=function(e){this._beforeAdding=e},e.prototype.beforeRemoving=function(e){this._beforeRemoving=e},e}(),a=function(t,r){var i=new c,o=this,a={fireOnAttributesModification:!1};return i.beforeAdding(function(n){var i,l=n.target;(l===e.document||l===e)&&(l=document.getElementsByTagName("html")[0]),i=new MutationObserver(function(e){r.call(this,e,n)});var c=t(n.options);i.observe(l,c),n.observer=i,n.me=o}),i.beforeRemoving(function(e){e.observer.disconnect()}),this.bindEvent=function(e,t,n){t=l.mergeArrays(a,t);for(var r=l.toElementsArray(this),o=0;o<r.length;o++)i.addEvent(r[o],e,t,n)},this.unbindEvent=function(){var e=l.toElementsArray(this);i.removeEvent(function(t){for(var r=0;r<e.length;r++)if(this===n||t.target===e[r])return!0;return!1})},this.unbindEventWithSelectorOrCallback=function(e){var t,r=l.toElementsArray(this),o=e;t="function"==typeof e?function(e){for(var t=0;t<r.length;t++)if((this===n||e.target===r[t])&&e.callback===o)return!0;return!1}:function(t){for(var i=0;i<r.length;i++)if((this===n||t.target===r[i])&&t.selector===e)return!0;return!1},i.removeEvent(t)},this.unbindEventWithSelectorAndCallback=function(e,t){var r=l.toElementsArray(this);i.removeEvent(function(i){for(var o=0;o<r.length;o++)if((this===n||i.target===r[o])&&i.selector===e&&i.callback===t)return!0;return!1})},this},s=function(){function e(e){var t={attributes:!1,childList:!0,subtree:!0};return e.fireOnAttributesModification&&(t.attributes=!0),t}function t(e,t){e.forEach(function(e){var n=e.addedNodes,i=e.target,o=[];null!==n&&n.length>0?l.checkChildNodesRecursively(n,t,r,o):"attributes"===e.type&&r(i,t,o)&&o.push({callback:t.callback,elem:i}),l.callCallbacks(o,t)})}function r(e,t){return l.matchesSelector(e,t.selector)&&(e._id===n&&(e._id=o++),-1==t.firedElems.indexOf(e._id))?(t.firedElems.push(e._id),!0):!1}var i={fireOnAttributesModification:!1,onceOnly:!1,existing:!1};f=new a(e,t);var c=f.bindEvent;return f.bindEvent=function(e,t,r){n===r?(r=t,t=i):t=l.mergeArrays(i,t);var o=l.toElementsArray(this);if(t.existing){for(var a=[],s=0;s<o.length;s++)for(var u=o[s].querySelectorAll(e),f=0;f<u.length;f++)a.push({callback:r,elem:u[f]});if(t.onceOnly&&a.length)return r.call(a[0].elem,a[0].elem);setTimeout(l.callCallbacks,1,a)}c.call(this,e,t,r)},f},u=function(){function e(){var e={childList:!0,subtree:!0};return e}function t(e,t){e.forEach(function(e){var n=e.removedNodes,i=[];null!==n&&n.length>0&&l.checkChildNodesRecursively(n,t,r,i),l.callCallbacks(i,t)})}function r(e,t){return l.matchesSelector(e,t.selector)}var i={};d=new a(e,t);var o=d.bindEvent;return d.bindEvent=function(e,t,r){n===r?(r=t,t=i):t=l.mergeArrays(i,t),o.call(this,e,t,r)},d},f=new s,d=new u;t&&i(t.fn),i(HTMLElement.prototype),i(NodeList.prototype),i(HTMLCollection.prototype),i(HTMLDocument.prototype),i(Window.prototype);var h={};return r(f,h,"unbindAllArrive"),r(d,h,"unbindAllLeave"),h}}(window,"undefined"==typeof jQuery?null:jQuery,void 0);

/* ======= CODE ======== */

// Add custom style tag to document for CSS customization
let style = document.createElement('style');
let baseStyle = `
.path-highlighted .rm-bullet .rm-bullet__inner,
.path-highlighted .rm-bullet .rm-bullet__inner--user-icon {
    background-color: ${bulletColor} !important;
    transform: scale(${scale});
}
`
if(highlightRefs) {
  baseStyle += `
.path-highlighted + .roam-block .rm-page-ref,
.path-highlighted + .roam-block .rm-alias {
	color: ${refColor};
}
.path-highlighted + .roam-block .rm-block-ref {
	border-bottom-color: ${refColor};
}
`
}
style.textContent = baseStyle
document.body.appendChild(style);

// Remove classes when block is unfocused
document.leave('textarea.rm-block-input', function(el) {
    let bullets = [].slice.call(document.querySelectorAll('.path-highlighted'));

    bullets.forEach(function(bullet) {
        bullet.classList.remove('path-highlighted');
    })
})

// Show highlighted bullets + path when block is focused
let pathid = 0;
document.arrive('textarea.rm-block-input', function(el) {
    let bullets = [];
    let block = el.closest('.roam-block-container');
    // iterate through parents and get bullet elements
    while(block) {
        bullets.push(block.querySelector('.controls'));
        block = block.parentElement.closest('.roam-block-container')
    }
    
    // bullet styles cannot be applied directly to the element because they are pseudotags
    // so we'll create a style string and add it to the style tag we created earlier
    let bulletStyle = ''
    bullets.forEach(function(bullet, i) {
        let lastBullet = i > 0 ? bullets[i-1] : null
        // give each bullet a special path identifier so that we can target it directly
        if(!bullet.dataset.pathidentifier) { bullet.dataset.pathidentifier = pathid++ }
        
        if(lastBullet != null && showLines == true) {
            let bboxA = lastBullet.getBoundingClientRect()
            let bboxB = bullet.getBoundingClientRect()

            bulletStyle += `
.path-highlighted[data-pathidentifier="${bullet.dataset.pathidentifier}"] .bp3-popover-target::before {
    content: "";
    position: absolute;
    top: 10px; left: 6px;
    width: ${bboxA.x-bboxB.x}px; height: ${bboxA.y-bboxB.y}px;
    border: ${lineWidth}px solid ${lineColor};
    border-right: none;
    border-top: none;
    border-bottom-left-radius: ${borderRadius}px;
    pointer-events: none;
}
`
        }
        
        // highlight bullet
        bullet.classList.add('path-highlighted')
    })
    
    // set content of style tag to include both the base styles from before and the bullet styles we just generated
    style.textContent = baseStyle + bulletStyle;
})
```

## Zotero extension on Roam

Here is the zotero extention on Roam (with my personal modification). It is a powerful extention that connects zotero library with Roam Research, and it will let roam becoming a hub for research and idea-creating.

The details of how to use zotero in Roam have been summarized in here: https://www.youtube.com/watch?v=zYCM5Za1-OA

Here is a great resource (and tutorial) from developer of this extension: https://alix-lahuec.gitbook.io/roam-zotero-data-importer/customization/user-settings

But what I want to focus here is how to modify the metadata output by yourself (this is not clear in the documentation and other tutorials, to my knowledge), so I want to add a bit of explanation in here.

The javascript that I have created is:

```javascript
// To install the extension, simply add the code below :
var s = document.createElement("script");
s.src = "https://cdn.jsdelivr.net/npm/@alixlahuec/zotero-roam@0.5";
s.id = "zotero-roam";
s.type = "text/javascript";
document.getElementsByTagName("body")[0].appendChild(s);

// The zoteroRoam_settings object will contain all your settings for the extension
// For now, we're doing a minimal configuration, with just a single data request.
// Paste this into your roam/js block, and fill out the API key + your user ID :

window.customPaperFormat = function(item){
    let metadata = [];
  
  	let mblock = {string: `Metadata`, children: []};
    
    if (item.data.title){
      mblock.children.push(`Title:: ${item.data.title}`) // Title, if available
    };
    if(item.data.creators.length > 0){
    let creatorsList = item.data.creators.map(function (creator) {
        let nameTag = "(" + [creator.firstName, creator.lastName].filter(Boolean).join(" ") + ")";
        if (creator.creatorType != "author") {
            nameTag = nameTag + " (" + creator.creatorType + ")"
        }
        return nameTag;
    })
    mblock.children.push("Author(s):: " + creatorsList.join(", "));
}
    if (item.data.abstractNote){
      mblock.children.push(`Abstract:: ${item.data.abstractNote}`) // Abstract, if available
    };
    mblock.children.push(`Publication:: ${ item.data.publicationTitle || item.data.bookTitle || "" }`) // Publication or book
    if (item.data.url){
      mblock.children.push(`URL : ${item.data.url}`) // URL, if available
    };
    if (item.data.dateAdded){
      mblock.children.push(`Date Added:: ${zoteroRoam.utils.makeDNP(item.data.dateAdded, {brackets: true})}`) // Date added, as Daily Notes Page reference
    };
  // Local + Web links to the item :
    mblock.children.push(`Zotero links:: ${zoteroRoam.formatting.getLocalLink(item)},${zoteroRoam.formatting.getWebLink(item)}`); 
    if (item.data.tags.length > 0){
      mblock.children.push(`Tags:: ${zoteroRoam.formatting.getTags(item)}`) // Tags, if any
    };
  
  // Item's children, if any are in the dataset
    let children = zoteroRoam.formatting.getItemChildren(item, {pdf_as: "links", notes_as: "formatted", split_char: "\n"});
    if(children.pdfItems){
      mblock.children.push(`PDF links : ${children.pdfItems.join(", ")}`);
    }
    if(children.notes){
      let notesBlock = {string: `[[Notes]]`, children: []};
      notesBlock.children.push(...children.notes.flat(1));
      mblock.children.push(notesBlock);
    }
  
  	metadata.push(mblock);
  	metadata.push(`Notes`)

    return metadata; 
};

zoteroRoam_settings = {
    dataRequests: {
        apikey: "[[your own apikey]]",
        dataURI: "users/[[your own number]]/items",
        params: ""
    },
    shortcuts: {
    	toggleSearchPanel: {altKey: true, 'π': true}, // alt+p
  	},
  	funcmap: {
      journalArticle: "customPaperFormat"
    }
}
```

Here I think need some explanations, if you want to create your own version of the output of metadata, you need to add `funcmap` inside the `zoteroRoam_settings`, and if you want to change the metadata for journal paper (most common), then you need to specify `journalArticle` and give the name of the function you will create later (for my case it is `customPaperFormat`).

Then we are going to create this function `customPaperFormat`. In the extension, there is a fixed grammer:

```javascript
window.customPaperFormat = function(item){
  /* some code in here */
}
```

So that we can create our function `customPaperFormat`.

Then we will modify the existing code in order to make our own. There are two things that I want to change in here (you can have more modifications, but I will introduce the basic structure of the code): (1) I want to have a first-level Metadata node, and all the metadata will be the second-level node. (2) I want to get rid of the new page for each author (I do not think that is necessary, if we want to create a page for particular author, we can do that later).

Here are some insights about how to modify the zotero-roam javascript:

* There is one input (`item`), which contains all the information about certain reference from zotero API. There is one output (`metadata`), which contains the information about the metadata block that we want to create.
* **Do not change this line**: `let metadata = []`, but use `metadata.push()` function to create your own block structure
* There are two kinds of blocks: (1) only string, which is very easy, just use `metadata.push('string')` (2) objects (which contains two things: (1) the name of this node (string) (2) the children node. 
  * The object block can be defined by using a dictionary: `let mblock = {string: `Metadata`, children: []};`, then you can use `mblock.children.push()` to create more complicated structures for your block. The block works like a dictionary (or you can think it as a JSON object).
* The details about how to extract information from item is over my capability right now, but I will learn more about that and share my knowledge in here. You can learn more details about the item json in this link (from zotero): https://gist.github.com/dstillman/f1030b9609aadc51ddec
* Every time you change something, you need to reload the page to let the change happen (which is a bit annoying ... to be honest)

If you have any questions, please leave a message in issue, and I will answer them as best as I could.
