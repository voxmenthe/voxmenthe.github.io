---
layout: post
title: Pandas - Basic to Intermediate Data Munging - Part 1
modified:
categories: blog/
excerpt:
tags: [python, pandas, munging]
image:
  feature:
date: 2017-01-08T10:31:00-00:00
---

##### Pandas is an awesome python library for manipulating data - easily as powerful as excel and much more flexible through its integration into the python ecosystem. If you're familiar with R, it's the R dataframes concept implemented in Python.

##### Pandas is especially helpful for cleaning data ('data munging'). Since the goal of data munging in data science is often to generate a matrix to be fed into a machine learning model, `pandas` is a valuable tool for data scientists who use python. 

##### In this tutorial, which began primarily my own notes, I have tried to move as quickly as possible beyond the basics, for which there are many good tutorials already in existence, and try to create as many examples as possible for things I have found useful.**

---

## Tutorial Part 1: Pandas Basics

### Covered in Part 1:
#### Basic indexing and boolean indexing in pandas
#### Groupby - grouping data by features and criterion
#### Binning with 'resample' and 'cut'
#### MultiIndexing
#### Some plotting with 'matplotlib' and 'seaborn'

---

#### Below is an html rendering of the jupyter notebook which can also be downloaded from my github page here: [https://github.com/voxmenthe/pandas-tutorial-by-jeff-coggshall](https://github.com/voxmenthe/pandas-tutorial-by-jeff-coggshall)

---

<html>
<head><meta charset="utf-8" />
<title>Pandas_Post1_Jeff</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.6 (http://getbootstrap.com)
 * Copyright 2011-2015 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    color: #000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: thin dotted;
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: thin dotted;
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: thin dotted;
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=1);
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
@media (max-width: 991px) {
  #ipython_notebook {
    margin-left: 10px;
  }
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#login_widget {
  float: right;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  text-align: center;
  vertical-align: middle;
  display: inline;
  opacity: 0;
  z-index: 2;
  width: 12ex;
  margin-right: -12ex;
}
.alternate_upload .btn-upload {
  height: 22px;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
ul#tabs {
  margin-bottom: 4px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: baseline;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
#tree-selector {
  padding-right: 0px;
}
#button-select-all {
  min-width: 50px;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI colors. */
.ansibold {
  font-weight: bold;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  border-left-width: 1px;
  padding-left: 5px;
  background: linear-gradient(to right, transparent -40px, transparent 1px, transparent 1px, transparent 100%);
}
div.cell.jupyter-soft-selected {
  border-left-color: #90CAF9;
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected {
  border-color: #ababab;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 5px, transparent 5px, transparent 100%);
}
@media print {
  div.cell.selected {
    border-color: transparent;
  }
}
div.cell.selected.jupyter-soft-selected {
  border-left-width: 0;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 7px, #E3F2FD 7px, #E3F2FD 100%);
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #66BB6A -40px, #66BB6A 5px, transparent 5px, transparent 100%);
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
@-moz-document url-prefix() {
  div.inner_cell {
    overflow-x: hidden;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  padding: 0.4em;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. We need the 0 value because of how we size */
  /* .CodeMirror-lines */
  padding: 0;
  border: 0;
  border-radius: 0;
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul {
  list-style: disc;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ul ul {
  list-style: square;
  margin: 0em 2em;
}
.rendered_html ul ul ul {
  list-style: circle;
  margin: 0em 2em;
}
.rendered_html ol {
  list-style: decimal;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
  margin: 0em 2em;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  background-color: #fff;
  color: #000;
  font-size: 100%;
  padding: 0px;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  border: 1px solid black;
  border-collapse: collapse;
  margin: 1em 2em;
}
.rendered_html td,
.rendered_html th {
  text-align: left;
  vertical-align: middle;
  padding: 4px;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget {
  float: right !important;
  float: right;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 20ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  margin-top: 6px;
}
span.save_widget span.filename {
  height: 1em;
  line-height: 1em;
  padding: 3px;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  display: none;
}
.command-shortcut:before {
  content: "(command)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}

@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Pandas-Tutorial">Pandas Tutorial<a class="anchor-link" href="#Pandas-Tutorial">&#182;</a></h1><p><strong>In this tutorial, I have borrowed extensively from others, but have made a concerted effort to synthesize the information in a useful way.</strong></p>
<p><strong>It is my hope that, while it serves primarily as my own notes and reference, it can also be a useful resource for the broader community.</strong></p>
<p>Note: I created and ran the tutorial using python version 3.5.2 and pandas version 0.19.2 though it will probably run on most other python 3 versions as well.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Load-Essential-Libraries">Load Essential Libraries<a class="anchor-link" href="#Load-Essential-Libraries">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>

<span class="kn">import</span> <span class="nn">zipfile</span>
<span class="kn">import</span> <span class="nn">requests</span>

<span class="o">%</span><span class="k">autosave</span> 0
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>



<div id="acf68ffa-de03-41e7-a505-276075956de5"></div>
<div class="output_subarea output_javascript ">
<script type="text/javascript">
var element = $('#acf68ffa-de03-41e7-a505-276075956de5');
IPython.notebook.set_autosave_interval(0)
</script>
</div>

</div>

<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Autosave disabled
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">!</span> python --version
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Python 3.5.2 :: Continuum Analytics, Inc.
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">pd</span><span class="o">.</span><span class="n">__version__</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[3]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&#39;0.19.2&#39;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Load-The-Data-&amp;-Do-Basic-Exploration">Load The Data &amp; Do Basic Exploration<a class="anchor-link" href="#Load-The-Data-&amp;-Do-Basic-Exploration">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;datafiles/mini_movie_data.csv&#39;</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[4]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
      <td>FoxS</td>
      <td>1962-04-02</td>
      <td>1.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(500) Days of Summer</td>
      <td>Minka Kelly</td>
      <td>-</td>
      <td>FoxS</td>
      <td>1980-06-24</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(500) Days of Summer</td>
      <td>Zooey Deschanel</td>
      <td>10</td>
      <td>FoxS</td>
      <td>1980-01-17</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10 Cloverfield Lane</td>
      <td>Mary Elizabeth Winstead</td>
      <td>4</td>
      <td>Par.</td>
      <td>1984-11-28</td>
      <td>0.0</td>
      <td>2016-03-11</td>
      <td>5000000.0</td>
      <td>69793284.0</td>
      <td>101493284.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">columns</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[5]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>Index([&#39;movie&#39;, &#39;actor&#39;, &#39;rank&#39;, &#39;studio&#39;, &#39;bday&#39;, &#39;male&#39;, &#39;release_date&#39;,
       &#39;production_budget&#39;, &#39;domestic_gross&#39;, &#39;worldwide_gross&#39;],
      dtype=&#39;object&#39;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[6]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>male</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>9342.000000</td>
      <td>9.342000e+03</td>
      <td>9.342000e+03</td>
      <td>9.342000e+03</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.668593</td>
      <td>5.082997e+07</td>
      <td>6.888544e+07</td>
      <td>1.540798e+08</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.470744</td>
      <td>5.020522e+07</td>
      <td>8.230204e+07</td>
      <td>2.253854e+08</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>1.500000e+04</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>1.600000e+07</td>
      <td>1.503490e+07</td>
      <td>2.284500e+07</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
      <td>3.500000e+07</td>
      <td>4.033402e+07</td>
      <td>7.143088e+07</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>6.900000e+07</td>
      <td>9.216786e+07</td>
      <td>1.857085e+08</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.000000</td>
      <td>4.250000e+08</td>
      <td>7.605076e+08</td>
      <td>2.783919e+09</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
RangeIndex: 9342 entries, 0 to 9341
Data columns (total 10 columns):
movie                9342 non-null object
actor                9342 non-null object
rank                 9342 non-null object
studio               9342 non-null object
bday                 9342 non-null object
male                 9342 non-null float64
release_date         9342 non-null object
production_budget    9342 non-null float64
domestic_gross       9342 non-null float64
worldwide_gross      9342 non-null float64
dtypes: float64(4), object(6)
memory usage: 729.9+ KB
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-rename-function">The <code>rename</code> function<a class="anchor-link" href="#The-rename-function">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># rename the &#39;movie&#39; column to &#39;title&#39;</span>
<span class="c1"># you can rename multiple columns by adding more key:value pairs to the dictionary</span>
<span class="n">df</span><span class="o">.</span><span class="n">rename</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">{</span><span class="s1">&#39;movie&#39;</span><span class="p">:</span><span class="s1">&#39;title&#39;</span><span class="p">},</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[8]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
      <td>FoxS</td>
      <td>1962-04-02</td>
      <td>1.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Basic-Indexing-and-data-access">Basic Indexing and data access<a class="anchor-link" href="#Basic-Indexing-and-data-access">&#182;</a></h2><p>Pandas has two main methods of grabbing data:</p>
<ul>
<li><code>.loc</code> for label-based indexing (like row or column names)</li>
<li><code>.iloc</code> for positional indexing (like array indices)</li>
<li>There is also <code>.ix</code> which tries to do both, but should not generally be used</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># get rows starting at index 1 and ending before 3</span>
<span class="c1"># and only get from columns at indices 1 and 3</span>
<span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">1</span><span class="p">:</span><span class="mi">3</span><span class="p">,[</span><span class="mi">1</span><span class="p">,</span><span class="mi">3</span><span class="p">]]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[9]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>actor</th>
      <th>studio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Clark Gregg</td>
      <td>FoxS</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Minka Kelly</td>
      <td>FoxS</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># note that the numbers only work in loc</span>
<span class="c1"># because are row labels are actually numbers at the moment</span>
<span class="n">df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">1</span><span class="p">:</span><span class="mi">3</span><span class="p">,</span><span class="s1">&#39;title&#39;</span><span class="p">:</span><span class="s1">&#39;rank&#39;</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[10]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(500) Days of Summer</td>
      <td>Minka Kelly</td>
      <td>-</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(500) Days of Summer</td>
      <td>Zooey Deschanel</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># these tools allow us to access any arbitrary set of points</span>
<span class="c1"># within the dataframe</span>
<span class="n">df</span><span class="o">.</span><span class="n">loc</span><span class="p">[[</span><span class="mi">3</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">8</span><span class="p">],[</span><span class="s1">&#39;actor&#39;</span><span class="p">,</span><span class="s1">&#39;studio&#39;</span><span class="p">,</span><span class="s1">&#39;rank&#39;</span><span class="p">]]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[11]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>actor</th>
      <th>studio</th>
      <th>rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Zooey Deschanel</td>
      <td>FoxS</td>
      <td>10</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Glenn Close</td>
      <td>BV</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>James Marsden</td>
      <td>Think</td>
      <td>29</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Boolean-Indexing">Boolean Indexing<a class="anchor-link" href="#Boolean-Indexing">&#182;</a></h2><ul>
<li>Pandas allows you to access data by criterion</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># create an array of alternating True and False values</span>
<span class="n">tf_array</span> <span class="o">=</span> <span class="p">[</span><span class="kc">True</span><span class="p">,</span> <span class="kc">False</span><span class="p">]</span> <span class="o">*</span> <span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span><span class="o">//</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># get every other value in the array, up to the 5th element</span>
<span class="n">df</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">tf_array</span><span class="p">,:][:</span><span class="mi">5</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[13]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(500) Days of Summer</td>
      <td>Minka Kelly</td>
      <td>-</td>
      <td>FoxS</td>
      <td>1980-06-24</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10 Cloverfield Lane</td>
      <td>Mary Elizabeth Winstead</td>
      <td>4</td>
      <td>Par.</td>
      <td>1984-11-28</td>
      <td>0.0</td>
      <td>2016-03-11</td>
      <td>5000000.0</td>
      <td>69793284.0</td>
      <td>101493284.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>102 Dalmatians</td>
      <td>Ioan Gruffudd</td>
      <td>4</td>
      <td>BV</td>
      <td>1973-10-06</td>
      <td>1.0</td>
      <td>2000-11-22</td>
      <td>85000000.0</td>
      <td>66941559.0</td>
      <td>66941559.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>10th &amp; Wolf</td>
      <td>James Marsden</td>
      <td>29</td>
      <td>Think</td>
      <td>1973-09-18</td>
      <td>1.0</td>
      <td>2006-08-18</td>
      <td>8000000.0</td>
      <td>54702.0</td>
      <td>143782.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># this true/false indexing can be directly extended to boolean conditions:</span>

<span class="c1"># first clean the data a bit</span>
<span class="n">df</span><span class="p">[</span><span class="s1">&#39;rank&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s1">&#39;rank&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">replace</span><span class="p">(</span><span class="s1">&#39;-&#39;</span><span class="p">,</span><span class="mi">9999999999999</span><span class="p">)</span>
<span class="n">df</span><span class="p">[</span><span class="s1">&#39;rank&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_numeric</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;rank&#39;</span><span class="p">])</span>

<span class="c1"># get all the movies with rank between 34 and 38 with &quot;Fox&quot; as the studio &amp; domestic_gross &lt; production_budget</span>
<span class="n">df</span><span class="p">[(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;rank&#39;</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">34</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;rank&#39;</span><span class="p">]</span> <span class="o">&lt;=</span> <span class="mi">38</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;studio&#39;</span><span class="p">]</span><span class="o">==</span><span class="s1">&#39;Fox&#39;</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;domestic_gross&#39;</span><span class="p">]</span><span class="o">&lt;</span><span class="n">df</span><span class="p">[</span><span class="s1">&#39;production_budget&#39;</span><span class="p">])]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[14]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1346</th>
      <td>Chain Reaction</td>
      <td>Morgan Freeman</td>
      <td>36</td>
      <td>Fox</td>
      <td>1937-06-01</td>
      <td>1.0</td>
      <td>1996-08-02</td>
      <td>55000000.0</td>
      <td>20550712.0</td>
      <td>59533842.0</td>
    </tr>
    <tr>
      <th>3617</th>
      <td>Joy</td>
      <td>Robert DeNiro</td>
      <td>34</td>
      <td>Fox</td>
      <td>1943-08-17</td>
      <td>1.0</td>
      <td>2015-12-25</td>
      <td>60000000.0</td>
      <td>56451232.0</td>
      <td>100751232.0</td>
    </tr>
    <tr>
      <th>3762</th>
      <td>Kiss of Death</td>
      <td>Nicolas Cage</td>
      <td>35</td>
      <td>Fox</td>
      <td>1964-01-07</td>
      <td>1.0</td>
      <td>1995-04-21</td>
      <td>40000000.0</td>
      <td>14924355.0</td>
      <td>14924355.0</td>
    </tr>
    <tr>
      <th>4366</th>
      <td>Meet Dave</td>
      <td>Eddie Murphy</td>
      <td>37</td>
      <td>Fox</td>
      <td>1961-04-03</td>
      <td>1.0</td>
      <td>2008-07-11</td>
      <td>60000000.0</td>
      <td>11803254.0</td>
      <td>50648806.0</td>
    </tr>
    <tr>
      <th>6701</th>
      <td>The Big Year</td>
      <td>Owen Wilson</td>
      <td>34</td>
      <td>Fox</td>
      <td>1968-11-18</td>
      <td>1.0</td>
      <td>2011-10-14</td>
      <td>41000000.0</td>
      <td>7204138.0</td>
      <td>7684524.0</td>
    </tr>
    <tr>
      <th>6704</th>
      <td>The Big Year</td>
      <td>Steve Martin</td>
      <td>34</td>
      <td>Fox</td>
      <td>1945-08-14</td>
      <td>1.0</td>
      <td>2011-10-14</td>
      <td>41000000.0</td>
      <td>7204138.0</td>
      <td>7684524.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="SettingWithCopy">SettingWithCopy<a class="anchor-link" href="#SettingWithCopy">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[85]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># another example</span>
<span class="n">f</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s1">&#39;a&#39;</span><span class="p">:[</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">4</span><span class="p">,</span><span class="mi">5</span><span class="p">],</span> <span class="s1">&#39;b&#39;</span><span class="p">:[</span><span class="mi">10</span><span class="p">,</span><span class="mi">20</span><span class="p">,</span><span class="mi">30</span><span class="p">,</span><span class="mi">40</span><span class="p">,</span><span class="mi">50</span><span class="p">]})</span>
<span class="n">f</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[85]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[87]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Let&#39;s take only the rows of `b` where `a` is 3 or less, and set the `b` values equal to `b` / 10:</span>
<span class="c1"># ! Pitfall - in pandas try to avoid side-by-side square brackets when indexing as it is not guaranteed</span>
<span class="c1"># whether the results of the first square bracket return a view or a copy that is then acted on by the</span>
<span class="c1"># second square brackets</span>
<span class="n">f</span><span class="p">[</span><span class="n">f</span><span class="p">[</span><span class="s1">&#39;a&#39;</span><span class="p">]</span> <span class="o">&lt;=</span> <span class="mi">3</span><span class="p">][</span><span class="s1">&#39;b&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">f</span><span class="p">[</span><span class="n">f</span><span class="p">[</span><span class="s1">&#39;a&#39;</span><span class="p">]</span> <span class="o">&lt;=</span> <span class="mi">3</span> <span class="p">][</span><span class="s1">&#39;b&#39;</span><span class="p">]</span> <span class="o">/</span> <span class="mi">10</span>
<span class="n">f</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stderr output_text">
<pre>/opt/conda/lib/python3.5/site-packages/ipykernel/__main__.py:5: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
</pre>
</div>
</div>

<div class="output_area"><div class="prompt output_prompt">Out[87]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># the correct way to do it is to use .loc and put it all in one set of brackets</span>
<span class="n">f</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">f</span><span class="p">[</span><span class="s1">&#39;a&#39;</span><span class="p">]</span> <span class="o">&lt;=</span> <span class="mi">3</span><span class="p">,</span> <span class="s1">&#39;b&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">f</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="n">f</span><span class="p">[</span><span class="s1">&#39;a&#39;</span><span class="p">]</span> <span class="o">&lt;=</span> <span class="mi">3</span><span class="p">,</span> <span class="s1">&#39;b&#39;</span><span class="p">]</span> <span class="o">/</span> <span class="mi">10</span>
<span class="n">f</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Groupby-objects">Groupby objects<a class="anchor-link" href="#Groupby-objects">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">actors</span> <span class="o">=</span><span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;actor&#39;</span><span class="p">)</span>
<span class="c1"># this results in a groupby object that we can run functions on or send queries to</span>
<span class="n">actors</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[15]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;pandas.core.groupby.DataFrameGroupBy object at 0x7fd322b77f28&gt;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># select the first row in each group</span>
<span class="c1"># The .head() is just so the printed dataframe doesn&#39;t fill the screen - it is optional</span>
<span class="n">actors</span><span class="o">.</span><span class="n">first</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[16]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aaron Eckhart</th>
      <td>Any Given Sunday</td>
      <td>3</td>
      <td>WB</td>
      <td>1968-03-12</td>
      <td>1.0</td>
      <td>1999-12-22</td>
      <td>60000000.0</td>
      <td>75530832.0</td>
      <td>100230832.0</td>
    </tr>
    <tr>
      <th>Aaron Johnson</th>
      <td>Anna Karenina</td>
      <td>7</td>
      <td>Focus</td>
      <td>1990-06-13</td>
      <td>1.0</td>
      <td>2012-11-16</td>
      <td>49000000.0</td>
      <td>12816367.0</td>
      <td>71004627.0</td>
    </tr>
    <tr>
      <th>Abbie Cornish</th>
      <td>A Good Year</td>
      <td>8</td>
      <td>Fox</td>
      <td>1982-08-07</td>
      <td>0.0</td>
      <td>2006-11-10</td>
      <td>35000000.0</td>
      <td>7459300.0</td>
      <td>42064105.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># select the last row in each group</span>
<span class="n">actors</span><span class="o">.</span><span class="n">last</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[17]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aaron Eckhart</th>
      <td>The Pledge</td>
      <td>13</td>
      <td>WB</td>
      <td>1968-03-12</td>
      <td>1.0</td>
      <td>2001-01-19</td>
      <td>45000000.0</td>
      <td>19719930.0</td>
      <td>29406132.0</td>
    </tr>
    <tr>
      <th>Aaron Johnson</th>
      <td>The Illusionist</td>
      <td>9999999999999</td>
      <td>YFG</td>
      <td>1990-06-13</td>
      <td>1.0</td>
      <td>2006-08-18</td>
      <td>16500000.0</td>
      <td>39868642.0</td>
      <td>83792062.0</td>
    </tr>
    <tr>
      <th>Abbie Cornish</th>
      <td>Sucker Punch</td>
      <td>4</td>
      <td>WB</td>
      <td>1982-08-07</td>
      <td>0.0</td>
      <td>2011-03-25</td>
      <td>75000000.0</td>
      <td>36392502.0</td>
      <td>89758389.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>What you should see from the two results above is that for each actor, we are getting different results in the rest of the columns, as expected.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># take the mean of all rows for each group</span>
<span class="c1"># columns which you can&#39;t take the mean of will automatically be dropped</span>
<span class="n">actors</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[18]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rank</th>
      <th>male</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aaron Eckhart</th>
      <td>1.209524e+01</td>
      <td>1.0</td>
      <td>5.087976e+07</td>
      <td>6.033282e+07</td>
      <td>1.171763e+08</td>
    </tr>
    <tr>
      <th>Aaron Johnson</th>
      <td>1.111111e+12</td>
      <td>1.0</td>
      <td>4.271111e+07</td>
      <td>4.884212e+07</td>
      <td>1.134827e+08</td>
    </tr>
    <tr>
      <th>Abbie Cornish</th>
      <td>5.000000e+00</td>
      <td>0.0</td>
      <td>5.100000e+07</td>
      <td>3.156147e+07</td>
      <td>8.960463e+07</td>
    </tr>
    <tr>
      <th>Abigail Breslin</th>
      <td>9.823529e+00</td>
      <td>0.0</td>
      <td>3.700604e+07</td>
      <td>5.992972e+07</td>
      <td>1.025613e+08</td>
    </tr>
    <tr>
      <th>Adam Brody</th>
      <td>3.000000e+12</td>
      <td>1.0</td>
      <td>2.062500e+07</td>
      <td>4.137886e+07</td>
      <td>7.525851e+07</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># get a group by name</span>
<span class="n">actors</span><span class="o">.</span><span class="n">get_group</span><span class="p">(</span><span class="s1">&#39;Aaron Eckhart&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[19]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bday</th>
      <th>domestic_gross</th>
      <th>male</th>
      <th>production_budget</th>
      <th>rank</th>
      <th>release_date</th>
      <th>studio</th>
      <th>title</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>597</th>
      <td>1968-03-12</td>
      <td>75530832.0</td>
      <td>1.0</td>
      <td>60000000.0</td>
      <td>3</td>
      <td>1999-12-22</td>
      <td>WB</td>
      <td>Any Given Sunday</td>
      <td>100230832.0</td>
    </tr>
    <tr>
      <th>831</th>
      <td>1968-03-12</td>
      <td>83552429.0</td>
      <td>1.0</td>
      <td>70000000.0</td>
      <td>5</td>
      <td>2011-03-11</td>
      <td>Sony</td>
      <td>Battle: Los Angeles</td>
      <td>213463976.0</td>
    </tr>
    <tr>
      <th>1610</th>
      <td>1968-03-12</td>
      <td>379418.0</td>
      <td>1.0</td>
      <td>450000.0</td>
      <td>24</td>
      <td>2006-08-11</td>
      <td>Fabr.</td>
      <td>Conversations with Other Women</td>
      <td>1297745.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># calling size() on a groupby object will return the number of rows each group contains</span>
<span class="n">actors</span><span class="o">.</span><span class="n">size</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[20]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>actor
Aaron Eckhart      21
Aaron Johnson       9
Abbie Cornish       9
Abigail Breslin    17
Adam Brody         10
dtype: int64</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># agg() can take a list of functions</span>
<span class="c1"># It makes a new column and applies them to each group in a groupby</span>
<span class="n">actors</span><span class="p">[</span><span class="s1">&#39;domestic_gross&#39;</span><span class="p">,</span><span class="s1">&#39;worldwide_gross&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">agg</span><span class="p">([</span><span class="s1">&#39;mean&#39;</span><span class="p">,</span><span class="s1">&#39;count&#39;</span><span class="p">,</span><span class="s1">&#39;std&#39;</span><span class="p">,</span><span class="s1">&#39;min&#39;</span><span class="p">,</span><span class="s1">&#39;max&#39;</span><span class="p">])</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>
<span class="c1"># Note that you end up with a multi-index, which we will cover later</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[21]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="5" halign="left">domestic_gross</th>
      <th colspan="5" halign="left">worldwide_gross</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>count</th>
      <th>std</th>
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>count</th>
      <th>std</th>
      <th>min</th>
      <th>max</th>
    </tr>
    <tr>
      <th>actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aaron Eckhart</th>
      <td>6.033282e+07</td>
      <td>21</td>
      <td>1.138151e+08</td>
      <td>17396.0</td>
      <td>533345358.0</td>
      <td>1.171763e+08</td>
      <td>21</td>
      <td>2.158466e+08</td>
      <td>17396.0</td>
      <td>1.002891e+09</td>
    </tr>
    <tr>
      <th>Aaron Johnson</th>
      <td>4.884212e+07</td>
      <td>9</td>
      <td>6.081880e+07</td>
      <td>115862.0</td>
      <td>200672193.0</td>
      <td>1.134827e+08</td>
      <td>9</td>
      <td>1.596594e+08</td>
      <td>117796.0</td>
      <td>5.290722e+08</td>
    </tr>
    <tr>
      <th>Abbie Cornish</th>
      <td>3.156147e+07</td>
      <td>9</td>
      <td>2.706417e+07</td>
      <td>4444637.0</td>
      <td>79249455.0</td>
      <td>8.960463e+07</td>
      <td>9</td>
      <td>7.701140e+07</td>
      <td>11229035.0</td>
      <td>2.429818e+08</td>
    </tr>
    <tr>
      <th>Abigail Breslin</th>
      <td>5.992972e+07</td>
      <td>17</td>
      <td>5.285277e+07</td>
      <td>187112.0</td>
      <td>227965690.0</td>
      <td>1.025613e+08</td>
      <td>17</td>
      <td>9.785130e+07</td>
      <td>597989.0</td>
      <td>4.082657e+08</td>
    </tr>
    <tr>
      <th>Adam Brody</th>
      <td>4.137886e+07</td>
      <td>10</td>
      <td>5.263487e+07</td>
      <td>769726.0</td>
      <td>145096820.0</td>
      <td>7.525851e+07</td>
      <td>10</td>
      <td>1.056659e+08</td>
      <td>786677.0</td>
      <td>2.865000e+08</td>
    </tr>
    <tr>
      <th>Adam DeVine</th>
      <td>1.243933e+08</td>
      <td>2</td>
      <td>8.399320e+07</td>
      <td>65001093.0</td>
      <td>183785415.0</td>
      <td>2.015199e+08</td>
      <td>2</td>
      <td>1.208806e+08</td>
      <td>116044347.0</td>
      <td>2.869954e+08</td>
    </tr>
    <tr>
      <th>Adam Sandler</th>
      <td>9.154979e+07</td>
      <td>28</td>
      <td>5.320617e+07</td>
      <td>9975684.0</td>
      <td>169700110.0</td>
      <td>1.618510e+08</td>
      <td>28</td>
      <td>1.110394e+08</td>
      <td>9975684.0</td>
      <td>4.693845e+08</td>
    </tr>
    <tr>
      <th>Adrianne Palicki</th>
      <td>8.366492e+07</td>
      <td>2</td>
      <td>5.495371e+07</td>
      <td>44806783.0</td>
      <td>122523060.0</td>
      <td>2.100436e+08</td>
      <td>2</td>
      <td>2.289321e+08</td>
      <td>48164150.0</td>
      <td>3.719231e+08</td>
    </tr>
    <tr>
      <th>Adrien Brody</th>
      <td>4.229720e+07</td>
      <td>15</td>
      <td>5.760924e+07</td>
      <td>12836.0</td>
      <td>218080025.0</td>
      <td>1.039203e+08</td>
      <td>15</td>
      <td>1.465820e+08</td>
      <td>12836.0</td>
      <td>5.505174e+08</td>
    </tr>
    <tr>
      <th>Aimee Teegarden</th>
      <td>2.415557e+07</td>
      <td>2</td>
      <td>1.983485e+07</td>
      <td>10130219.0</td>
      <td>38180928.0</td>
      <td>5.337639e+07</td>
      <td>2</td>
      <td>6.026417e+07</td>
      <td>10763183.0</td>
      <td>9.598959e+07</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="mi">1</span><span class="n">e8</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[22]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>100000000.0</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># this example illustrates 2 things:</span>
<span class="c1"># 1) grouping based on a conditional statement (i.e. is divisible by 3)</span>
<span class="c1"># 2) iterating through groups in a groupby</span>
<span class="k">for</span> <span class="n">name</span><span class="p">,</span> <span class="n">group</span> <span class="ow">in</span> <span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">worldwide_gross</span><span class="o">%</span><span class="k">3</span>==0):
    <span class="nb">print</span><span class="p">(</span><span class="n">name</span><span class="p">,</span> <span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span> <span class="n">group</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">))</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;* * *&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>False 
                   title         actor           rank studio        bday  male  \
0  (500) Days of Summer  Chloe Moretz             11   FoxS  1997-02-10   0.0   
1  (500) Days of Summer   Clark Gregg              7   FoxS  1962-04-02   1.0   
2  (500) Days of Summer   Minka Kelly  9999999999999   FoxS  1980-06-24   0.0   

  release_date  production_budget  domestic_gross  worldwide_gross  
0   2009-07-17          7500000.0      32391374.0       59101642.0  
1   2009-07-17          7500000.0      32391374.0       59101642.0  
2   2009-07-17          7500000.0      32391374.0       59101642.0  
* * *
True 
                title                 actor  rank studio        bday  male  \
5     102 Dalmatians           Glenn Close     7     BV  1947-03-19   0.0   
6     102 Dalmatians         Ioan Gruffudd     4     BV  1973-10-06   1.0   
12  12 Years a Slave  Benedict Cumberbatch     8   FoxS  1976-07-19   1.0   

   release_date  production_budget  domestic_gross  worldwide_gross  
5    2000-11-22         85000000.0      66941559.0       66941559.0  
6    2000-11-22         85000000.0      66941559.0       66941559.0  
12   2013-10-18         20000000.0      56671993.0      181025343.0  
* * *
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Datatypes:-type-and-dtype">Datatypes: type and dtype<a class="anchor-link" href="#Datatypes:-type-and-dtype">&#182;</a></h1><ul>
<li>It is always worth keeping track of what the datatypes are in your dataframe</li>
<li>Pandas provides a number of functions to manage this:</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Review what the dataframe looks like:</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[24]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
      <td>FoxS</td>
      <td>1962-04-02</td>
      <td>1.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># the info function provides an overview of the datatypes of each column</span>
<span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
RangeIndex: 9342 entries, 0 to 9341
Data columns (total 10 columns):
title                9342 non-null object
actor                9342 non-null object
rank                 9342 non-null int64
studio               9342 non-null object
bday                 9342 non-null object
male                 9342 non-null float64
release_date         9342 non-null object
production_budget    9342 non-null float64
domestic_gross       9342 non-null float64
worldwide_gross      9342 non-null float64
dtypes: float64(4), int64(1), object(5)
memory usage: 729.9+ KB
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># you can change datatypes by using the pandas.DataFrame.astype function</span>
<span class="c1"># which casts to a numpy dtype - in this case we convert everything in the df to a string</span>
<span class="n">df_string</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="s1">&#39;str&#39;</span><span class="p">)</span>
<span class="n">df_string</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[26]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
      <td>FoxS</td>
      <td>1962-04-02</td>
      <td>1.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df_string</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;class &#39;pandas.core.frame.DataFrame&#39;&gt;
RangeIndex: 9342 entries, 0 to 9341
Data columns (total 10 columns):
title                9342 non-null object
actor                9342 non-null object
rank                 9342 non-null object
studio               9342 non-null object
bday                 9342 non-null object
male                 9342 non-null object
release_date         9342 non-null object
production_budget    9342 non-null object
domestic_gross       9342 non-null object
worldwide_gross      9342 non-null object
dtypes: object(10)
memory usage: 729.9+ KB
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># but we are limited in what we can do, since if we tried to convert a string to </span>
<span class="c1"># an integer or floating point number, it throws an error</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="pd.to_numeric()">pd.to_numeric()<a class="anchor-link" href="#pd.to_numeric()">&#182;</a></h2><p>Converts a series, array or dataframe to a numeric datatype</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># example Dataframe of numbers-as-strings</span>
<span class="n">num_example</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="nb">list</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="s1">&#39;298576&#39;</span><span class="p">),</span><span class="nb">list</span><span class="p">(</span><span class="s1">&#39;814309&#39;</span><span class="p">))),</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;a&#39;</span><span class="p">,</span><span class="s1">&#39;b&#39;</span><span class="p">])</span>
<span class="n">num_example</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[29]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># if you add columns a and b, they&#39;re just concatenated together</span>
<span class="n">num_example</span><span class="o">.</span><span class="n">a</span> <span class="o">+</span> <span class="n">num_example</span><span class="o">.</span><span class="n">b</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[30]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>0    28
1    91
2    84
3    53
4    70
5    69
dtype: object</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># apply pd.to_numeric across the whole dataframe to convert everything to numeric values</span>
<span class="n">num_numeric</span> <span class="o">=</span> <span class="n">num_example</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">to_numeric</span><span class="p">)</span>
<span class="n">num_numeric</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[31]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># now adding the columns gives you the sum</span>
<span class="n">num_numeric</span><span class="o">.</span><span class="n">a</span> <span class="o">+</span> <span class="n">num_numeric</span><span class="o">.</span><span class="n">b</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[32]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>0    10
1    10
2    12
3     8
4     7
5    15
dtype: int64</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># this example illustrates 2 things:</span>
<span class="c1"># 1) grouping based on a conditional statement (i.e. is an even number)</span>
<span class="c1"># 2) iterating through groups in a groupby</span>
<span class="k">for</span> <span class="n">name</span><span class="p">,</span> <span class="n">group</span> <span class="ow">in</span> <span class="n">num_numeric</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">num_numeric</span><span class="o">.</span><span class="n">a</span><span class="o">%</span><span class="k">2</span>==0):
    <span class="nb">print</span><span class="p">(</span><span class="n">name</span><span class="p">,</span> <span class="s1">&#39;</span><span class="se">\n</span><span class="s1">&#39;</span><span class="p">,</span> <span class="n">group</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s1">&#39;* * *&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>False 
    a  b
1  9  1
3  5  3
4  7  0
* * *
True 
    a  b
0  2  8
2  8  4
5  6  9
* * *
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Working-with-Timestamps-and-Datetime">Working with Timestamps and Datetime<a class="anchor-link" href="#Working-with-Timestamps-and-Datetime">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[84]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Let&#39;s look at our dataframe again</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[84]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
      <td>FoxS</td>
      <td>1962-04-02</td>
      <td>1.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(500) Days of Summer</td>
      <td>Minka Kelly</td>
      <td>9999999999999</td>
      <td>FoxS</td>
      <td>1980-06-24</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># what is the data type (dtype) of the bday column?</span>
<span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="o">.</span><span class="n">dtype</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[35]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>dtype(&#39;O&#39;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># or check the dtype of the first element</span>
<span class="nb">type</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="p">[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[36]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>str</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="pd.to_datetime">pd.to_datetime<a class="anchor-link" href="#pd.to_datetime">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># convert the columns of date-time strings to pandas Timestamp objects</span>
<span class="c1"># we don&#39;t use .apply here because we only want to change these 2 specified columns</span>
<span class="k">for</span> <span class="n">datetime_col</span> <span class="ow">in</span> <span class="p">[</span><span class="s1">&#39;bday&#39;</span><span class="p">,</span> <span class="s1">&#39;release_date&#39;</span><span class="p">]:</span>
    <span class="n">df</span><span class="p">[</span><span class="n">datetime_col</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">datetime_col</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="o">.</span><span class="n">dtype</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[38]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>dtype(&#39;&lt;M8[ns]&#39;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">type</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="p">[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[39]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>pandas.tslib.Timestamp</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Instant-converstion-to-day/month/year-with">Instant converstion to day/month/year with<a class="anchor-link" href="#Instant-converstion-to-day/month/year-with">&#182;</a></h2><p><strong> <code>pd.Series.dt.&lt;day/month/year/second/etc...&gt;</code> </strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="s1">&#39;years&#39;</span><span class="p">,</span> <span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">year</span><span class="o">.</span><span class="n">unique</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>years [1997 1962 1980 1984 1947 1973 1974 1976 1959 1977 1963 1983 1966 1967 1978
 1979 1948 1975 1955 1943 1972 1969 1985 1987 1952 1954 1971 1946 1961 1981
 1960 1968 1970 1982 1964 1958 1989 1986 1996 1951 1992 1942 1965 1953 1940
 1929 1950 1937 1933 1936 1930 1931 1934 1938 1956 1957 1939 1949 1944 1990
 1998 1926 1988 1991 2003 1935 1924 1945 1928 1994 1999 1875 1993 1925 1922
 1995]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># this doesn&#39;t work:</span>
<span class="c1"># df[df.bday &gt; 1995]</span>

<span class="c1"># so instead you can compare to a Timestamp or other datetime object</span>
<span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">bday</span> <span class="o">&gt;</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="s1">&#39;1-1-1995&#39;</span><span class="p">)]</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[41]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>3 Days to Kill</td>
      <td>Hailee Steinfeld</td>
      <td>4</td>
      <td>Rela.</td>
      <td>1996-12-11</td>
      <td>0.0</td>
      <td>2014-02-21</td>
      <td>28000000.0</td>
      <td>30697999.0</td>
      <td>38959900.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># or, use the .dt syntax:</span>
<span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">year</span> <span class="o">&gt;</span> <span class="mi">1995</span><span class="p">]</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[42]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>3 Days to Kill</td>
      <td>Hailee Steinfeld</td>
      <td>4</td>
      <td>Rela.</td>
      <td>1996-12-11</td>
      <td>0.0</td>
      <td>2014-02-21</td>
      <td>28000000.0</td>
      <td>30697999.0</td>
      <td>38959900.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Pitfall!</span>
<span class="c1"># when you want to select using multiple conditions, watch out for this pandas pitfall</span>
<span class="c1"># (this doesn&#39;t work:)</span>
<span class="c1"># df[2000 &gt; df.bday.dt.year &gt; 1995].head()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Pitfall!</span>
<span class="c1"># Instead, use the bitwise and (&amp;) operator. However...</span>
<span class="c1"># (this doesn&#39;t work either):</span>
<span class="c1"># df[2000 &gt; df.bday.dt.year &amp; df.bday.dt.year &gt; 1995].head()</span>
<span class="c1"># Instead, use the bitwise and (&amp;) operator. However...</span>
<span class="c1"># (this doesn&#39;t work either):</span>
<span class="c1"># df[2000 &gt; df.bday.dt.year &amp; df.bday.dt.year &gt; 1995].head()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Since-the-'&amp;'-operator-has-a-really-high-precedence-in-the-order-of-operations,-be-sure-to-enclose-each-condition-in-parentheses">Since the '&amp;' operator has a really high precedence in the order of operations, be sure to enclose each condition in parentheses<a class="anchor-link" href="#Since-the-'&amp;'-operator-has-a-really-high-precedence-in-the-order-of-operations,-be-sure-to-enclose-each-condition-in-parentheses">&#182;</a></h2><p>Eg: <code>2000 &gt; df.bday.dt.year &amp; df.bday.dt.year &gt; 1995</code> is evaluated the same as</p>
<p><code>2000 &gt; (df.bday.dt.year &amp; df.bday.td.year) &gt; 1995</code></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># select birthdays between 1995 and 2000, non-inclusive</span>
<span class="n">df</span><span class="p">[(</span><span class="mi">2000</span> <span class="o">&gt;</span> <span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">year</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">bday</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">year</span> <span class="o">&gt;</span> <span class="mi">1995</span><span class="p">)]</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[45]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>3 Days to Kill</td>
      <td>Hailee Steinfeld</td>
      <td>4</td>
      <td>Rela.</td>
      <td>1996-12-11</td>
      <td>0.0</td>
      <td>2014-02-21</td>
      <td>28000000.0</td>
      <td>30697999.0</td>
      <td>38959900.0</td>
    </tr>
    <tr>
      <th>307</th>
      <td>After Earth</td>
      <td>Jaden Smith</td>
      <td>4</td>
      <td>Sony</td>
      <td>1998-07-08</td>
      <td>1.0</td>
      <td>2013-05-31</td>
      <td>130000000.0</td>
      <td>60522097.0</td>
      <td>251499665.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># example of .dt.month</span>
<span class="c1"># Note: you rarely need to add columns like this!! You can use .dt directly for a groupby or for a selection</span>
<span class="n">df2</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">df2</span><span class="p">[</span><span class="s1">&#39;release_month&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df2</span><span class="o">.</span><span class="n">release_date</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">month</span>
<span class="n">df2</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[46]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
      <th>release_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(500) Days of Summer</td>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(500) Days of Summer</td>
      <td>Clark Gregg</td>
      <td>7</td>
      <td>FoxS</td>
      <td>1962-04-02</td>
      <td>1.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(500) Days of Summer</td>
      <td>Minka Kelly</td>
      <td>9999999999999</td>
      <td>FoxS</td>
      <td>1980-06-24</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">monthly_mean</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">release_date</span><span class="o">.</span><span class="n">dt</span><span class="o">.</span><span class="n">month</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
<span class="n">monthly_mean</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[47]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rank</th>
      <th>male</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1195928753192</td>
      <td>0.674300</td>
      <td>3.260153e+07</td>
      <td>3.810404e+07</td>
      <td>7.400509e+07</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1059027777788</td>
      <td>0.635417</td>
      <td>4.066693e+07</td>
      <td>4.773956e+07</td>
      <td>9.061837e+07</td>
    </tr>
    <tr>
      <th>3</th>
      <td>855614973272</td>
      <td>0.664439</td>
      <td>4.960052e+07</td>
      <td>6.042128e+07</td>
      <td>1.255552e+08</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">monthly_mean</span><span class="p">[[</span><span class="s1">&#39;domestic_gross&#39;</span><span class="p">,</span><span class="s1">&#39;worldwide_gross&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">&#39;Mean monthly gross&#39;</span><span class="p">,</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">7</span><span class="p">,</span><span class="mi">4</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[48]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x7fd322b3f6d8&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
iIgEYpEiIiIiEohFioiIiEggFikiIiIigVikiIiIiARikSIiIiISiEWKiIiISCAWKSIiIiKBWKSI
iIiIBGKRIiIiIhKIRYqIiIhIIBYpIiIiIoFYpIiIiIgEYpEiIiIiEohFioiIiEggFikiIiIigVik
iIiIiARSu0idPn0awcHB8PX1hUQiwa+//lrr+L///hsSiUTpl5OTE/Ly8gSHJiIiItIFRuquUFJS
AicnJ7z++uuYMmWKSuuIRCLExsbC1NRUsczKykrdtyYiIiLSKWoXKT8/P/j5+QEA5HK5yutZWlqi
WbNm6r4dERERkc5Su0gJIZfLMXToUJSVlaFz586YPHkyPD09G+KtiYiIiDRG40WqRYsWWLBgAbp0
6QKpVIro6GgEBQVh165dcHJyUnkeAwMRDAxE9ZrN0NBA6b/6Qh9zM3PDEPJnxNDQAEZG2vuM+pgZ
UD+3LmTWx+80MzccffxO60JmjRcpe3t72NvbK352d3dHeno6IiIiEBoaqvI8lpamEInqt0g9JBab
aGReTdPH3MysWc2aGau9jlhsAgsL07oHaog+ZgbUz60LmR/Sp+/0Q8ysefr4ndaFzA1yaO9xLi4u
OHv2rFrr5Off08geKbHYBIWF91FZKavXuTVJH3Mzc8MoLi5Ve53CwvsoKLingTSq0cfMgPq5dSGz
Pn6nmbnh6ON3WpOZVS1cWilSqampaNmypVrryGRyyGSqn9yujspKGSoq9OfL/pA+5mZmzRLyZ0Tb
n08fMwPq59aFzA/pUhZVMbPm6eN3WhcyC7r9wY0bNxRX7KWnpyM1NRXNmzdH69atsXz5cmRnZysO
223evBk2Njbo1KkTysrKEB0djbi4OGzatKlePwgRERFRQ1O7SCUnJyMoKAgikQgikUhRmPz9/RES
EoLc3FxkZmYqxpeXlyM0NBTZ2dkwNjaGo6MjIiIi4O3tXX+fgoiIiEgL1C5S3bp1Q2pqao2vh4SE
KP08ceJETJw4Uf1kRERERDpOv67NJCIiItIhLFJEREREArFIEREREQnEIkVEREQkEIsUERERkUAs
UkREREQCsUgRERERCcQiRURERCQQixQRERGRQCxSRERERAKxSBEREREJxCJFREREJBCLFBEREZFA
LFJEREREArFIEREREQnEIkVEREQkEIsUERERkUAsUkREREQCsUgRERERCWSk7QD0bJBKpYiP/weF
hfdRWSmrc7yzswsaN27cAMmIiIiEY5GiBpGcfB6zfpwLsa1lnWML0/OxCHPh4eHVAMmIiIiEY5Gi
BiO2tYSlQ0ttxyAiIqo3PEeKiIiISCAWKSIiIiKBWKSIiIiIBGKRIiIiIhKIRYqIiIhIIF61R6Tj
pFIpUlLOqzT20qV/NZyGiIgexSJFpONSUs5jelgMzKzs6hybdTUedq81QCgiIgLAIkWkF8ys7GDe
qlOd44ry0gFkaD4QEREB4DlSRERERIKxSBEREREJxCJFREREJBCLFBEREZFALFJEREREArFIERER
EQnEIkVEREQkEIsUERERkUC8IScREdR7FA/Ax/EQ0QMsUkRU7/Tx+YDqPIoH4ON4iOgBFikiqnf6
+nxAVR/FA/BxPET0gNpF6vTp09iwYQNSUlKQk5ODNWvWoG/fvrWuExcXh9DQUFy6dAlt2rRBcHAw
hg0bJjg0Eek+Ph+QiJ4Fap9sXlJSAicnJ8ydOxcikajO8RkZGQgODkb37t2xb98+BAUFYc6cOTh5
8qSgwERERES6Qu09Un5+fvDz8wMAyOXyOsfv2LEDNjY2mD59OgCgQ4cOOHPmDCIiItCzZ091356I
iIhIZ2j89gfnzp2Dj4+P0rJevXohMTFR029NREREpFEaP9k8JycHVlZWSsusrKxQXFwMqVSKxo0b
qzSPgYEIBgZ1H0pUh6GhgdJ/9YU+5lb3987Q0ABGRtr9fLqynTX9/prY1sxc/fz8TquPmRuOPv49
rQuZ9eaqPUtLU5XOyRJCLDbRyLyapk+5mzUzVmu8WGwCCwtTDaVRj7a3s6bfXxPbmpmrn5/faeGY
WfP08e9pXcis8SLVokUL5OXlKS3Ly8tDs2bNVN4bBQD5+fc0skdKLDZBYeF9VFbK6nVuTdLH3MXF
pWqNLyy8j4KCexpKo5rKygpcu3YRxcWlkMnqPh+wSxcXtb7TqiosvF/vcz4+f31va2aufn5tf6f1
8e8OZm44+vj3tCYzq1q4NF6k3N3dcfz4caVlJ0+ehLu7u1rzyGRylf4xE6KyUoaKCv35sj+kT7nV
/b3Thc+WlHQOs36cC7GtZZ1jC9PzsahyLjw8vOo9h6b/ItbEtmbm6ufX9nf6IV3Koipm1jx9/Hta
FzKrXaRKSkpw48YNxRV76enpSE1NRfPmzdG6dWssX74c2dnZCA0NBQCMGjUKkZGR+PrrrzF8+HCc
OnUKsbGxCA8Pr9cPQqQJYltLWDq01HYMIiLSUWoXqeTkZAQFBUEkEkEkEikKk7+/P0JCQpCbm4vM
zEzFeBsbG4SHhyMkJARbt25Fq1atsGjRoipX8hERkWZJpVLEx/+j8iEnZ2fNHK4mepqoXaS6deuG
1NTUGl8PCQmpsszb2xsxMTHqvhUREdWj5OTz6h2uhmYOVxM9TfTmqj0iInpyPFxNVL/06yYXRERE
RDqERYqIiIhIIB7a00M8YZSIiEg3sEjpIZ4wSkREpBtYpPQUTxglIiLSPp4jRURERCQQixQRERGR
QCxSRERERAKxSBEREREJxCJFREREJBCLFBEREZFALFJEREREAvE+UkRERE8hqVSKlJTzKo+/dOlf
DaZ5erFIERERPYVSUs5jelgMzKzsVBqfdTUedq9pONRTiEWKiIjoKWVmZQfzVp1UGluUlw4gQ7OB
6qCPe9FYpIiIiEgn6ONeNBYpIiIi0hn6theNV+0RERERCcQiRURERCTQM31oTyqVIj7+HxQW3kdl
pUyldZydXdC4cWMNJyMiIiJ98EwXqeTk85j141yIbS1VGl+Yno9FmAsPDy8NJyMiIiJ98EwXKQAQ
21rC0qGltmMQEdFTgkc7ni3PfJEiIiKqTzza8WxhkSIiIqpnPNrx7OBVe0REREQCsUgRERERCcQi
RURERCQQixQRERGRQDzZnIiIdJa6txLgbQSoobFIERGRzlLnVgK8jQBpA4sUERHpNN5KgHQZz5Ei
IiIiEohFioiIiEggHtojwaRSKVJSzqs09tKlfzWchoiIqOGxSJFgKSnnMT0sBmZWdnWOzboaD7vX
GiAUERFRA2KRoidiZmUH81ad6hxXlJcOIEPzgYiIiBoQz5EiIiIiEohFioiIiEggFikiIiIigQQV
qcjISPTp0weurq544403kJSUVOPYv//+GxKJROmXk5MT8vLyBIcmIiIi0gVqn2x++PBhLF26FAsX
LoSLiws2b96MiRMn4ujRo7C0rP4W/iKRCLGxsTA1NVUss7KyEp6aiIiISAeovUcqIiICI0eOhL+/
PxwcHDB//nwYGxtj9+7dta5naWkJKysrxS8iIiIifadWkSovL0dKSgp69OihWCYSieDj44PExMQa
15PL5Rg6dCh69eqF8ePH4+zZs8ITExEREekItQ7tFRQUoLKyEtbW1krLrayscO3atWrXadGiBRYs
WIAuXbpAKpUiOjoaQUFB2LVrF5ycnIQnJyIiPmGASMs0fkNOe3t72NvbK352d3dHeno6IiIiEBoa
qvI8BgYiGBiI6jWbkPkMDQ1gZKTdix3Vza2pzIaGmtsO3M7K82qSJnIzc/Xza+L7kZSUorEnDPDP
oTC68m+LPn6n9TGzWkXKwsIChoaGyM3NVVqel5dXZS9VbVxcXNQ+vGdpaQqRqH6LVLNmxmqvIxab
wMLCtO6BGqRubk1lFotN6n3OR+fmdv5vXk3SRG5mrn5+TX0/NPWEAf45FEZX/m3Rx++0PmZWq0g1
atQIzs7OOHXqFPr27QvgwflPp06dwrhx41SeJzU1FS1btlQraH7+vXrfI1VcXKr2OoWF91FQcK9e
c0ilUiQnq7ZrHgAuXkxVa35NZH44r6ZoKrM61P1+6ON2fjh/fedm5urn17fvB/8cCqMr/7bo43da
lzKrWrjUPrT31ltvYdasWejSpYvi9gelpaUICAgAACxfvhzZ2dmKw3abN2+GjY0NOnXqhLKyMkRH
RyMuLg6bNm1S631lMjlkMrm6ceucU12VlTJUVMjqNce5c+dU3jUPqL97XhOZH86rKZrKrA51vx/6
uJ0fzl/fuZm5+vn17fvBP4fC6Mq/Lfr4ndbHzGoXqVdffRUFBQVYtWoVcnNz4eTkhA0bNijuIZWb
m4vMzEzF+PLycoSGhiI7OxvGxsZwdHREREQEvL296+9TPAVU3TUP8AHAREREukLQyeZjx47F2LFj
q30tJCRE6eeJEydi4sSJQt6GiIiISKdp/Ko9Il3CS8WJiKg+sUjRMyUl5bzGLhUnIqJnD4sUPXM0
dak4ERE9e7R71zIiIiIiPcYiRURERCQQixQRERGRQE/dOVK8KouIiIgaylNXpHhVFhERETWUp65I
Abwqi4iIiBrGU1mkiIiI6hNPG6GasEgREVGD0sdSwtNGqCYsUkRE1KD0tZTwtBGqDosUERE1OJYS
elrwPlJEREREArFIEREREQnEIkVEREQkEIsUERERkUAsUkREREQCsUgRERERCcQiRURERCQQixQR
ERGRQCxSRERERAKxSBEREREJxCJFREREJBCLFBEREZFALFJEREREArFIEREREQnEIkVEREQkEIsU
ERERkUAsUkREREQCsUgRERERCcQiRURERCQQixQRERGRQCxSRERERAKxSBEREREJxCJFREREJBCL
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
RU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[49]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># you don&#39;t need to make a new column for a one-off</span>
<span class="p">(</span><span class="n">monthly_mean</span><span class="o">.</span><span class="n">domestic_gross</span> <span class="o">/</span> <span class="n">monthly_mean</span><span class="o">.</span><span class="n">worldwide_gross</span><span class="p">)</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">&#39;Mean Domestic / Worldwide Gross Ratio by month&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[49]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x7fd322e6f518&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAp8AAAIFCAYAAACUFZYtAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3XlYVdUC///P4SApJCqomWNFXQ4xCGIZZlqYI5pDJRlq
jmXltbplZoNlVmplls2mhRlm+jXN1LTMskcjc0gtbn5vKYWmpQxGogjC/v3hl/PzCNjZCEuh9+t5
enpYZ+01nL05fth77X0clmVZAgAAAAzwOdsDAAAAwD8H4RMAAADGED4BAABgDOETAAAAxhA+AQAA
YAzhEwAAAMYQPgEAAGAM4RMAAADGED4BAABgDOETgCTpt99+k8vl0tKlS8/2UM6KgQMHavjw4X9b
LzU1VS6XS1u3bj2j/oqKiuRyufTGG2/8bd0ZM2YoPDz8jPpD5arsffLAAw/oiiuuqLT2agLek5qL
8IkzsmTJErlcrtP+Y9ypUye5XC6NHj3a8OjsiY+Pd88lLCxMV1xxhXr37q2JEydqx44dZ3t4lWb5
8uWaO3duma85HI5K7+/f//637rjjjjJf27Fjh1wuV5njufPOO+VyubRkyZJSryUlJalTp06VOk47
c6+s98nhcHjVlrf17NqzZ4+eeOIJdevWTa1bt1Z0dLQSEhI0efJk/e9//6v0/qrSwIED3b+/LpdL
rVu3Vp8+fTRv3jxV9Fukjxw5oldeeUWbN28u9Vpl75Oq2sfnOpPvMc4dvmd7AKgZateureXLl6tN
mzYe5d9++63++OMPnXfeeWdpZPZcfvnlGj58uCzLUl5ennbt2qVVq1Zp4cKFGjZsmMaPH3+2h3jG
li9frp9++km33XabR3mzZs20fft21apVq9L6On78uL7++ms98MADZb4eHh6uOnXqaMuWLaXGs23b
Nvn6+mrr1q3q16+fu7ywsFA//PCDOnfuXGnjPBucTmelv992rFmzRg888ID8/PzUu3dvhYaGyuFw
aPfu3fr000+1YMECrV27VhdccMFZGZ9dDodDTZs21X/+8x9ZlqWcnBwtW7ZMTz/9tP7880+NGTPG
dpslwcjX11dt27b1eG3s2LG6++67K2v4/1ine49RcxE+USk6duyoVatW6dFHH5WPz/9/Qn358uWK
iIhQTk7OWRyd9xo3bqxevXp5lI0bN07333+/3nnnHbVq1Uq33HLLWRpd1fPz86vU9jZt2qQjR46U
e5bS6XQqKiqq1Fnz9PR05eTkqHfv3tqyZYvHa2lpaTp27FipP3QqKj8/X7Vr166Utuyq7PfbW7/8
8ovGjRunVq1a6Z133lFQUJDH6+PGjdN7773n8btclrP53pWlXr16Hr+/iYmJ6tatm+bNm1eh8Hm6
M6Y+Pj5/+/7g71X0rDSqN35zcMYcDod69eqlQ4cOacOGDe7ywsJCrV69Wr169SrzA8ayLCUnJ6tX
r16KiorS1VdfrYkTJyo3N9ej3ueff6477rhD11xzjSIjI9WlSxe99tprKi4u9qg3ePBg9e7dW7t2
7dLgwYMVHR2tjh07avbs2Wc0Pz8/P02bNk316tUrtT7v6NGjmjp1qq699lpFRkaqe/fuevvtt0u1
4XK59NRTT2nVqlVKSEhQ69atdcstt7gvbS5YsEBdu3ZVVFSUBg8erH379pVqY/v27RoxYoTatm2r
6OhoDR48uFRoy8vL09NPP634+HhFRkaqffv2Gj58uH788Uf3e/Tll19q37597suTJWcQy1vzuXv3
bt1zzz2Ki4tT69at1b17d82YMcOr9+6rr77SpZdeqqZNm5ZbJzY2VllZWdqzZ4+7bOvWrapbt64S
ExO1e/duHTp0yOM1h8Oh2NhYj3bmzZunhIQERUZG6pprrtFTTz2lw4cPe9QZOHCg+vXrpx07dujW
W29VdHS0Zs6cWe7Y9u/fr9GjRysmJkbt27fXtGnTVFBQ4HE8JycnKzw8XEeOHHGXzZo1Sy6XS88/
/7y77Pjx44qJidGLL74oqfw1n99++6369++vqKgodevWTYsWLSp3fEuWLFH//v3VunVrtWvXTvff
f7/++OOPcuufPL78/HxNnTq1VPCUTgSrIUOGqFGjRu6ykvV3v/76q0aOHKk2bdp4XAlYsWKF+vXr
p6ioKMXFxWn8+PE6ePCgR7sHDhzQ+PHj1bFjR0VGRqpDhw66++679fvvv7vr7NixQ8OGDVO7du3U
unVrde7cWY899tjfzqks5513niIiIpSbm+vxB3BBQYFefPFF9e/fX23btlVMTIwGDx7scek3IyND
11xzjRwOh1588UX370vJ/iprzefx48f1yiuv6Prrr1dkZKQ6d+6sl156SYWFhV6POSMjQ8OGDVNM
TIw6duyo119/3f2aZVm69tprNXbs2FLb5efnKyYmRpMnTy637ZJjbsqUKVq5cqV69uzp/iz6+eef
JUkpKSnq0qWLoqKidNttt3nsmxLe7OuS4+X33393/w7FxcV5/E783Xtc4nRtoHrizCcqRbNmzdS6
dWutWLFC11xzjSRp3bp1Onz4sBISEvTuu++W2uaxxx7T0qVLdeONN2rIkCHau3ev5s2bp507d+r9
99+X0+mUdOIf2ICAAA0fPlz+/v765ptvNHPmTOXl5WncuHEebf75558aNWqUunTpooSEBK1evVrT
p09XaGioe1wV4e/vry5dumjx4sXatWuXQkJCJEmjR4/Wpk2bdNNNN8nlcmn9+vV69tlndeDAAT30
0EMebWzatElr167VrbfeKkl68803NXr0aI0YMUILFizQrbfeqtzcXL311lt6+OGHlZyc7N42NTVV
t99+uyIiIjRmzBj5+Pjoww8/1G233ab58+crMjJSkjRx4kR99tlnGjRokEJCQnTo0CFt2bJFu3bt
UlhYmO666y49++yz+uOPP/Twww/Lsiz5+/uXO++dO3cqKSlJfn5+SkxMVLNmzZSRkaEvv/xS9913
39++b+vWrdN111132jqxsbGyLEtbtmxRixYtJJ0ImK1bt1ZUVJR8fX313XffudvZunWrAgIC5HK5
3G3MmDFDb775pq655hrdeuut2r17t+bPn68ffvhB8+fPd5+hcjgcysrK0ujRo9W7d2/169fPI2Cd
7OjRoxoyZIgyMzM1ZMgQBQcHa+nSpfr666891qHFxsaquLhYW7duVYcOHdxjdDqdHmEmLS1N+fn5
uvLKK8t9L3bu3KlRo0apUaNGuueee1RYWKiXXnpJwcHBpeq+8sorevXVV9WrVy8NGDBAWVlZevfd
d/X999+7f2fKs27dOl1yySUKCwsrt86pHA6Hjh8/rhEjRqhdu3aaMGGC6tSpI0latGiRHnvsMUVH
R2vcuHE6ePCg5s6dq++++85jLHfffbcyMjI0ePBgXXjhhcrKytL69ev1+++/q0mTJsrMzNSIESPU
uHFj3XnnnQoICNBvv/2mtWvXej3OU+3du1c+Pj6qW7euuyw3N1dLlixRQkKCEhMTdfjwYS1atEjD
hw/X4sWLddlll6lhw4aaOHGinnzySXXv3t39R1rJe1bWesSHHnpIy5cvV0JCgmJjY7V9+3a9/vrr
Sk9Pd//RcTqFhYUaOXKkYmNjNW7cOH311Vd66aWXZFmW7rrrLjkcDvXu3VvvvvuuDh8+rPPPP9+9
7Zo1a5Sfn68+ffr8bT8bN27UmjVrNHDgQBUXF2vWrFkaPXq0brvtNi1atEiDBg3SoUOH9NZbb+mR
Rx7RnDlz3Nt6u69Ljpfhw4erbdu2euihh7RhwwbNmTNHrVq10s033/y373HJe3K6NlBNWcAZ+PDD
Dy2Xy2X98MMP1nvvvWfFxsZax44dsyzLsu655x7rtttusyzLsq677jrrjjvucG+3adMmKzQ01Fqx
YoVHe+vXr7dCQ0Ot5cuXu8tK2jvZxIkTrejoaKugoMBdNmjQIMvlclnLli1zlxUUFFhXX321NXbs
2L+dy6ljPFVycrLlcrmstWvXWpZlWZ999pkVGhpqvfnmmx71xo4da4WFhVkZGRnustDQUCsqKsra
t2+fu+yDDz6wQkNDrQ4dOlhHjhxxl7/wwguWy+WyfvvtN3dZ165drVGjRnn0c+zYMatz587W8OHD
3WVt27a1Jk+efNp53nHHHVZ8fHyp8r1791qhoaHWkiVL3GVJSUlWbGys9fvvv5+2zbLs2bPHCg0N
tTZt2nTaeocPH7Yuv/xy69FHH3WXde/e3Xr11Vcty7Ksm2++2Xruuefcr8XFxXnM+eDBg1Z4eHip
fTd37lzL5XJZH330kbts4MCBlsvlshYvXlxqHAMHDrSGDRvm/nnOnDmWy+Wy1qxZ4y47evSo1blz
Z8vlcllbtmyxLMuyjh8/bkVHR1szZsywLMuyiouLrSuuuMK69957rYiICPfx+9Zbb1nh4eFWXl6e
e7vQ0FDr9ddfd7d/xx13WNHR0daBAwfcZT/99JMVFhZmhYeHu8syMjKssLAwa86cOR5z2Llzp3X5
5Zdbs2fPLjW/EocOHbJCQ0Ote+65p9Rrubm5VnZ2tvu/k3/3HnjgAcvlclkzZ8702ObYsWNWu3bt
rH79+nn8Pq5Zs8YKDQ21XnvtNcuyLCs7O9sKDQ215s6dW+7YVq1aZblcLmvnzp3l1inPwIEDrd69
e7vHvnv3bmvKlClWaGioNWbMGI+6RUVFVmFhYam5X3XVVdbEiRPdZQcPHiy1j0rMmDHDY5/88MMP
VmhoqDVp0iSPes8884zlcrmszZs3n3b8Je/v1KlTPcpHjBhhRUVFWX/++adlWZb1888/W6Ghodai
RYs86o0aNcrq2rXrafsoOeZat27t8TudkpJihYaGWh07drSOHj3qLn/22Wctl8vlruvtvj55PrNm
zfIYww033GAlJia6fz7de+xtG6h+uOyOStOjRw/l5+friy++UF5enr788kv17t27zLqrV69WYGCg
rrrqKuXk5Lj/CwsLk7+/vzZu3Oiue/K6uLy8POXk5Cg2Nlb5+fnavXu3R7v+/v4efdaqVUtRUVEe
l3QrquQMYV5enqQTl5R9fX01aNAgj3rDhw9XcXGxvvrqK4/yuLg4XXjhhe6fo6KiJEndunVzn0E6
ubxkzD/++KN+/fVXJSQkeLxXhw8fVlxcnMfZtbp162r79u06cODAGc83Oztbmzdv1k033VShm06+
/PJLBQYG/u3azICAAIWGhrrXdmZnZys9Pd29XZs2bdzLC9LT05Wdne1xyX3Dhg0qKioqdcPSLbfc
ojp16mjdunUe5bVr1/bq7NBXX32lCy+80OPGptq1a2vAgAEe9ZxOp2JiYtz74f/+3/+rv/76S3fc
cYeOHz+ubdu2SZK2bNmi0NDQcs80l9yc1a1bN4+zsZdeeqni4uI86q5evVoOh0Ndu3b1OCYaNWqk
5s2be/z+nKpkKUJZ47j11lsVFxfn/m/BggWl6py65nnHjh06dOiQbr31Vo+bpzp37qxWrVq5339/
f3/5+vpq48aN+uuvv8ocW2BgoCzL0tq1a1VUVFTuHMrzv//9zz32Hj16KDk5WV26dNHTTz/tUc/H
x0e+vicu/FmWpT///FOFhYWKiIjQf//7X9v9SifOJjscDg0dOtSjvOQGxlOPw/IkJSV5/Dxo0CAV
FBTom2++kSSFhIQoPDxcH3/8sbtOdna2vv76a91www1e9dGhQweP3+nWrVtLOvEZfvIa3pLyks8i
b/f1yRITEz1+jo2Ntf15XBlt4NzCZXdUmqCgIMXFxWn58uU6evSoiouL1a1btzLr/vrrr8rNzVX7
9u1LvVZyabTEzz//rBkzZmjjxo0ea/gcDkepf8SaNGlSqr169epVymNjStb0lVxW2rdvnxo3blzq
H/GSS/Knrts8OXhKcl8GPHXMdevWlWVZ7rWvv/zyiySVe6e9j4+P/vrrL9WtW1fjxo3ThAkTdO21
1yo8PFydOnVSnz593Jez7di7d6+kE+GnItatW6err77aq5sy2rRpo5SUFB06dEjfffedfH193f/w
xcTE6P3331dhYWGZ6z1L3ueLL77Yo00/Pz81a9ZMv/32m0d5kyZN3Es6Tmffvn1q2bJlqfJT+5FO
/GM4a9YsFRYWasuWLbrwwgvlcrl02WWXafPmzbryyiu1detW9e3bt9z+srKyVFBQUG6fJwfKjIwM
FRUV6frrry9V1+FweFyOPVXJ8XvyGtUSTz/9tPLy8spcNiKdeE9PXaawb98+ORwOXXTRRWWOOy0t
TdKJ9Zf/+c9/NH36dMXFxSkmJkbXXnut+vbt615WcNVVV6lLly6aOXOm3n77bV155ZW6/vrrlZCQ
4NXNWa1atdKkSZNUXFysX3/9VW+88Yays7PLfNrG4sWLlZycrPT0dB0/ftxdXtY8vLFv3z45nc5S
+++CCy5wLx/4O06nU82bN/cou+iii2RZlsf2ffv21dSpU/XHH3/oggsu0CeffKKioiKvw2dZnznl
lZ/8WeTtvi7h7++vwMBAj7LAwED9+eefXo2zstrAuYfwiUrVq1cvPfbYYzp48KA6duxY7j+CxcXF
atiwoZ5//vkyb0YquQnir7/+UlJSkgIDA3XvvfeqRYsW8vPzU1pamqZPn15q2/KCTll92FUSYMsK
B94oL/CUV14y5pL/P/TQQwoNDS2zbkkA7tGjh6644gp99tln7rVRb731ll555ZUzWvNqV35+vr79
9ltNmjTJq/qxsbFKSUnR1q1b9d133+lf//qX+2xwTEyMCgoK9P3337vXUkZHR1d4bFVxd3ZsbKwK
Cgq0fft2bdmyxR2O27Ztqy1btuinn37Sn3/+WWmPkikuLpavr6/eeuutMl8/3XrP+vXrKygoSD/9
9FOp10rOumdkZJT5O3Omj0wbPny4unTpojVr1mj9+vV68cUXNWvWLM2bN0//+te/5HA49PLLL2vb
tm364osvtH79ek2YMEFz587VggUL/nbf+fv766qrrpIktW/fXq1bt9ZNN92kF1980eOPtw8//FCP
PPKIunXrpttvv11BQUHy8fHRa6+9VilXDapaQkKCpk2bpuXLl2vEiBH6+OOP1bp1a6//yCzvM6ey
Pz+9+SPPRBs49xA+Uam6dOmixx9/XNu3bz/tHdEtW7bUN998ozZt2pz2jMbGjRuVm5ur1157zeNs
l+lLLkeOHNGaNWt04YUXus9sNm3aVN98842OHDnicfZz165d7tcrQ8k/KAEBAaUuv5alYcOGGjhw
oAYOHKjs7Gz169dPb7zxhu3wWXIGpqyQ8ndSU1NVWFiojh07elW/5KajzZs3a9u2bR6X6hs3bqwL
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
2rRp436vyrp7/t5771XDhg31/vvva+rUqapfv74GDhyoe++9t9RZrtMdCye/5u/vr3fffVdPPvmk
5s2bJ39/f91www2Ki4sr87vq27Ztq3feeadUyCi5M7es9Z6n7v+wsDDNnj1b06ZN08svv6wmTZro
vvvu0969ez3CpyTdeeedCgkJ0dy5c91nQC+88EJ16tTJq6UGXbp00bJly/TOO+9o/fr1Wrx4sfsr
Kq+//nolJibqsssuK/f9OdnNN9+sgIAAzZ49W88//7z8/f3VvXt33X///e71p02bNlVCQoJSU1P1
0UcfydfXV5dccolefvll93jbtWuntLQ0rVixQllZWapbt66io6M1ZsyYUsdEWcob34gRIzR8+HCl
pKRo9OjRuvnmm5WVlaWFCxdq/fr1CgkJ0QsvvKBly5Zpx44dHts+88wzevrppzVlyhQVFhbqnnvu
KTcYTZ06Va1atdLSpUv16aefqlGjRrrrrrt01113/e3YpRPhbs6cOXr88ce1atUq1a1bV2PHjvW4
4nJy3e7du2vRokW2liOc7jPHm88ib/Z1eduW53TvMZflayaHVRl3YgDA/zN79mwlJydr/fr1Z3so
QI321FNPadmyZVq/fv1Z+6pWoCIqtOYzJSVF8fHxioqK0oABA0r9pXiqgoICzZgxw/2Vf507d9aH
H35YoQEDOLc1b95cDz/88NkeBlCjHT16VB9//LG6d+9O8ES1Y/uy+8qVKzV16lRNnjxZkZGRmjt3
rkaOHKlVq1aVu5j+nnvuUU5Ojp555hm1bNlSBw8etLWgHUD10b1797M9BKDGysrK0tdff61PPvlE
hw8frtA6S+Bss33ZfcCAAYqKitKjjz4q6cRi5E6dOmnw4MEaNWpUqfpfffWVHnjgAa1Zs6bUgmkA
AOC91NRUDRs2TA0bNtTYsWO9upENONfYOvNZWFiotLQ0j8X2DodD7du3d3+F3Km++OILRURE6K23
3tJHH32kOnXqKD4+Xvfee+8ZP7AYAIB/kri4OO3cufNsDwM4I7bCZ05OjoqKitSwYUOP8uDg4FIP
QS6xZ88ebd68WX5+fnr11VeVk5OjJ554Qn/++aeeeeaZio8cAAAA1U6VP2Tesiz5+Pho+vTpioyM
VMeOHTVhwgQtXbrU1kODuSkfAACg+rN15rNBgwZyOp3KzMz0KM/Kyip1NrREo0aNdMEFF3g8/+uS
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
6NHavn271+ETAAAA1Z+tONugQQM5nU5lZmZ6lGdlZZU6G1qiUaNGysrKKlX//PPPJ3gCAAD8w9gK
n7Vq1VJ4eLhSU1PdZZZlKTU1VTExMWVuEx0d7VFfkjZs2KDo6OgKDBcAAADVme0L+UOHDtWiRYu0
dOlS7dq1S48//rjy8/PVv39/SdL06dM1fvx4d/1bbrlFe/bs0XPPPafdu3crJSVFq1ev1rBhwypv
FgAAAKgWbN1wJEk9e/ZUTk6OZs6cqczMTIWFhWn27NkKCgqSJGVmZmr//v3u+s2bN9esWbM0ZcoU
zZs3T02aNNFTTz1V6g54AAAA1Hy2bjgCAAAAzgTf7Q4AAABjCJ8AAAAwhvAJAAAAYwifAAAAMIbw
CQAAAGMInwAAADCG8AmcBTzhDADwT2X7IfMAzlxkZKQ++ugjhYSEnO2hADDkwIEDev/997VlyxYd
PHhQPj4+atGihTp37qz+/fvL6XSe7SECRvCQ+XLs379fM2fO1JQpU872ULySn5+vH374QfXr19el
l17q8dqxY8f0ySefqG/fvmdpdPbt2rVL27ZtU3R0tEJCQrRr1y69++67Kigo0A033KC4uLizPUSv
lHf8vPvuu7rhhhtUv359SdKECRNMDqvSHDlyRJ988okyMjLUqFEjJSQkqEGDBmd7WF5LS0tTYGCg
WrRoIUlaunSpFixYoP3796tp06YaNGiQEhISzvIovTd58mT16NFDbdu2PdtDqRTvvfeeduzYoU6d
OikhIUFLly7VrFmzVFxcrK5du2rs2LHy9a0e51C+//57DRs2TC1btlTt2rW1bds29erVS4WFhVq/
fr1CQkI0e/ZsnX/++Wd7qECVI3yWY+fOnerXr59+/PHHsz2Uv5Wenq4RI0Zo3759cjgcio2N1Qsv
vKDGjRtLOvGVp9dcc021mIskffXVV7rrrrsUEBCgo0eP6pVXXtH48ePlcrlUXFysTZs2ac6cOdUi
gLpcLrlcLtWtW9ejfNOmTYqIiFCdOnXkcDj07rvvnqUR2tOzZ0/Nnz9f9evX1/79+5WUlKTc3Fxd
dNFFysjIkK+vrz744AN3mDvX3XDDDXrooYfUvn17LVq0SE899ZRuvvlmhYSEKD09XYsWLdIjjzyi
m2666WwP9f9r796Doir/P4C/DzeRRVAuolCQNsACgmyyKUheQDItx1thKAGaAouXZUTw1hhSaQYk
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
rkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Let's-get-month-names-on-the-x-axis-instead-using-calendar-library">Let's get month names on the x-axis instead using <code>calendar library</code><a class="anchor-link" href="#Let's-get-month-names-on-the-x-axis-instead-using-calendar-library">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[50]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">calendar</span>

<span class="c1"># we have the option of full name of month, or abbreviated name</span>
<span class="nb">print</span><span class="p">(</span><span class="n">calendar</span><span class="o">.</span><span class="n">month_name</span><span class="p">[</span><span class="mi">1</span><span class="p">:</span><span class="mi">4</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="n">calendar</span><span class="o">.</span><span class="n">month_abbr</span><span class="p">[</span><span class="mi">1</span><span class="p">:</span><span class="mi">4</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&#39;January&#39;, &#39;February&#39;, &#39;March&#39;]
[&#39;Jan&#39;, &#39;Feb&#39;, &#39;Mar&#39;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[51]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># map over the index of using calendar&#39;s month names</span>
<span class="n">monthly_mean</span><span class="o">.</span><span class="n">index</span> <span class="o">=</span> <span class="n">monthly_mean</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">map</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">calendar</span><span class="o">.</span><span class="n">month_abbr</span><span class="p">[</span><span class="n">x</span><span class="p">])</span>
<span class="n">monthly_mean</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[51]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rank</th>
      <th>male</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>1195928753192</td>
      <td>0.674300</td>
      <td>3.260153e+07</td>
      <td>3.810404e+07</td>
      <td>7.400509e+07</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>1059027777788</td>
      <td>0.635417</td>
      <td>4.066693e+07</td>
      <td>4.773956e+07</td>
      <td>9.061837e+07</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>855614973272</td>
      <td>0.664439</td>
      <td>4.960052e+07</td>
      <td>6.042128e+07</td>
      <td>1.255552e+08</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>1133720930244</td>
      <td>0.635174</td>
      <td>3.608773e+07</td>
      <td>4.362819e+07</td>
      <td>9.773371e+07</td>
    </tr>
    <tr>
      <th>May</th>
      <td>1255349500721</td>
      <td>0.670471</td>
      <td>8.347447e+07</td>
      <td>1.177966e+08</td>
      <td>2.914820e+08</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>1754601227000</td>
      <td>0.693252</td>
      <td>7.135558e+07</td>
      <td>1.056504e+08</td>
      <td>2.331871e+08</td>
    </tr>
    <tr>
      <th>Jul</th>
      <td>1550190597212</td>
      <td>0.691233</td>
      <td>6.919861e+07</td>
      <td>1.067479e+08</td>
      <td>2.508663e+08</td>
    </tr>
    <tr>
      <th>Aug</th>
      <td>1179487179497</td>
      <td>0.685897</td>
      <td>3.949550e+07</td>
      <td>5.043031e+07</td>
      <td>9.527081e+07</td>
    </tr>
    <tr>
      <th>Sep</th>
      <td>936675461754</td>
      <td>0.646438</td>
      <td>3.078705e+07</td>
      <td>3.375987e+07</td>
      <td>6.493184e+07</td>
    </tr>
    <tr>
      <th>Oct</th>
      <td>1147928994095</td>
      <td>0.649704</td>
      <td>3.106601e+07</td>
      <td>3.545069e+07</td>
      <td>7.204215e+07</td>
    </tr>
    <tr>
      <th>Nov</th>
      <td>1331133113321</td>
      <td>0.695270</td>
      <td>5.857765e+07</td>
      <td>8.035767e+07</td>
      <td>1.899561e+08</td>
    </tr>
    <tr>
      <th>Dec</th>
      <td>1408345752617</td>
      <td>0.667660</td>
      <td>5.358927e+07</td>
      <td>7.840979e+07</td>
      <td>1.848689e+08</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[52]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># now we have month abbreviations as x lables when we plot</span>
<span class="p">(</span><span class="n">monthly_mean</span><span class="o">.</span><span class="n">domestic_gross</span> <span class="o">/</span> <span class="n">monthly_mean</span><span class="o">.</span><span class="n">worldwide_gross</span><span class="p">)</span><span class="o">.</span><span class="n">plot</span><span class="o">.</span><span class="n">bar</span><span class="p">(</span><span class="n">title</span><span class="o">=</span><span class="s1">&#39;Mean Domestic/Wordwide Gross Ratio by month&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[52]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x7fd3209150f0&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAp8AAAH5CAYAAADHrVXSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3XlcVXXi//H3BcQFJVkyR0ssMy6xiWuoqWFpLqRZbhFm
btmMme3ZYpnOuJQ5ObZYOuGUlvpVmkLSyRadDCs0tUgbx0iz3MBbKC7I5fz+8McdrxfsXpCPQq/n
4+GjR5/7OZ/lnsPlzTmfc67NsixLAAAAgAF+53sAAAAA+P0gfAIAAMAYwicAAACMIXwCAADAGMIn
AAAAjCF8AgAAwBjCJwAAAIwhfAIAAMAYwicAAACMIXwC+E0//fST7Ha73nnnnfM9lCq3bNky2e12
7d+/v1Lt7N69W3a7Xe+9995v1n3wwQfVo0ePSvWHc+tc75OhQ4fq5ptvPmft1QS8J79fhE9UmfT0
dNntdtntdm3atKnMOl27dpXdbtfYsWMNj843SUlJrrlERUWpXbt2Sk5O1qRJk7R169bzPbxzJiMj
QwsXLizzNZvNVuF2LctSYmKiFixYoDFjxqh9+/YedbZt2ya73a6kpCSP1zZs2CC73a5ly5ZVeAy+
qMxcK9KOzWY7Z32ebtu2bXrkkUeUlJSkuLg4tW7dWjfffLNmzZqln3766Zz3V5W6dOni+hm02+1K
SEjQoEGD9O6771a4zf3792vu3Ln6z3/+4/Haud4nVbF/q4Pfeo/x+xRwvgeAmq9OnTrKyMhQ69at
3cq/+OIL7d+/X7Vr1z5PI/PN1VdfrREjRsiyLBUWFmrnzp1atWqVli5dqjvvvFOPPPLI+R5ipWVk
ZGjHjh2644473MqbNm2qLVu2qFatWhVqd8uWLfrll1/UrVs3FRcX69///rd27Nihli1buups2rRJ
AQEB2rt3r/bv369LLrnE7TWbzeZxDF3ImjVrpi1btigwMPC89L948WL9+c9/VmhoqJKTk3XFFVeo
uLhY//nPf7RixQotXLiwWv3hZLPZFBMTo+HDh8uyLB04cEDLli3Tww8/LKfTWaEzaPv27dPcuXMV
ERGhq666yu216dOny7KsczX8362zvcf4/SJ8osp16dJFq1at0hNPPCE/v/+dbM/IyFBMTIwcDsd5
HJ33GjVqpL59+7qVPfTQQ3rggQf0+uuvKyIiQkOGDDlPo6t6lQlRa9euVZMmTdSiRQs5HA5ZlqWN
Gzd6hM+uXbtqw4YN2rhxo3r37u16bePGjWrYsKFatGhRqTlI0okTJ4z9wXO+gueXX36pqVOnqn37
9nrllVdUp04dt9cfffRRvfjii7/ZzvHjxz22PZ8aN27s9jPYv39/XX/99UpLS6tQ+DxbuPT396/Q
GOGOAI+ycNkdVcpms6lv37765ZdftH79elf5yZMntXr1avXt27fMDyfLspSWlqa+ffsqLi5OnTp1
0qRJk1RQUOBW78MPP9Rdd92la6+9VrGxsbrhhhv00ksvqaSkxK1eamqqkpOTtXPnTqWmpqpVq1bq
0qWL5s+fX6n5BQYGasaMGbrooov0yiuvuL127NgxTZ8+Xd26dVNsbKxuvPFG/f3vf/dow263a+rU
qVq1apX69Omj+Ph4DRkyxHWZ6u2331aPHj0UFxen1NRU/fzzzx5tbNmyRSNHjlTbtm3VqlUrpaam
eix1KCws1J///GclJSUpNjZWHTt21IgRI7Rt2zbXe/TJJ5/o559/dl3a7N69u6Ty13x+//33uvfe
e5WYmKj4+HjdeOONmj17tsf41q5dq27dukmS4uLiVKtWLY/xbdq0Se3atVNcXJzba5ZlacuWLUpI
SHCrv3v3bo0fP17t27dXq1atNGTIEP373/92q5OVlSW73a5Vq1bp+eefV5cuXZSQkKBjx45Jkr77
7julpqYqPj5e3bp107x58zzGPnXqVHXq1Mmt7KmnnpLdbtdbb73lKtu/f7/b0oDy1nyWHvdxcXG6
6aab9OGHH3r0WTrv119/XX369FFsbKw6d+6sp59+WkeOHCmz/unmzp2rgIAAPffcc2WGx8DAQN13
331uZaXr77Zu3arbbrtNrVq10pw5c1yvv/HGG66xXHvttZo6darHWHJzczVu3Dh16tRJcXFx6tat
mx544AEdPXrUVWfdunUaOnSo2rVrp4SEBN1444164YUXfnNOZQkLC1Pz5s21e/dut3KHw6Hp06cr
OTlZCQkJatu2rcaMGeN26TcrK0tDhgyRzWbTQw895FpSU7q/ylrzWVhYqL/85S/q2rWrYmNj1atX
L6Wlpfk05q+//lpDhgxRfHy8rr/+ei1dutT12pEjRxQfH68ZM2Z4bPfzzz8rKiqqzM+QUqXH3D/+
8Q+9+eab6t69uxISEjRy5EgdOHBAlmVp7ty56tq1q+Lj43XPPfeUeTx5s69Lj5cdO3a4foa6dOmi
119/3VXnt97jUmdrAzUTZz5R5Zo2bar4+HitXLlS1157raRTYeTIkSPq06eP/vGPf3hs8+STT+qd
d97RLbfcomHDhmnPnj164403tH37dr311luusxLp6ekKCgrSiBEjVK9ePW3YsEFz5sxRYWGhHnro
Ibc2f/31V40ePVo33HCD+vTpo9WrV2vWrFmKjIx0jasi6tWrpxtuuEHLly/Xzp07XWfnxo4dqy+/
/FK33nqr7Ha7Pv30U82cOVMHDhzQo48+6tbGl19+qY8++ki33XabJGnevHkaO3asRo4cqbffflu3
3XabCgoK9Nprr+mxxx5z+4WXlZWlMWPGKCYmRuPGjZOfn59WrFihO+64Q4sXL1ZsbKwkadKkSfrg
gw90++23q0WLFvrll1+0ceNG7dy5U1FRUfrjH/+omTNnav/+/XrsscdkWZbq1atX7ry3b9+ulJQU
BQYGavDgwWratKl2796tTz75xC3Y5OXladu2bZowYYKkU8EnOjpaGzdudNXZt2+f9u7dq4SEBP36
669au3at67XvvvtOR44cUZs2bVxlBw8e1JAhQ1RcXKzU1FQ1aNBA6enpuuuuu/Tiiy/quuuucxvr
3LlzVbt2bY0aNUrHjx9XQECADhw4oGHDhsnPz09jx45V7dq1tWTJEo+w1rZtWy1atEi5ubm6/PLL
JZ0Kyv7+/srOztbQoUMlSdnZ2bLZbGrXrl2579natWt133336aqrrtIDDzwgh8OhRx55RI0bN/ao
+9hjjykjI0O33HKL7rjjDv3444968803tX37di1evNjtKsLpCgsLlZ2drU6dOik8PLzcsZzJZrMp
Pz9fY8eOVXJysm6++WZdfPHFkqTZs2dr3rx5uvbaa3Xbbbfp+++/1+LFi/XNN9+4xlJUVKSRI0eq
pKREd9xxh8LCwrRv3z59/PHHOnLkiOrVq6fvvvtOf/zjHxUTE6N7771XgYGB+uGHH/TVV195Pc7T
FRcXa//+/brooovcykuPw549e+rSSy9VXl6e3nrrLaWmpiozM1NhYWFq2bKlxo0bp7lz5+q2225z
/XFTurTjzDWflmXprrvu0qZNmzRw4EBFRkZq3bp1mj59ug4ePOjxeVMWh8OhsWPHqk+fPkpOTtbK
lSs1adIk1a5dW/369VP9+vXVvXt3ZWZmeizjee+99+Tn56fk5OTf7Cc9PV1Op1PDhg2Tw+HQggUL
dN999ykhIUFfffWVxowZo9zcXC1atEghISF65plnXNt6s69L3x+Hw6HRo0erV69e6tOnj95//33N
nDlTdrtdiYmJv/kel74nZ2sDNZQFVJEVK1ZYdrvd+uabb6w333zTatOmjXXixAnLsizr3nvvte64
4w7Lsizruuuus+666y7Xdl9++aUVGRlprVy50q29Tz/91IqMjLQyMjJcZaXtnW7SpElWq1atrKKi
IlfZ7bffbtntduvdd991lRUVFVmdOnWyxo8f/5tzOXOMZ0pLS7Psdrv10UcfWZZlWR988IEVGRlp
zZs3z63e+PHjraioKGv37t2ussjISCsuLs76+eefXWVLliyxIiMjrc6dO1tHjx51lT///POW3W63
fvrpJ1dZjx49rNGjR7v1c+LECat79+7WiBEjXGVt27a1pkyZctZ53nXXXVZSUpJH+Z49e6zIyEgr
PT3dVZaSkmK1adPG2rdv31nbXLZsmdWqVSu3fTVz5kzLbrdb+/fvtyzLsjIyMqz4+Hjr5MmT1tq1
a63o6GirsLDQsizLevPNNy273W599dVXru2feeYZy263W1u2bHGVHT582LruuuusHj16uMo+++wz
KzIy0urZs6fb8VDaRlRUlLVt2zZXWX5+vtW6dWvLbre75nXw4EErMjLSWrp0qWVZlvXLL79Ydrvd
mjBhgtW1a1fXtpMnT7Y6derk+v9du3ZZkZGRbsdc3759rW7durnt03Xr1lmRkZFu496wYYMVGRlp
rVq1ym3Mn3zyiRUZGWm9//775b7fOTk5VmRkpDVz5kyP1xwOh3Xo0CHXv9Pfk6FDh1p2u91avny5
2zYHDx60oqOjPY7/hQsXWna73frnP/9pWZZlff3111ZkZKT14Ycflju2BQsWWHa73Tp8+HC5dcrT
pUsXa8yYMa6xf/fdd9b9999v2e12a9q0aW51z9zXlmVZu3fvtmJiYtx+Jjdv3uyxj0o9+OCDbvtk
1apVVmRkpDV//ny3euPGjbOuvvpqt5/JspS+v2+++aar7MSJE1ZycrJ17bXXWiUlJZZlndrHdrvd
+uyzz9y279u3r3XnnXeetY/SY+7Mz42ZM2dakZGR1oABAyyn0+kqv/fee634+HhXmbf7+vT5nP45
feLECSsxMdG6//77XWVne4+9bQM1D5fdYUSvXr10/PhxffzxxyosLNQnn3xS7l/wq1evVnBwsK65
5ho5HA7Xv6ioKNWrV0+ff/65q+7pa+oKCwvlcDjUpk0bHT9+XN9//71bu/Xq1XPrs1atWoqLi9OP
P/5Y6fmVniEsLCyUdOrSYkBAgG6//Xa3eiNGjFBJSYnWrVvnVp6YmKg//OEPrv+Pi4uTJPXs2VN1
69b1KC8d87Zt27Rr1y716dPH7b06cuSIEhMTlZ2d7dq2QYMG2rJliw4cOFDp+R46dEjZ2dm69dZb
3W4MKsu6devUoUMHt33Vpk0bWZblGt9XX32l6OhoBQQEKCEhQU6nU1u2bJF06ixj7dq1FRMT49Zm
QkKC6/2QpPr162vgwIHavXu3cnNz3cYwYMAAj5ul1q1bp9atW8tut7vKQkND1adPH7d64eHhioiI
cI01OztbgYGBuvPOO7Vv3z7XXePZ2dlnvSFq37592rFjhwYMGOC2T6+99lo1b97cre7q1avVsGFD
tW/f3m2/xsbGqk6dOm4/A2cqvTxa1lnr6667TomJia5/Zx6HderUUb9+/dzK1q9fL6fT6XET2pAh
Q1S3bl3XWerg4GBJp97XEydOlDm2Bg0aSJLWrFlT7vjPZt26da6x33TTTcrMzNTAgQP1wAMPuNU7
fV87nU798ssvCgoKUkREhL799tsK912rVi2lpKS4lQ8fPlxOp9NjyUdZAgMDNXDgQLf/Hzx4sA4e
POga17XXXquwsDC3S9Pbtm3Tjh07dNNNN3k11t69e7sdY/Hx8ZJOrZE9/Yx5fHy8Tpw44fpM8HZf
l2rQoIHb2uzAwEDFxsb69Jl6LtpA9cNldxgRGhqqxMREZWRk6NixYyopKVHPnj3LrLtr1y4VFBSo
Y8eOHq+VXhos9d///lezZ8/W559/7rYmyWaz6fDhw27blnVp86KLLirzESC+Kl3TFhQUJOnU+qxG
jRp5BIDSS/Jnrts8PXhK//slfeaYGzRoIMuyXGtff/jhB0kq9057Pz8/HT58WA0aNNBDDz2kiRMn
qlu3boqOjlbXrl3Vr18/XXbZZb5OV3v27JEkXXnllWetV1xcrM8++0wPPvigW3nr1q1ls9m0adMm
9e7dW5s2bXKtq2zQoIGuvPJKbdy4UYmJifrqq68UGxurgID/fVzt3bu3zMc1nf7+ll4il6RLL73U
o255bVxxxRUeZW3atHEFvo0bNyouLk6xsbFq0KCBsrOz1aBBA+3YsUO33nprue9FaUht1qyZx2uX
X3652x9Lu3bt0i+//FLmZcczfwbOVHoMnr7OstSrr76q4uJiffvtt3ruuec8Xm/cuLHHjTalx+rp
76d0KiQ0bdrUbV7Dhg3TG2+8oXfeeUdt27ZVUlKSbrrpJtWvX1+SlJycrOXLl2vixImaOXOmEhMT
1aNHD/Xo0cOrx+4kJCRo/Pjxrrv2X375Zf36668ef1iUlJQoLS1Nb7/9tn766Sc5nU5Jp9673/pj
qTw///yzGjdu7LEso7yf6bJccsklHjehNW/eXJZl6aefflJ0dLT8/PzUt29fLV++XE8//bQCAwP1
7rvvqm7dul4/d9Tbz5PS/fLrr7+qcePGXu/rUmV9pgYHB7s+l7xxLtpA9UP4hDF9+/bVk08+qYMH
D6pLly6uD74zlZSUKDw8XM8991yZNyOFhoZKkg4fPqyUlBQFBwdrwoQJuuyyyxQYGKicnBzNmjXL
Y9vy1siV1YevSgNsWcHCG+XdWVteeemYS//76KOPKjIyssy6pQG4V69eateunT744AOtX79eCxYs
0Guvvaa5c+dWas3r2WRnZ6uwsFBdunRxK2/YsKGuuOIKbdq0SUePHtV3332ncePGuV5PSEjQpk2b
tH//fv38889erXM7m8re3d6mTRulp6dr3759rlBc+uinjRs3utYctm3btlL9lCopKVGjRo00c+bM
Mo/PsLCwcreNiIiQv7+/duzY4fHa6etRy2q3sne2P/bYY7r11lv14Ycfav369ZoyZYrmz5+vJUuW
6OKLL1adOnX01ltvacOGDVq7dq3+/e9/a+XKlerUqZMWLFjwm+2HhobqmmuukSR17txZERER+tOf
/qQ333zT7SrDiy++qBdffFGDBg1SYmKiLrroItlsNk2ZMqVa3H3dv39/paWl6aOPPlLPnj2VmZmp
7t27n3UN9unK+6w715+B5+KJADxV4PeJ8AljbrjhBj311FPasmVLmXdEl2rWrJk2bNig1q1bn/VR
NZ9//rkKCgr00ksvud2MYvpyzdGjR7VmzRr94Q9/cJ0FadKkiTZs2KCjR4+6/cLYuXOn6/VzofSs
ZVBQkFeL88PDwzV06FANHTpUhw4d0s0336xXXnnF5/BZeiaxrIBzurVr1+rKK68sc75t2rTRihUr
tH79epWUlLjdzZ6QkKCVK1e6zjaevn+lU2d2zry0Lvn2/v7hD3/Qrl27PMrPXK4h/S9Urlu3Tjk5
Obrnnntc5StWrFBwcLCCgoIUFRVVbn9NmzaVpDL7PHMul112mbKzs9WmTRufn61av359tWnTRhs2
bFBeXp5PNx2VpfS9zM3NdTtLVVRUpJ9++snj5q6rrrpKV111le6++25lZ2fr9ttv15IlS1x/XNhs
Ntel89JHPs2dO1dffvnlWW/WKkv37t3VunVrvfzyyxo4cKDrj4x//etf6tSpk9uNNJJUUFDgNgdf
HnLepEkTZWdnezx+ypdjbv/+/SoqKnL7XMvNzZXNZnMdH9KpJ2BcddVVeu+999SwYUPt37/fYzlE
VfB1X3uDB8mjLKz5hDH16tXT008/rXHjxpX5LTalevXqpeLi4jKfQ+h0Ol2X0/39/WVZlttf7UVF
RVq8ePG5H3w5Tpw4oYceekgFBQW6++67XeVdu3ZVcXGx3nzzTbf6aWlp8vPz8zgTWFExMTFq1qyZ
FixYUOZl1kOHDkk6dSbtzEelhIaGqlGjRioqKnKV1atXz6tH+YSGhqpdu3Zavny59u7dW269devW
qWvXrmW+1rp1axUXF2vBggWKiIhQSEiI67WEhAQVFhZq8eLF8vf391hL2bVrV3311Vf6+uuvXWWF
hYVatmyZmjVr5nbZsLxffl27dtWmTZtcj5qSTt2Zv3LlSo+6ERERCgsL0+uvvy7LslxBuW3btsrN
zdWaNWuUkJBw1l+0jRs3VsuWLZWenu62r9auXetxibFXr146efKkXn75ZY92iouLf3MfjRs3TidP
ntTDDz/seqzU6c58FNnZdOrUSf7+/h5PpViyZImOHTvmeoTWkSNHPNq96qqrZLPZdPLkSUnSL7/8
4tF+6Zrb049DX4wePVr5+fn6v//7P1dZWWf4MjIylJeX51ZWui7yzEe4laVr1646efKkx+fLwoUL
5e/v79XPdFFRkZYsWeLx/+Hh4R5/uPTr109r167VG2+8ofDwcI/HffnKmxDo7b72hS/vMX4/OPOJ
KnXm5Zz+/fv/5jbt2rXT4MGD9eqrr2rbtm3q1KmTAgIC9MMPP2j16tV64okn1KNHDyUkJOiiiy7S
ww8/rGHDhkmS3n333Sr7S/vAgQOur/I7evSo/vvf/2rVqlXKz8/XiBEj3G4kSEpKUocOHfTXv/5V
e/bscT1q6eOPP9bw4cMrtM6yLDabTVOnTtWYMWPUt29fDRgwQJdccon279+vzz//XPXr19fLL7/s
uvR94403KjIyUkFBQVq/fr2++eYbt8c+RUdH6/3339f06dMVGxurevXqlXu24/HHH1dKSopuvvlm
DR48WJdeeqn27NmjtWvX6p133tGPP/6onTt3avLkyWVuX3o2c/PmzRowYIDba82bN1dISIg2b96s
yMhIjyUaY8aM0fvvv6+RI0e6HrW0YsUK7d+/3+OPlvIuKY4ePVrvvfee7rzzTqWmpqp27dpaunSp
LrvsMn333Xdljnf16tW6+uqrXesqY2JiVKdOHe3atcurh5w/+OCDuvvuu13PSHQ4HFq8eLFatmzp
Fr4SExN166236uWXX9a3336rxMREBQQEKDc3V6tXr9bTTz/tegZrWdq3b68nnnhCf/nLX9SjRw8l
Jyfr8ssvV1FRkXJzc5WRkaHatWt7dVY0PDxco0aN0rx58zR69Gh169ZN33//vd5++221atXKdYPW
+vXrNW3aNN14442KiIhQcXGx0tPTVatWLdf67r/97W/avHmzunTpoiZNmigvL0+LFy9WkyZNPJ7j
6q3rrrtOV1xxhV5//XUNHTpUfn5+rme2Pv7442rVqpW2b9+ujIwMj7W/ERERCgoK0ltvvaXatWur
Xr16SkhI8FgzKZ26ctOuXTs999xz2rVrl+tRS2vXrtXIkSPL3OZMjRo10iuvvKLdu3crIiJCGRkZ
+u9//6tp06Z5BObk5GQ9//zz+uijj5SamlruJXNvlfdzcHq5t/vaF768x/j9IHyiSnkTBMv6DuXJ
kycrJiZGS5Ys0V//+lf5+/uradOm6t+/v+ssWMOGDTVv3jxNnz5dL7zwgoKDg9WvXz9dc801Gjly
pNdj8Tasln5Pts1mU1BQkBo3bqzu3bvr1ltvdT1L8/Q2X3nlFc2ZM0eZmZlKT09X06ZN9cgjj2j4
8OFej6us184sa9++vd5++2299NJLWrRokY4eParw8HDFx8dr8ODBkk6t5UtJSdH69ev1wQcfqKSk
RBEREXr66adddSTptttu0/bt25Wenq6FCxeqSZMmrvB5Zr92u11Lly7VCy+8oLffflsnTpxQkyZN
XHeurlu3TsHBweXeAX7ZZZepUaNGysvLKzN4JCQk6OOPPy5zHWWjRo309ttv69lnn9Ubb7yhoqIi
2e12zZs3T507dz7r+1Xqkksu0T/+8Q9NnTpVr776qkJCQnTbbbcpJCREkyZN8qjftm1b/etf/3Ib
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-resample-method">The resample method<a class="anchor-link" href="#The-resample-method">&#182;</a></h2><p>A convenient way to bin timeseries data</p>
<p><strong>Warning:</strong> resample only works with a Timestamp-indexed dataframe. You can always set your index to your datetime column of interest <code>df.set_index('datetime_column)</code> to make this work</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[53]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># let&#39;s look at moves of a given actor, by year</span>
<span class="n">actor_df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">actor</span><span class="o">==</span><span class="s1">&#39;Samuel L. Jackson&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s1">&#39;male&#39;</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">actor_df</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[53]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5734</th>
      <td>School Daze</td>
      <td>Samuel L. Jackson</td>
      <td>9999999999999</td>
      <td>Col.</td>
      <td>1948-12-21</td>
      <td>1988-02-12</td>
      <td>6000000.0</td>
      <td>14545844.0</td>
      <td>14545844.0</td>
    </tr>
    <tr>
      <th>1933</th>
      <td>Do the Right Thing</td>
      <td>Samuel L. Jackson</td>
      <td>9999999999999</td>
      <td>Uni.</td>
      <td>1948-12-21</td>
      <td>1989-06-30</td>
      <td>6000000.0</td>
      <td>24289231.0</td>
      <td>24289231.0</td>
    </tr>
    <tr>
      <th>5785</th>
      <td>Sea of Love</td>
      <td>Samuel L. Jackson</td>
      <td>9999999999999</td>
      <td>Uni.</td>
      <td>1948-12-21</td>
      <td>1989-09-15</td>
      <td>19000000.0</td>
      <td>53350495.0</td>
      <td>53350495.0</td>
    </tr>
    <tr>
      <th>4491</th>
      <td>Mo' Better Blues</td>
      <td>Samuel L. Jackson</td>
      <td>9999999999999</td>
      <td>Uni.</td>
      <td>1948-12-21</td>
      <td>1990-08-03</td>
      <td>10000000.0</td>
      <td>16153000.0</td>
      <td>16153000.0</td>
    </tr>
    <tr>
      <th>2758</th>
      <td>Goodfellas</td>
      <td>Samuel L. Jackson</td>
      <td>9999999999999</td>
      <td>WB</td>
      <td>1948-12-21</td>
      <td>1990-09-19</td>
      <td>25000000.0</td>
      <td>46261759.0</td>
      <td>46261759.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[54]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># visualize what the data looks like now: it&#39;s irregular by year</span>
<span class="n">actor_df</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">,</span><span class="s1">&#39;production_budget&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[54]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x7fd32092e828&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAp8AAAHiCAYAAACuvKeKAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3XmcHHWdP/5X9Tn3fV+5IAeQEMKhRsLhusKKCD++gMgC
u7CiKISvgIqruCCLBORURHZBWVyIuLrIigqiXxYIAgIhhJiQScg5R+a+z76qfn9Ufaqre3p6unu6
uqp7Xs/HgweT7p7umppK+t3vz/v9/kiKoiggIiIiIsoAh9UHQEREREQLB4NPIiIiIsoYBp9ERERE
lDEMPomIiIgoYxh8EhEREVHGMPgkIiIiooxh8ElEREREGcPgk4iIiIgyhsEnEREREWUMg08iIiIi
ypisCj63bt2Ka665Bhs2bMDKlSvx0ksvJf0cr732Gj73uc9h3bp1+NjHPobrr78enZ2dJhwtERER
EUXLquBzcnISq1atwq233gpJkpL+/o6ODlx77bX42Mc+ht/85jd4/PHHMTQ0hI0bN5pwtEREREQU
zWX1ASTjtNNOw2mnnQYAUBRlxv1+vx8PPPAAfv/732NsbAzLly/HTTfdhFNOOQUAsGvXLsiyjK9+
9av691x11VW49tprEQqF4HQ6M/ODEBERES1QWZX5nMvtt9+O999/Hw8++CCee+45nH322bj66qvR
1tYGADj22GPhcDjwzDPPQJZljI2N4Te/+Q3Wr1/PwJOIiIgoAyQlVgoxC6xcuRIPP/ww/uZv/gYA
0NXVhU9+8pN45ZVXUF1drT/uyiuvxJo1a3DDDTcAAN555x189atfxfDwMEKhEE444QQ89thjKCoq
suTnICIiIlpIsmrZPZ69e/ciFArhrLPOiliSDwQCKC8vBwD09/fjlltuwQUXXIBzzjkH4+Pj+MEP
foCNGzfiP/7jP6w6dCIiIqIFI2eCz4mJCbhcLjz77LNwOCKrCQoKCgAAmzdvRnFxMW666Sb9vnvv
vRenn346duzYgTVr1mT0mImIiIgWmpwJPo855hiEQiH09/fjxBNPjPmY6elpuFyRP7Lompdl2fRj
JCIiIlrokmo4+vd//3dceOGFWLduHdavX49rr70WBw8enPP73nrrLVxwwQVYvXo1zjrrLDz77LMp
Hezk5CRaW1uxe/duAEB7eztaW1vR1dWFxYsX4zOf+Qxuvvlm/OlPf0JHRwd27NiBRx99FK+++ioA
6BnOhx9+GIcPH8auXbvwz//8z2hqasIxxxyT0jERERERUeKSaji6+uqrcc4552D16tUIBoO4//77
8eGHH+L5559HXl5ezO/p6OjAueeei89//vO48MIL8eabb+LOO+/Eo48+io9//ONJHezbb7+NK664
YsaMz/PPPx+bNm1CKBTCI488gv/5n/9BT08PysvLsXbtWmzcuBFHH300AOD555/HT37yExw6dAj5
+flYu3Ytvva1r2HJkiVJHQsRERERJW9e3e6Dg4NYv349nnrqKZx00kkxH3PPPfdgy5Yt+O1vf6vf
duONN2JsbAyPPfZYqi9NRERERFloXnM+x8bGIEkSysrKZn3M+++/j/Xr10fcduqpp2L79u3zeWki
IiIiykIpB5+KouDOO+/EiSeeiKOOOmrWx/X19aGysjLitsrKSoyPj8Pv96f68kRERESUhVLudr/t
ttuwb98+PP300+k8nlkpipLSfu5EREREZB8pBZ+33347tmzZgs2bN6OmpibuY6urqzEwMBBx28DA
AIqKiuDxeBJ+zcHBCTgcDD7Tyel0oKQkH6OjUwiFOGrKDDzH5uM5Nh/Psfl4js3Hc5wZ5eWFcz4m
6eDz9ttvx0svvYSnnnoKDQ0Ncz5+7dq12LJlS8Rtr7/+OtauXZvU68qyAlnOyp1AbS8UkhEM8i+i
mXiOzcdzbD6eY/PxHJuP59h6SdV83nbbbfjtb3+L++67D/n5+ejv70d/fz98Pp/+mPvvvx8333yz
/udLLrkE7e3tuOeee3DgwAFs3rwZL774Iq688sr0/RRERERElBWSynz+4he/gCRJuPzyyyNu37Rp
E84//3wAaoNRV1eXfl9TUxMeffRRbNq0CU8++STq6upwxx13zOiAJyIiIqLcN685n5nU1zdm9SHk
HJfLgfLyQgwNTXAJwiQ8x+bjOTYfz7H5eI7Nx3OcGdXVxXM+Zl5zPomIiIiIksHgk4iIiIgyhsEn
EREREWUMg08iIiIiyhgGn0RERESUMQw+iYiIiChjGHwSERERUcYw+CQiIiKijGHwuQDceed38a1v
fd3017noos/iV7/6hemvI2zc+CU89ND9aX/e7u4ubNhwMvbt+zDtz01ERLTQMfikpL3wwu9w9tln
zrj9Jz/5T3z2s/+fBUeUfpIkpf05Mx2cExER2VFSe7uTdYLBIFwue/y6FEWJGZyVlpZZcDTmyJJd
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
7sTChQuRn5+PMWPG4LbbbsOuXbuE17/++ms899xzAIAJEyYgMzMT06ZNE16vrq7G008/jfHjx2Pk
yJG46667UFhYaNU4CYIgxMhcPQCCIIiBwjAMampq8Nprr+HBBx/EoEGDEBsbiwULFqCxsRFPPfUU
YmJi8N///hdLlizB119/jbS0NIvHKisrw7x585Ceno7XX38dDMPgvffew4IFC/Djjz9CLpcDAKqq
qnDnnXciISEBHR0d2LBhA+644w5s3boVISEhAIAlS5YgOjoay5cvR1BQEC5evIjq6mrhs44cOYJ7
7rkHV155Jd566y10dHTgrbfewkMPPYQNGzb069yLiorw+OOP44orrsCzzz6L8vJyPPHEE9BoNCb7
lZeX44orrsDChQshlUrx22+/YcmSJVi7di3GjRuHqVOn4sEHH8T777+Pjz/+GEFBQVAoFACAlpYW
zJs3D4GBgXjxxRcRFBSEdevWYcGCBfjpp58QERFh9XdGEAQBliAIwkN55pln2MzMTPbYsWPCti+/
/JLNyclhS0pKTPa97bbb2CeeeEL4+6677mKXLFki/L106VL2mmuuYdVqtbCtvr6ezcvLY9evX2/x
83U6HdvZ2cnm5eWxX3zxBcuyLNvQ0MBmZGSw27dv73Hc8+fPZ++8806TbWfPnmUzMzPZnTt39n3i
LMs+8cQT7NVXX83q9Xph25dffslmZGSw7777rsX36PV6VqvVsgsXLmSfeuopYftXX33FZmZmso2N
jSb7v/322+y4cePYhoYGYZtarWavvPJK9o033ujXOAmCIMyhsDtBEB5NWFgYcnNzhb/37t2L9PR0
pKSkQKfTQafTQavVIj8/32JYmmfPnj246qqrIJFIhPeFhIQgOzvb5H1Hjx7Fn/70J1x++eXIzs7G
qFGj0NnZifPnzwMAwsPDER8fj5UrV2Lz5s0mHk8A6OrqwpEjR3DttdcKn6PT6ZCSkoJBgwb1OkYx
x44dw5VXXgmGYYRt1157bbf9qqursWzZMkyZMgXZ2dnIycnBnj17uqUKWGLv3r24/PLLERISIoyT
YRiMGzeu3+MkCIIwh8LuBEF4NFFRUSZ/NzY24uTJk8jJyem2r0zW8yWvqakJa9euxZo1a0y2Mwwj
hKErKytx3333ITc3F6+88gpiYmIgl8tx//33mxQ6ffLJJ/jf//1fvPzyy+jo6EBOTg6effZZjB07
Fs3NzdDpdFi+fDlee+21bp9VVVXVr/Oura1FZGSkybagoCAolUrhb5Zl8cADD8M177oAAARkSURB
VKC9vR1PPPEEkpOT4e/vj7fffhuVlZV9fkZjYyMKCgq6zSXDMEhOTu7XOAmCIMwh45MgCK8iNDQU
mZmZeO2116yq3g4NDcXUqVMxf/78bu8LDAwEAPz222/o7OzEqlWrEBQUBADQ6XRobm422T8lJQVv
vfUWdDodjhw5gpUrV+LBBx/Eb7/9hpCQEDAMgwceeABXX311t3GEh4f3a7zR0dGor6832dbW1mai
1Xnx4kUUFRXhvffew5VXXils7+rq6tdnhIaGYvLkyXjiiSe6zQlvkBMEQVgLGZ8EQXgV+fn5+O23
3xAdHY3o6Oh+v2/ChAk4c+YMsrKyTELZYlQqFRiGMfGgbtmyBVqt1uL+UqkUY8eOxf3334+HHnoI
NTU1SElJwahRo1BSUoLHH3/cupMTMWLECGzfvh3PPvusMN4ff/zRZB/eyBSPt6KiAocPH0Zqaqqw
jS+mMheZnzBhAr799lsMGTIEfn5+Ax4rQRCEGOlLL730kqsHQRAEMRC2bduGmpoa3HnnncK2tLQ0
/Prrr9iwYQOUSiXa29tRVFSE77//Hnv37sWECRMAcBJDCoUCs2bNAgBkZmbiww8/xN69e6FUKtHU
1ISCggKsX78eHR0dSEtLg7+/PzZs2IDz588jNDQU27dvx/vvvw+JRIKMjAxMmTIFp06dwtKlS6FW
q9HW1obi4mL861//gkKhwCOPPAKGYTB06FC8/fbbOH36NGQyGerq6nDw4EGsWbMGoaGhSEhI6PPc
U1JSsHr1ahw/fhwhISHYvXs3PvzwQ2g0GowePRqXXXYZQkJC8PXXX+PIkSOIi4tDYWEhnn/+eQQE
BEAulwvzptPp8Pnnn0MulyMwMBDNzc2IjIxEVlYWvvjiC2zZsgV+fn5obW3FiRMn8NVXX+Hs2bMY
NWqUA75VgiC8HfJ8EgTh0Zh7KRUKBdauXYtVq1bh/fffR21tLcLDw5GdnY158+b1+N7k5GRs3LgR
b731lpCrGR0djXHjxiEjIwMAkJ6ejhUrVmDVqlX/v507RlEYiMI4/gU7QRAsnNZCiJUEtPACniRN
QME6pbUhGu3ExsJChJwgfQ7gGQQr7YVkq10IrOCyMlj8f+2DzCNpPmbeREEQyHVdJUlS2cH83nHd
bre6Xq9qNBoaDAZaLBY/63mep8PhoPV6rTAM9Xg81G63NRqNXp6l7PV6Wq1WiqJI0+lU3W5XcRzL
9/3Ku9hsNprP55rNZjLGKAgC5Xmu8/lcedZkMtHpdNJut5MxRlmWqdls6ng8arlcKooi3e93tVot
9ft9jcfjF78QAFQ55V+GogAAAIB/4FdLAAAAsIZjdwD4MGVZqiiKp/VarWaxGwB4L8InAHyYMAyV
pumvNcdxtN/vNRwOLXcFAO/BzCcAfJjL5aLb7fa03ul0VK/XLXYEAO9D+AQAAIA1XDgCAACANYRP
AAAAWEP4BAAAgDWETwAAAFhD+AQAAIA1hE8AAABYQ/gEAACANV9lPHVtqYPkcQAAAABJRU5ErkJg
gg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[55]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># take the mean of all the numerical columns</span>
<span class="n">actor_df</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">resample</span><span class="p">(</span><span class="s1">&#39;AS&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[55]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rank</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>1.000000e+13</td>
      <td>6000000.0</td>
      <td>14545844.0</td>
      <td>14545844.0</td>
    </tr>
    <tr>
      <th>1989-01-01</th>
      <td>1.000000e+13</td>
      <td>12500000.0</td>
      <td>38819863.0</td>
      <td>38819863.0</td>
    </tr>
    <tr>
      <th>1990-01-01</th>
      <td>1.000000e+13</td>
      <td>17500000.0</td>
      <td>31207379.5</td>
      <td>31207379.5</td>
    </tr>
    <tr>
      <th>1991-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1992-01-01</th>
      <td>1.000000e+13</td>
      <td>45000000.0</td>
      <td>83287363.0</td>
      <td>178100000.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Note-that-by-default,-missing-bins-get-replaced-with-a-NaN-row.-This-can-be-useful-if-you-want-to-set-a-default-value-for-the-missing-bins">Note that by default, missing bins get replaced with a NaN row. This can be useful if you want to set a default value for the missing bins<a class="anchor-link" href="#Note-that-by-default,-missing-bins-get-replaced-with-a-NaN-row.-This-can-be-useful-if-you-want-to-set-a-default-value-for-the-missing-bins">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[56]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># same as above, but fill all NaNs with 0</span>
<span class="n">actor_df</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">resample</span><span class="p">(</span><span class="s1">&#39;AS&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[56]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rank</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>1.000000e+13</td>
      <td>6000000.0</td>
      <td>14545844.0</td>
      <td>14545844.0</td>
    </tr>
    <tr>
      <th>1989-01-01</th>
      <td>1.000000e+13</td>
      <td>12500000.0</td>
      <td>38819863.0</td>
      <td>38819863.0</td>
    </tr>
    <tr>
      <th>1990-01-01</th>
      <td>1.000000e+13</td>
      <td>17500000.0</td>
      <td>31207379.5</td>
      <td>31207379.5</td>
    </tr>
    <tr>
      <th>1991-01-01</th>
      <td>0.000000e+00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1992-01-01</th>
      <td>1.000000e+13</td>
      <td>45000000.0</td>
      <td>83287363.0</td>
      <td>178100000.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[57]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># if we want 5-year bins instead, we can plug in a 5 to the resample &quot;rule&quot;: &#39;5AS&#39;</span>
<span class="n">actor_df</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">resample</span><span class="p">(</span><span class="s1">&#39;5AS&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[57]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rank</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>1.000000e+13</td>
      <td>1.850000e+07</td>
      <td>3.964795e+07</td>
      <td>5.545005e+07</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>2.727273e+12</td>
      <td>2.393636e+07</td>
      <td>7.105578e+07</td>
      <td>1.462092e+08</td>
    </tr>
    <tr>
      <th>1998-01-01</th>
      <td>1.000000e+12</td>
      <td>5.027560e+07</td>
      <td>4.919147e+07</td>
      <td>8.413794e+07</td>
    </tr>
    <tr>
      <th>2003-01-01</th>
      <td>3.290909e+01</td>
      <td>4.277273e+07</td>
      <td>5.912338e+07</td>
      <td>1.154025e+08</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>2.727273e+12</td>
      <td>9.595455e+07</td>
      <td>1.294431e+08</td>
      <td>2.701183e+08</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>2.200000e+01</td>
      <td>1.217500e+08</td>
      <td>1.138697e+08</td>
      <td>3.472769e+08</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="resample-resolutions-available-(via-SO-answer):">resample resolutions available <a href="http://stackoverflow.com/a/17001474">(via SO answer)</a>:<a class="anchor-link" href="#resample-resolutions-available-(via-SO-answer):">&#182;</a></h2>
<pre><code>B       business day frequency
C       custom business day frequency (experimental)
D       calendar day frequency
W       weekly frequency
M       month end frequency
BM      business month end frequency
CBM     custom business month end frequency
MS      month start frequency
BMS     business month start frequency
CBMS    custom business month start frequency
Q       quarter end frequency
BQ      business quarter endfrequency
QS      quarter start frequency
BQS     business quarter start frequency
A       year end frequency
BA      business year end frequency
AS      year start frequency
BAS     business year start frequency
BH      business hour frequency
H       hourly frequency
T       minutely frequency
S       secondly frequency
L       milliseonds
U       microseconds
N       nanoseconds</code></pre>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[58]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># let&#39;s say we want the mean, and also the count</span>
<span class="c1"># we can pass a list of methods using &#39;apply&#39;</span>
<span class="n">yr_bins</span> <span class="o">=</span> <span class="n">actor_df</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">resample</span><span class="p">(</span><span class="s1">&#39;5AS&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">([</span><span class="s1">&#39;mean&#39;</span><span class="p">,</span><span class="s1">&#39;count&#39;</span><span class="p">,</span><span class="s1">&#39;sem&#39;</span><span class="p">])</span>
<span class="n">yr_bins</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[58]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">rank</th>
      <th colspan="3" halign="left">production_budget</th>
      <th colspan="3" halign="left">domestic_gross</th>
      <th colspan="3" halign="left">worldwide_gross</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>count</th>
      <th>sem</th>
      <th>mean</th>
      <th>count</th>
      <th>sem</th>
      <th>mean</th>
      <th>count</th>
      <th>sem</th>
      <th>mean</th>
      <th>count</th>
      <th>sem</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>1.000000e+13</td>
      <td>6</td>
      <td>0.000000e+00</td>
      <td>1.850000e+07</td>
      <td>6</td>
      <td>6.135960e+06</td>
      <td>3.964795e+07</td>
      <td>6</td>
      <td>1.088412e+07</td>
      <td>5.545005e+07</td>
      <td>6</td>
      <td>2.537732e+07</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>2.727273e+12</td>
      <td>11</td>
      <td>1.408358e+12</td>
      <td>2.393636e+07</td>
      <td>11</td>
      <td>7.175555e+06</td>
      <td>7.105578e+07</td>
      <td>11</td>
      <td>3.427397e+07</td>
      <td>1.462092e+08</td>
      <td>11</td>
      <td>9.151223e+07</td>
    </tr>
    <tr>
      <th>1998-01-01</th>
      <td>1.000000e+12</td>
      <td>10</td>
      <td>1.000000e+12</td>
      <td>5.027560e+07</td>
      <td>10</td>
      <td>5.932781e+06</td>
      <td>4.919147e+07</td>
      <td>10</td>
      <td>9.543079e+06</td>
      <td>8.413794e+07</td>
      <td>10</td>
      <td>2.357590e+07</td>
    </tr>
    <tr>
      <th>2003-01-01</th>
      <td>3.290909e+01</td>
      <td>11</td>
      <td>4.909091e+00</td>
      <td>4.277273e+07</td>
      <td>11</td>
      <td>7.540004e+06</td>
      <td>5.912338e+07</td>
      <td>11</td>
      <td>2.268627e+07</td>
      <td>1.154025e+08</td>
      <td>11</td>
      <td>5.307465e+07</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>2.727273e+12</td>
      <td>11</td>
      <td>1.408358e+12</td>
      <td>9.595455e+07</td>
      <td>11</td>
      <td>1.828343e+07</td>
      <td>1.294431e+08</td>
      <td>11</td>
      <td>3.411070e+07</td>
      <td>2.701183e+08</td>
      <td>11</td>
      <td>7.069114e+07</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[59]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># or you can get very fancy and pass a dict of dicts</span>
<span class="c1"># the first key references the DataFrames&#39; original column name while</span>
<span class="c1"># the second key defines the name of a new column</span>
<span class="n">yr_bins</span> <span class="o">=</span> <span class="n">actor_df</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="s1">&#39;release_date&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">resample</span><span class="p">(</span><span class="s1">&#39;5AS&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">({</span>
        <span class="s1">&#39;production_budget&#39;</span><span class="p">:{</span><span class="s1">&#39;avg&#39;</span><span class="p">:</span><span class="s1">&#39;mean&#39;</span><span class="p">,</span> <span class="s1">&#39;ct&#39;</span><span class="p">:</span><span class="s1">&#39;count&#39;</span><span class="p">,</span> <span class="s1">&#39;stdEm&#39;</span><span class="p">:</span><span class="s1">&#39;sem&#39;</span><span class="p">},</span>
        <span class="s1">&#39;domestic_gross&#39;</span><span class="p">:{</span><span class="s1">&#39;low&#39;</span><span class="p">:</span><span class="s1">&#39;min&#39;</span><span class="p">,</span> <span class="s1">&#39;high&#39;</span><span class="p">:</span><span class="s1">&#39;max&#39;</span><span class="p">},</span>
        <span class="s1">&#39;worldwide_gross&#39;</span><span class="p">:{</span><span class="s1">&#39;total&#39;</span><span class="p">:</span><span class="s1">&#39;sum&#39;</span><span class="p">}})</span>
<span class="n">yr_bins</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[59]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">domestic_gross</th>
      <th colspan="3" halign="left">production_budget</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th></th>
      <th>high</th>
      <th>low</th>
      <th>ct</th>
      <th>stdEm</th>
      <th>avg</th>
      <th>total</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>83287363.0</td>
      <td>14545844.0</td>
      <td>6</td>
      <td>6.135960e+06</td>
      <td>1.850000e+07</td>
      <td>3.327003e+08</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>395708305.0</td>
      <td>749741.0</td>
      <td>11</td>
      <td>7.175555e+06</td>
      <td>2.393636e+07</td>
      <td>1.608301e+09</td>
    </tr>
    <tr>
      <th>1998-01-01</th>
      <td>94999143.0</td>
      <td>687081.0</td>
      <td>10</td>
      <td>5.932781e+06</td>
      <td>5.027560e+07</td>
      <td>8.413794e+08</td>
    </tr>
    <tr>
      <th>2003-01-01</th>
      <td>261441092.0</td>
      <td>3172382.0</td>
      <td>11</td>
      <td>7.540004e+06</td>
      <td>4.277273e+07</td>
      <td>1.269428e+09</td>
    </tr>
    <tr>
      <th>2008-01-01</th>
      <td>318604126.0</td>
      <td>1110509.0</td>
      <td>11</td>
      <td>1.828343e+07</td>
      <td>9.595455e+07</td>
      <td>2.971301e+09</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>259746958.0</td>
      <td>54096599.0</td>
      <td>4</td>
      <td>2.250324e+07</td>
      <td>1.217500e+08</td>
      <td>1.389107e+09</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Special-note:-try-not-to-use-method-names-as-column-names.-It-will-make-indexing-more-annoying.">Special note: try not to use method names as column names. It will make indexing more annoying.<a class="anchor-link" href="#Special-note:-try-not-to-use-method-names-as-column-names.-It-will-make-indexing-more-annoying.">&#182;</a></h3><h4 id="For-example,-a-column-named-'mean'-will-cause-a-collision-when-you-call-df.mean-with-the-function-call-having-precedence">For example, a column named 'mean' will cause a collision when you call df.mean with the function call having precedence<a class="anchor-link" href="#For-example,-a-column-named-'mean'-will-cause-a-collision-when-you-call-df.mean-with-the-function-call-having-precedence">&#182;</a></h4><p>You will only be able to acced the column like: `df['mean']</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Multiindexing">Multiindexing<a class="anchor-link" href="#Multiindexing">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[60]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">yr_bins</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[60]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">domestic_gross</th>
      <th colspan="3" halign="left">production_budget</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th></th>
      <th>high</th>
      <th>low</th>
      <th>ct</th>
      <th>stdEm</th>
      <th>avg</th>
      <th>total</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>83287363.0</td>
      <td>14545844.0</td>
      <td>6</td>
      <td>6.135960e+06</td>
      <td>1.850000e+07</td>
      <td>3.327003e+08</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>395708305.0</td>
      <td>749741.0</td>
      <td>11</td>
      <td>7.175555e+06</td>
      <td>2.393636e+07</td>
      <td>1.608301e+09</td>
    </tr>
    <tr>
      <th>1998-01-01</th>
      <td>94999143.0</td>
      <td>687081.0</td>
      <td>10</td>
      <td>5.932781e+06</td>
      <td>5.027560e+07</td>
      <td>8.413794e+08</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[61]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">yr_bins</span><span class="o">.</span><span class="n">production_budget</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[61]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ct</th>
      <th>stdEm</th>
      <th>avg</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>6</td>
      <td>6.135960e+06</td>
      <td>1.850000e+07</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>11</td>
      <td>7.175555e+06</td>
      <td>2.393636e+07</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[62]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># chaining the dot column name syntax is fine</span>
<span class="n">yr_bins</span><span class="o">.</span><span class="n">production_budget</span><span class="o">.</span><span class="n">avg</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[62]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>release_date
1988-01-01    1.850000e+07
1993-01-01    2.393636e+07
1998-01-01    5.027560e+07
2003-01-01    4.277273e+07
2008-01-01    9.595455e+07
2013-01-01    1.217500e+08
Freq: 5AS-JAN, Name: avg, dtype: float64</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[63]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># you can also index both levels of the column index by name, as strings</span>
<span class="n">yr_bins</span><span class="p">[</span><span class="s1">&#39;production_budget&#39;</span><span class="p">,</span><span class="s1">&#39;avg&#39;</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[63]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>release_date
1988-01-01    1.850000e+07
1993-01-01    2.393636e+07
1998-01-01    5.027560e+07
2003-01-01    4.277273e+07
2008-01-01    9.595455e+07
2013-01-01    1.217500e+08
Freq: 5AS-JAN, Name: (production_budget, avg), dtype: float64</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Flattening-a-multi-level-column-index">Flattening a multi-level column index<a class="anchor-link" href="#Flattening-a-multi-level-column-index">&#182;</a></h2><h3 id="Use-a-list-comprehension-to-rewrite-the-column-names">Use a list comprehension to rewrite the column names<a class="anchor-link" href="#Use-a-list-comprehension-to-rewrite-the-column-names">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[64]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">yr_bins</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[64]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">domestic_gross</th>
      <th colspan="3" halign="left">production_budget</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th></th>
      <th>high</th>
      <th>low</th>
      <th>ct</th>
      <th>stdEm</th>
      <th>avg</th>
      <th>total</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>83287363.0</td>
      <td>14545844.0</td>
      <td>6</td>
      <td>6.135960e+06</td>
      <td>1.850000e+07</td>
      <td>3.327003e+08</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>395708305.0</td>
      <td>749741.0</td>
      <td>11</td>
      <td>7.175555e+06</td>
      <td>2.393636e+07</td>
      <td>1.608301e+09</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[65]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">yr_bins</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">values</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[(&#39;domestic_gross&#39;, &#39;high&#39;) (&#39;domestic_gross&#39;, &#39;low&#39;)
 (&#39;production_budget&#39;, &#39;ct&#39;) (&#39;production_budget&#39;, &#39;stdEm&#39;)
 (&#39;production_budget&#39;, &#39;avg&#39;) (&#39;worldwide_gross&#39;, &#39;total&#39;)]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[66]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">yr_bins_flat</span> <span class="o">=</span> <span class="n">yr_bins</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="c1"># use an underscore as delimiter is an optional convention</span>
<span class="n">yr_bins_flat</span><span class="o">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;_&#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">col</span><span class="p">)</span> <span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="n">yr_bins</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">values</span><span class="p">]</span>
<span class="n">yr_bins_flat</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[66]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>domestic_gross_high</th>
      <th>domestic_gross_low</th>
      <th>production_budget_ct</th>
      <th>production_budget_stdEm</th>
      <th>production_budget_avg</th>
      <th>worldwide_gross_total</th>
    </tr>
    <tr>
      <th>release_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1988-01-01</th>
      <td>83287363.0</td>
      <td>14545844.0</td>
      <td>6</td>
      <td>6.135960e+06</td>
      <td>1.850000e+07</td>
      <td>3.327003e+08</td>
    </tr>
    <tr>
      <th>1993-01-01</th>
      <td>395708305.0</td>
      <td>749741.0</td>
      <td>11</td>
      <td>7.175555e+06</td>
      <td>2.393636e+07</td>
      <td>1.608301e+09</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[67]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># you can also access specific index levels using the get_level_values function</span>
<span class="n">yr_bins</span><span class="o">.</span><span class="n">columns</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[67]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>MultiIndex(levels=[[&#39;domestic_gross&#39;, &#39;production_budget&#39;, &#39;worldwide_gross&#39;], [&#39;avg&#39;, &#39;ct&#39;, &#39;high&#39;, &#39;low&#39;, &#39;stdEm&#39;, &#39;total&#39;]],
           labels=[[0, 0, 1, 1, 1, 2], [2, 3, 1, 4, 0, 5]])</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[68]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">yr_bins</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">get_level_values</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[68]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>Index([&#39;domestic_gross&#39;, &#39;domestic_gross&#39;, &#39;production_budget&#39;,
       &#39;production_budget&#39;, &#39;production_budget&#39;, &#39;worldwide_gross&#39;],
      dtype=&#39;object&#39;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[69]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">yr_bins</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">get_level_values</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[69]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>Index([&#39;high&#39;, &#39;low&#39;, &#39;ct&#39;, &#39;stdEm&#39;, &#39;avg&#39;, &#39;total&#39;], dtype=&#39;object&#39;)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="pd.cut():-bins-numeric-values-and-converts-to-categorical-values"><code>pd.cut()</code>: bins numeric values and converts to categorical values<a class="anchor-link" href="#pd.cut():-bins-numeric-values-and-converts-to-categorical-values">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[70]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># make some fake data</span>
<span class="n">no_movies</span> <span class="o">=</span> <span class="mi">10</span>
<span class="n">ratings_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="o">.</span><span class="n">from_dict</span><span class="p">({</span>
        <span class="s1">&#39;rating_no&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">rand</span><span class="p">(</span><span class="n">no_movies</span><span class="p">),</span>
        <span class="s1">&#39;movie&#39;</span><span class="p">:</span> <span class="n">df</span><span class="o">.</span><span class="n">title</span><span class="o">.</span><span class="n">sample</span><span class="p">(</span><span class="n">no_movies</span><span class="p">)</span>
    <span class="p">})</span>

<span class="c1"># fake gross based on fake rating</span>
<span class="n">ratings_df</span><span class="p">[</span><span class="s1">&#39;gross&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">ratings_df</span><span class="o">.</span><span class="n">rating_no</span><span class="o">*</span><span class="mi">100000000</span><span class="p">,</span> <span class="n">decimals</span><span class="o">=</span><span class="mi">2</span><span class="p">)</span>

<span class="c1"># save this unmodified version for later</span>
<span class="n">ratings_df_orig</span> <span class="o">=</span> <span class="n">ratings_df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>

<span class="n">ratings_df</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[70]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie</th>
      <th>rating_no</th>
      <th>gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4277</th>
      <td>Manderlay</td>
      <td>0.738555</td>
      <td>73855520.21</td>
    </tr>
    <tr>
      <th>4102</th>
      <td>Love Actually</td>
      <td>0.010958</td>
      <td>1095817.02</td>
    </tr>
    <tr>
      <th>9084</th>
      <td>Whipped</td>
      <td>0.066883</td>
      <td>6688330.31</td>
    </tr>
    <tr>
      <th>8716</th>
      <td>Trouble with the Curve</td>
      <td>0.857547</td>
      <td>85754670.87</td>
    </tr>
    <tr>
      <th>6987</th>
      <td>The Devil Wears Prada</td>
      <td>0.992611</td>
      <td>99261063.44</td>
    </tr>
    <tr>
      <th>8330</th>
      <td>The Town</td>
      <td>0.521661</td>
      <td>52166097.94</td>
    </tr>
    <tr>
      <th>4927</th>
      <td>One True Thing</td>
      <td>0.802086</td>
      <td>80208581.33</td>
    </tr>
    <tr>
      <th>696</th>
      <td>Austin Powers: International Man of Mystery</td>
      <td>0.373662</td>
      <td>37366213.10</td>
    </tr>
    <tr>
      <th>4827</th>
      <td>Now You See Me</td>
      <td>0.187231</td>
      <td>18723109.19</td>
    </tr>
    <tr>
      <th>7743</th>
      <td>The Master</td>
      <td>0.802130</td>
      <td>80212985.66</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[71]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># cut numerical ratings into N bins</span>

<span class="c1"># here&#39;s what the labels default to when you don&#39;t define your own lables</span>
<span class="n">ratings_df</span><span class="p">[</span><span class="s1">&#39;rating_category_ugly&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">cut</span><span class="p">(</span><span class="n">ratings_df</span><span class="o">.</span><span class="n">rating_no</span><span class="p">,</span> <span class="n">bins</span><span class="o">=</span><span class="mi">4</span><span class="p">)</span>

<span class="c1"># you can substitute whatever labels you want</span>
<span class="n">ratings_df</span><span class="p">[</span><span class="s1">&#39;rating_category&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">cut</span><span class="p">(</span><span class="n">ratings_df</span><span class="o">.</span><span class="n">rating_no</span><span class="p">,</span> <span class="n">bins</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;bad&#39;</span><span class="p">,</span><span class="s1">&#39;mediocre&#39;</span><span class="p">,</span><span class="s1">&#39;good&#39;</span><span class="p">,</span><span class="s1">&#39;excellent&#39;</span><span class="p">])</span>

<span class="n">ratings_df</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[71]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>movie</th>
      <th>rating_no</th>
      <th>gross</th>
      <th>rating_category_ugly</th>
      <th>rating_category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4277</th>
      <td>Manderlay</td>
      <td>0.738555</td>
      <td>73855520.21</td>
      <td>(0.502, 0.747]</td>
      <td>good</td>
    </tr>
    <tr>
      <th>4102</th>
      <td>Love Actually</td>
      <td>0.010958</td>
      <td>1095817.02</td>
      <td>(0.00998, 0.256]</td>
      <td>bad</td>
    </tr>
    <tr>
      <th>9084</th>
      <td>Whipped</td>
      <td>0.066883</td>
      <td>6688330.31</td>
      <td>(0.00998, 0.256]</td>
      <td>bad</td>
    </tr>
    <tr>
      <th>8716</th>
      <td>Trouble with the Curve</td>
      <td>0.857547</td>
      <td>85754670.87</td>
      <td>(0.747, 0.993]</td>
      <td>excellent</td>
    </tr>
    <tr>
      <th>6987</th>
      <td>The Devil Wears Prada</td>
      <td>0.992611</td>
      <td>99261063.44</td>
      <td>(0.747, 0.993]</td>
      <td>excellent</td>
    </tr>
    <tr>
      <th>8330</th>
      <td>The Town</td>
      <td>0.521661</td>
      <td>52166097.94</td>
      <td>(0.502, 0.747]</td>
      <td>good</td>
    </tr>
    <tr>
      <th>4927</th>
      <td>One True Thing</td>
      <td>0.802086</td>
      <td>80208581.33</td>
      <td>(0.747, 0.993]</td>
      <td>excellent</td>
    </tr>
    <tr>
      <th>696</th>
      <td>Austin Powers: International Man of Mystery</td>
      <td>0.373662</td>
      <td>37366213.10</td>
      <td>(0.256, 0.502]</td>
      <td>mediocre</td>
    </tr>
    <tr>
      <th>4827</th>
      <td>Now You See Me</td>
      <td>0.187231</td>
      <td>18723109.19</td>
      <td>(0.00998, 0.256]</td>
      <td>bad</td>
    </tr>
    <tr>
      <th>7743</th>
      <td>The Master</td>
      <td>0.802130</td>
      <td>80212985.66</td>
      <td>(0.747, 0.993]</td>
      <td>excellent</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[72]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># `pd.cut` gives us an excellent way to groupby based on bins</span>
<span class="c1"># Eg. we can use the new categorical ratings to find the mean gross for each rating bin</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;mean gross for each rating bin&#39;</span><span class="p">)</span>
<span class="n">ratings_df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;rating_category&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>mean gross for each rating bin
</pre>
</div>
</div>

<div class="output_area"><div class="prompt output_prompt">Out[72]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating_no</th>
      <th>gross</th>
    </tr>
    <tr>
      <th>rating_category</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bad</th>
      <td>0.088358</td>
      <td>8.835752e+06</td>
    </tr>
    <tr>
      <th>mediocre</th>
      <td>0.373662</td>
      <td>3.736621e+07</td>
    </tr>
    <tr>
      <th>good</th>
      <td>0.630108</td>
      <td>6.301081e+07</td>
    </tr>
    <tr>
      <th>excellent</th>
      <td>0.863593</td>
      <td>8.635933e+07</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[73]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Even if we didn&#39;t care about assigning labels like &#39;bad&#39;, &#39;mediocre&#39; etc to the rating numbers</span>
<span class="c1"># pd.cut is still very useful if we want to groupby on binned numerical data</span>

<span class="c1"># We can do this as a one-liner, using the copy of the original ratings_df before we added the extra columns</span>
<span class="n">ratings_df_orig</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">cut</span><span class="p">(</span><span class="n">ratings_df_orig</span><span class="o">.</span><span class="n">rating_no</span><span class="p">,</span><span class="n">bins</span><span class="o">=</span><span class="mi">5</span><span class="p">),</span><span class="n">as_index</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[73]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rating_no</th>
      <th>gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.088358</td>
      <td>8.835752e+06</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.373662</td>
      <td>3.736621e+07</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.521661</td>
      <td>5.216610e+07</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.738555</td>
      <td>7.385552e+07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.863593</td>
      <td>8.635933e+07</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Random-Useful-Functions">Random Useful Functions<a class="anchor-link" href="#Random-Useful-Functions">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="isin">isin<a class="anchor-link" href="#isin">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[74]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># which female actors appear most often in the dataset?</span>
<span class="n">top_actresses</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">male</span><span class="o">==</span><span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;actor&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">size</span><span class="p">()</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
<span class="n">top_actresses</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[74]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>actor
Susan Sarandon      33
Julia Roberts       32
Julianne Moore      31
Cate Blanchett      30
Sigourney Weaver    29
dtype: int64</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[75]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># often we want to select all rows where a column contains any value in a list</span>
<span class="c1"># eg. select all rows where df.actor is in our list of actors</span>
<span class="n">actor_list</span> <span class="o">=</span> <span class="p">[</span><span class="s1">&#39;Susan Sarandon&#39;</span><span class="p">,</span><span class="s1">&#39;Julia Roberts&#39;</span><span class="p">]</span>

<span class="c1"># use pandas.DataFrame.isin to find all the movies that have at least one of the actors in our list</span>
<span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="o">.</span><span class="n">actor</span><span class="o">.</span><span class="n">isin</span><span class="p">(</span><span class="n">actor_list</span><span class="p">)]</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[75]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>353</th>
      <td>Alfie</td>
      <td>Susan Sarandon</td>
      <td>32</td>
      <td>Par.</td>
      <td>1946-10-04</td>
      <td>0.0</td>
      <td>2004-11-05</td>
      <td>40000000.0</td>
      <td>13395939.0</td>
      <td>35195939.0</td>
    </tr>
    <tr>
      <th>442</th>
      <td>America's Sweethearts</td>
      <td>Julia Roberts</td>
      <td>14</td>
      <td>SonR</td>
      <td>1967-10-28</td>
      <td>0.0</td>
      <td>2001-07-20</td>
      <td>46000000.0</td>
      <td>93607673.0</td>
      <td>160648493.0</td>
    </tr>
    <tr>
      <th>607</th>
      <td>Anywhere But Here</td>
      <td>Susan Sarandon</td>
      <td>25</td>
      <td>Fox</td>
      <td>1946-10-04</td>
      <td>0.0</td>
      <td>1999-11-12</td>
      <td>23000000.0</td>
      <td>18653615.0</td>
      <td>18653615.0</td>
    </tr>
    <tr>
      <th>624</th>
      <td>Arbitrage</td>
      <td>Susan Sarandon</td>
      <td>39</td>
      <td>RAtt.</td>
      <td>1946-10-04</td>
      <td>0.0</td>
      <td>2012-09-14</td>
      <td>12000000.0</td>
      <td>7919574.0</td>
      <td>35830713.0</td>
    </tr>
    <tr>
      <th>686</th>
      <td>August: Osage County</td>
      <td>Julia Roberts</td>
      <td>28</td>
      <td>Wein.</td>
      <td>1967-10-28</td>
      <td>0.0</td>
      <td>2013-12-25</td>
      <td>25000000.0</td>
      <td>37738810.0</td>
      <td>50738810.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="unique">unique<a class="anchor-link" href="#unique">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[76]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># how many unique studio names are there?</span>
<span class="nb">print</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">studio</span><span class="o">.</span><span class="n">unique</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>151
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[77]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">studio</span><span class="o">.</span><span class="n">unique</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&#39;FoxS&#39; &#39;Par.&#39; &#39;BV&#39; &#39;Think&#39; &#39;Fox&#39; &#39;MGM/W&#39; &#39;NL&#39; &#39;WB&#39; &#39;WB (NL)&#39; &#39;Uni.&#39; &#39;Sony&#39;
 &#39;SPC&#39; &#39;Focus&#39; &#39;Rela.&#39; &#39;FoxA&#39; &#39;LGF&#39; &#39;Mira.&#39; &#39;Anch.&#39; &#39;Sum.&#39; &#39;Orion&#39; &#39;UA&#39;
 &#39;Col.&#39; &#39;MGM&#39; &#39;ORF&#39; &#39;WIP&#39; &#39;ParV&#39; &#39;A24&#39; &#39;RAtt.&#39; &#39;PicH&#39; &#39;Cinc&#39; &#39;Wein.&#39; &#39;P/DW&#39;
 &#39;FRun&#39; &#39;SGem&#39; &#39;SonR&#39; &#39;Lori&#39; &#39;NM&#39; &#39;LG/S&#39; &#39;Magn.&#39; &#39;Strand&#39; &#39;DW&#39; &#39;Eros&#39;
 &#39;Lions&#39; &#39;FL&#39; &#39;Vari.&#39; &#39;Viv.&#39; &#39;CE&#39; &#39;VE&#39; &#39;P4&#39; &#39;First&#39; &#39;Echo&#39; &#39;RTWC&#39; &#39;Dim.&#39;
 &#39;CBS&#39; &#39;USA&#39; &#39;MNE&#39; &#39;Circ&#39; &#39;Rom.&#39; &#39;Can.&#39; &#39;Film&#39; &#39;Art.&#39; &#39;FFn.&#39; &#39;Free&#39; &#39;IFC&#39;
 &#39;App.&#39; &#39;CityL&#39; &#39;Over.&#39; &#39;ATO&#39; &#39;Gram.&#39; &#39;TriS&#39; &#39;AL&#39; &#39;IDP&#39; &#39;ParC&#39; &#39;Fabr.&#39;
 &#39;WGUSA&#39; &#39;BST&#39; &#39;FD&#39; &#39;Wells&#39; &#39;Dar.&#39; &#39;Gold.&#39; &#39;Acc.&#39; &#39;Imag.&#39; &#39;BDF&#39; &#39;Dest.&#39;
 &#39;OMNI/FSR&#39; &#39;TRR&#39; &#39;FInd.&#39; &#39;Emb&#39; &#39;Trim.&#39; &#39;Vita.&#39; &#39;YFG&#39; &#39;Ode.&#39; &#39;Drft.&#39;
 &#39;Roxie&#39; &#39;W/Dim.&#39; &#39;Good&#39; &#39;Cow.&#39; &#39;LGP&#39; &#39;WHE&#39; &#39;Prior.&#39; &#39;Rog.&#39; &#39;Code&#39; &#39;LD&#39;
 &#39;Oct.&#39; &#39;PMKBNC&#39; &#39;Lot47&#39; &#39;NCeV&#39; &#39;E1&#39; &#39;IA&#39; &#39;Mont.&#39; &#39;RS&#39; &#39;Osci.&#39; &#39;PH&#39; &#39;AIP&#39;
 &#39;AFFRM&#39; &#39;NYer&#39; &#39;RCR&#39; &#39;IMG/B&#39; &#39;GldC&#39; &#39;NW&#39; &#39;SMod&#39; &#39;Isld&#39; &#39;Boro.&#39; &#39;Slow&#39;
 &#39;Sav.&#39; &#39;RKO&#39; &#39;TFA&#39; &#39;Istr&#39; &#39;Triu&#39; &#39;Alc&#39; &#39;Atl&#39; &#39;Cohen&#39; &#39;Indic.&#39; &#39;Poly&#39;
 &#39;Scre.&#39; &#39;STX&#39; &#39;Pala.&#39; &#39;Saban&#39; &#39;SenD&#39; &#39;Strat.&#39; &#39;Mang.&#39; &#39;AFD&#39; &#39;Excel&#39; &#39;IW&#39;
 &#39;BPic&#39; &#39;GK&#39; &#39;Reg.&#39; &#39;RM&#39; &#39;NxtM&#39; &#39;FCW&#39; &#39;OrionC&#39;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[78]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># unique values are unsorted so if you want them sorted...</span>
<span class="nb">print</span><span class="p">(</span><span class="nb">sorted</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">studio</span><span class="o">.</span><span class="n">unique</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[&#39;A24&#39;, &#39;AFD&#39;, &#39;AFFRM&#39;, &#39;AIP&#39;, &#39;AL&#39;, &#39;ATO&#39;, &#39;Acc.&#39;, &#39;Alc&#39;, &#39;Anch.&#39;, &#39;App.&#39;, &#39;Art.&#39;, &#39;Atl&#39;, &#39;BDF&#39;, &#39;BPic&#39;, &#39;BST&#39;, &#39;BV&#39;, &#39;Boro.&#39;, &#39;CBS&#39;, &#39;CE&#39;, &#39;Can.&#39;, &#39;Cinc&#39;, &#39;Circ&#39;, &#39;CityL&#39;, &#39;Code&#39;, &#39;Cohen&#39;, &#39;Col.&#39;, &#39;Cow.&#39;, &#39;DW&#39;, &#39;Dar.&#39;, &#39;Dest.&#39;, &#39;Dim.&#39;, &#39;Drft.&#39;, &#39;E1&#39;, &#39;Echo&#39;, &#39;Emb&#39;, &#39;Eros&#39;, &#39;Excel&#39;, &#39;FCW&#39;, &#39;FD&#39;, &#39;FFn.&#39;, &#39;FInd.&#39;, &#39;FL&#39;, &#39;FRun&#39;, &#39;Fabr.&#39;, &#39;Film&#39;, &#39;First&#39;, &#39;Focus&#39;, &#39;Fox&#39;, &#39;FoxA&#39;, &#39;FoxS&#39;, &#39;Free&#39;, &#39;GK&#39;, &#39;GldC&#39;, &#39;Gold.&#39;, &#39;Good&#39;, &#39;Gram.&#39;, &#39;IA&#39;, &#39;IDP&#39;, &#39;IFC&#39;, &#39;IMG/B&#39;, &#39;IW&#39;, &#39;Imag.&#39;, &#39;Indic.&#39;, &#39;Isld&#39;, &#39;Istr&#39;, &#39;LD&#39;, &#39;LG/S&#39;, &#39;LGF&#39;, &#39;LGP&#39;, &#39;Lions&#39;, &#39;Lori&#39;, &#39;Lot47&#39;, &#39;MGM&#39;, &#39;MGM/W&#39;, &#39;MNE&#39;, &#39;Magn.&#39;, &#39;Mang.&#39;, &#39;Mira.&#39;, &#39;Mont.&#39;, &#39;NCeV&#39;, &#39;NL&#39;, &#39;NM&#39;, &#39;NW&#39;, &#39;NYer&#39;, &#39;NxtM&#39;, &#39;OMNI/FSR&#39;, &#39;ORF&#39;, &#39;Oct.&#39;, &#39;Ode.&#39;, &#39;Orion&#39;, &#39;OrionC&#39;, &#39;Osci.&#39;, &#39;Over.&#39;, &#39;P/DW&#39;, &#39;P4&#39;, &#39;PH&#39;, &#39;PMKBNC&#39;, &#39;Pala.&#39;, &#39;Par.&#39;, &#39;ParC&#39;, &#39;ParV&#39;, &#39;PicH&#39;, &#39;Poly&#39;, &#39;Prior.&#39;, &#39;RAtt.&#39;, &#39;RCR&#39;, &#39;RKO&#39;, &#39;RM&#39;, &#39;RS&#39;, &#39;RTWC&#39;, &#39;Reg.&#39;, &#39;Rela.&#39;, &#39;Rog.&#39;, &#39;Rom.&#39;, &#39;Roxie&#39;, &#39;SGem&#39;, &#39;SMod&#39;, &#39;SPC&#39;, &#39;STX&#39;, &#39;Saban&#39;, &#39;Sav.&#39;, &#39;Scre.&#39;, &#39;SenD&#39;, &#39;Slow&#39;, &#39;SonR&#39;, &#39;Sony&#39;, &#39;Strand&#39;, &#39;Strat.&#39;, &#39;Sum.&#39;, &#39;TFA&#39;, &#39;TRR&#39;, &#39;Think&#39;, &#39;TriS&#39;, &#39;Trim.&#39;, &#39;Triu&#39;, &#39;UA&#39;, &#39;USA&#39;, &#39;Uni.&#39;, &#39;VE&#39;, &#39;Vari.&#39;, &#39;Vita.&#39;, &#39;Viv.&#39;, &#39;W/Dim.&#39;, &#39;WB&#39;, &#39;WB (NL)&#39;, &#39;WGUSA&#39;, &#39;WHE&#39;, &#39;WIP&#39;, &#39;Wein.&#39;, &#39;Wells&#39;, &#39;YFG&#39;]
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Using-seaborn's-groupby-support">Using seaborn's groupby support<a class="anchor-link" href="#Using-seaborn's-groupby-support">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[79]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">!</span> pip install --upgrade seaborn -q
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[80]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">n_top</span> <span class="o">=</span> <span class="mi">15</span>
<span class="c1"># we only want one row per movie, we don&#39;t care about actors</span>
<span class="n">by_movie_df</span> <span class="o">=</span> <span class="n">df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;title&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">first</span><span class="p">()</span>
<span class="n">by_movie_df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[80]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>(500) Days of Summer</th>
      <td>Chloe Moretz</td>
      <td>11</td>
      <td>FoxS</td>
      <td>1997-02-10</td>
      <td>0.0</td>
      <td>2009-07-17</td>
      <td>7500000.0</td>
      <td>32391374.0</td>
      <td>59101642.0</td>
    </tr>
    <tr>
      <th>10 Cloverfield Lane</th>
      <td>Mary Elizabeth Winstead</td>
      <td>4</td>
      <td>Par.</td>
      <td>1984-11-28</td>
      <td>0.0</td>
      <td>2016-03-11</td>
      <td>5000000.0</td>
      <td>69793284.0</td>
      <td>101493284.0</td>
    </tr>
    <tr>
      <th>102 Dalmatians</th>
      <td>Glenn Close</td>
      <td>7</td>
      <td>BV</td>
      <td>1947-03-19</td>
      <td>0.0</td>
      <td>2000-11-22</td>
      <td>85000000.0</td>
      <td>66941559.0</td>
      <td>66941559.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[81]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># select only the top N studios, by total production budget of all movies</span>
<span class="n">top_studio_names</span> <span class="o">=</span> <span class="n">by_movie_df</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">&#39;studio&#39;</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">&#39;production_budget&#39;</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span><span class="o">.</span><span class="n">index</span><span class="p">[:</span><span class="n">n_top</span><span class="p">]</span>

<span class="n">top_studio_df</span> <span class="o">=</span> <span class="n">by_movie_df</span><span class="p">[</span><span class="n">by_movie_df</span><span class="o">.</span><span class="n">studio</span><span class="o">.</span><span class="n">isin</span><span class="p">(</span><span class="n">top_studio_names</span><span class="p">)]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[82]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">top_studio_df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">4</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[82]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>actor</th>
      <th>rank</th>
      <th>studio</th>
      <th>bday</th>
      <th>male</th>
      <th>release_date</th>
      <th>production_budget</th>
      <th>domestic_gross</th>
      <th>worldwide_gross</th>
    </tr>
    <tr>
      <th>title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 Cloverfield Lane</th>
      <td>Mary Elizabeth Winstead</td>
      <td>4</td>
      <td>Par.</td>
      <td>1984-11-28</td>
      <td>0.0</td>
      <td>2016-03-11</td>
      <td>5000000.0</td>
      <td>69793284.0</td>
      <td>101493284.0</td>
    </tr>
    <tr>
      <th>102 Dalmatians</th>
      <td>Glenn Close</td>
      <td>7</td>
      <td>BV</td>
      <td>1947-03-19</td>
      <td>0.0</td>
      <td>2000-11-22</td>
      <td>85000000.0</td>
      <td>66941559.0</td>
      <td>66941559.0</td>
    </tr>
    <tr>
      <th>12 Rounds</th>
      <td>John Cena</td>
      <td>4</td>
      <td>Fox</td>
      <td>1977-04-23</td>
      <td>1.0</td>
      <td>2009-03-27</td>
      <td>20000000.0</td>
      <td>12234694.0</td>
      <td>17306648.0</td>
    </tr>
    <tr>
      <th>13 Hours: The Secret Soldiers of Benghazi</th>
      <td>John Krasinski</td>
      <td>4</td>
      <td>Par.</td>
      <td>1979-10-20</td>
      <td>1.0</td>
      <td>2016-01-15</td>
      <td>50000000.0</td>
      <td>52853219.0</td>
      <td>68053219.0</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[83]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">14</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>

<span class="c1"># we pass the studio column to sns.violinplot</span>
<span class="c1"># sns.violinplot(top_studio_df.production_budget, groupby=top_studio_df.studio) # old syntax</span>
<span class="n">sns</span><span class="o">.</span><span class="n">violinplot</span><span class="p">(</span><span class="s1">&#39;studio&#39;</span><span class="p">,</span><span class="s1">&#39;production_budget&#39;</span><span class="p">,</span><span class="n">data</span><span class="o">=</span><span class="n">top_studio_df</span><span class="p">)</span> <span class="c1"># new syntax</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Production budget distributions for the top 10 studios&#39;</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABIYAAALCCAYAAACr9thAAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAAPYQAAD2EBqD+naQAAIABJREFUeJzs3Xl4U3XaxvE7XWgL1AIK78iiSBkoYllFNhVlEEFEEJRN
QVzHBRgUlIIOgjKgsgzWijMgssumgKAgUl4UGTdQUGHABVBkX8pS2tIlyfsHb0O2pkmaNk3O93Nd
XBc5SZOnp+ck59x5fr9jslqtVgEAAAAAAMBwIoJdAAAAAAAAAIKDYAgAAAAAAMCgCIYAAAAAAAAM
imAIAAAAAADAoAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAM
imAIABA0K1asUFJSkg4fPlzmr52SkqKOHTuW+et+8803SkpK0ieffFJmr7V169ZSf62ScldrWf6N
OnbsqNGjR9tur1y5UklJSdq1a1eZvP7AgQM1cODAMnktf2zevFk9e/ZUkyZN1KhRI50/fz4odSQl
JWnChAlBeW0EnrvPgPK+LwBAOCIYAgCDKjzxLfzXpEkT3X777Xr55Zd16tSpMqnBZDLJZDKV2vMf
P35caWlp2rNnj9vXjogIzsdgaf7OwXitf//730pPTy/x8zjX6s/faO/evUpLS/M5bHS3LQZ63RVX
W7C2x+KcOXNGTz/9tGJjY/Xiiy/qtddeU1xcXKm93vbt25WWlha08EkK3DbtrxMnTmjKlCkaNGiQ
WrRoUWzA+91336l///5q1qyZbrzxRk2YMEHZ2dkBqcXffcobRX0GlNd9AQDCVVSwCwAABI/JZNLf
/vY31apVS7m5ufr222+1ePFibd68WR9++KFiYmKCXWKJFAZDtWvXVlJSksN9EyZMkMViCUpdVqs1
KK9bWv71r3+pS5cu6tSpU0Cf15+/0a+//qq0tDS1bt1aNWvW9PrnPv7441I/GfVU25w5c0r1tUvi
xx9/VHZ2toYPH642bdqU+utt375db775pnr16qXKlSuX+uu5U1rbtLf279+v2bNn6+qrr1bDhg21
Y8eOIh+7e/duPfjgg0pMTNTo0aN19OhRzZ49WwcOHNDMmTNLXIu/+5S/yvO+AADhimAIAAzupptu
UuPGjSVJ99xzj6pUqaK5c+dq48aNuuOOO9z+TE5OTql2DASKpwAmMjJSkZGRZVgNfOXP38hqtfrU
6ZObm6uYmBhFR0f7Wp7PPNUWFVV+D8kKOwjj4+MD9pye3kPCLTj1x3XXXaevv/5al112mdavX6/h
w4cX+dhp06YpISFBCxcuVMWKFSVJNWvW1NixY/XFF1+oXbt2JarF132qpMrzvgAA4Yo+TQCAgzZt
2shqtergwYOSLs0BsXXrVo0bN07t2rXTLbfcYnv8f//7Xz3yyCNq2bKlmjdvrsGDB+v77793ed5f
f/1VgwYNUtOmTdWhQwe99dZbbrtBkpKSlJaW5rLceQ4YScrMzNTEiRPVsWNHJScnq0OHDho1apTO
nDmjb775Rvfee69MJpNSUlKUlJSkRo0aadWqVZLcz1+Tk5OjV155RbfccouSk5PVpUsXvfPOO25r
nDBhgtLT09W9e3clJyfrzjvv1Oeff178CtbFTi2z2axp06bpxhtvVPPmzfXEE0/o6NGjxf7O0sU5
OAYNGuSw7NixY3ryySfVvHlztWvXTpMmTVJeXp7bk+xFixapU6dOatq0qfr06aNt27a5fc68vDyl
pqaqc+fOSk5O1i233KLJkycrLy/PYV1cuHDBYWiiu5r9qdXd3+ijjz5Sr1691KJFC7Vs2VLdu3fX
ggULJF0cHll4Aj1w4EDb37xwCE7Hjh31+OOPa8uWLerdu7eaNGmipUuXelzXOTk5Gjt2rFq3bq2W
LVtq1KhROnfunMNjvNlmi6vN3frPyMjQmDFj1L59ezVp0kQ9evSwbb+FDh06pKSkJM2ZM0fLli3T
bbfdpuTkZN1zzz368ccfHR578uRJjR49Wh06dFBycrJuvPFGPfnkkx6HCA0cOFApKSmSpN69e7v8
fdetW6devXqpadOmatOmjZ599lkdO3bM4TlSUlLUvHlz/fHHH3r00UfVokULPfvss25fLy0tTZMn
T7atv8L15FyjN/vesWPHNHr0aLVv3972uPfff7/I37VQcdu0N+95hT+7bdu2YrcfdypWrKjLLrus
2MedP39eX375pXr06GELhSSpZ8+eiouL07p164p9jpLsU768X3v7GeDvvlDU7zJ//vxi1wEAGB2R
PADAwe+//y5JqlKliqRL86yMHz9e1apV01NPPaWcnBxJ0i+//KL77rtP8fHxeuyxxxQZGamlS5dq
4MCBWrhwoZo0aSLp4gnpwIEDZbFY9Ne//lVxcXFaunRpiYaqZWdna8CAAdq/f7969+6ta6+9VqdP
n9b//u//6ujRo6pfv76GDRum1NRU9e3bV9dff70kqXnz5rbfy/lb8Mcff1xbt27VPffco6SkJG3Z
skWvvfaajh8/bjs5LrRt2zZ98sknGjBggCpVqqQFCxZo2LBh+vTTT5WQkOCxdqvVqrfeeksRERF6
9NFHlZGRoblz5+rBBx/UBx98oAoVKvi0LnJzczVo0CAdO3ZMgwYNUvXq1fXBBx/oq6++cvkd3333
Xb388stq1aqVHnzwQR08eFBPPfWUEhIS9Kc//cmhxieeeELfffed+vXrp3r16umnn37SvHnz9Pvv
v9tOBidPnqznn3/eFjJJ0lVXXRWQWp3/Rv/5z380YsQItW/fXvfee6+ki/OffPfddxo4cKCuv/56
27b3xBNPqF69epKkxMRE23Ps379fI0aMUL9+/dS3b19dc801RdZqtVr10ksvKSEhQcOGDdP+/fv1
7rvv6vDhw7YTZ295U5vzerr//vv1xx9/6P7771ft2rX18ccfKyUlRZmZmS6T865Zs0ZZWVnq16+f
TCaTZs2apWHDhik9Pd3WdTVkyBDt27dPAwcOVM2aNXXq1Cl98cUXOnz4cJFDhJ588kmtW7dOy5cv
1/Dhw1WrVi3b33fFihUaM2aMmjZtqhEjRujUqVOaN2+etm/frlWrVtmGgRUGoQ8//LBatmyplJQU
xcbGun29zp07a//+/Vq7dq2ef/552/tQtWrVbI/xZt87deqU+vTpo8jISA0cOFBVq1bV5s2b9fzz
zysrK8sleLDnaZv29j2vUKC2n6L8/PPPKigosHV9FoqOjlajRo303//+1+PPB2Kf8kZJPgO83ReK
+l22b9/u8e8NACAYAgDDy8zM1OnTp5WXl6dvv/1WM2bMUFxcnENXkCRVrVpV8+bNczhRnz59usxm
sxYvXqxatWpJknr06KEuXbpo8uTJtpOfmTNn6syZM1q+fLmuu+46SRe/0e7cubPfdb/99tu2uS/+
8pe/2JY//vjjtv/ffPPNSk1NVfPmzdW9e3ePz5eenq6vv/5azzzzjB577DFJ0oABA/S3v/1N8+fP
13333ac6derYHr9v3z6tXbtWtWvXliTdcMMN6tGjhz788EPdd999xdZ/7tw5rVu3zjacplGjRho+
fLiWLVum+++/3/sVIWnJkiU6cOCAXn/9dds67dOnj+666y6Hx+Xn5ys1NVVNmzbVvHnzbHPqNGzY
UCkpKQ7B0OrVq/XVV19p4cKFtjBNkv785z9r3Lhx2rFjh5o1a6bu3btr7Nixql27drHr2Jda3fns
s88UHx+v2bNnu72/Tp06uv7667Vw4UK1a9dOrVq1cnnMgQMHNHv2bK+H18TExGju3Lm2cOXKK6/U
lClTtGnTJt16661ePYe3tdlbsmSJ9u/frylTpqhbt26SpH79+um+++7T9OnT1bt3b4cOkSNHjmjD
hg22MKZu3bp66qmntGXLFnXo0EGZmZnasWOHRo0apQcffND2c4XbelHatm2ro0ePavny5Q7DTgsK
CjR16lQ1bNhQCxYssIWZLVq00F//+lfNnTtXQ4YMsT1Pfn6+unbtqqefftrj6zVo0ECNGzfW2rVr
9Ze//MVtYOXNvjdt2jRZrVatWrXK1nnTt29fjRgxQmlpaerXr1+RAaynbdrb97xCgdp+inLixAmZ
TCZVr17d5b7q1avr22+/9fjzgdinvFGSzwBv94XifhcAQNEYSqaL3zw9/vjjuummm5SUlKSNGzf6
/Byff/65+vbtqxYtWqht27YaNmyYDh06VArVAkDgWK1WDR48WG3btlWHDh00YsQIVa5cWW+++aZq
1Khhe5zJZLINyypksVj0xRdf6LbbbrOdIEkXT0buvPNOfffdd8rKypJ08VLXTZs2tZ0QSBeDJm+C
hKJs2LBBSUlJDqFQSWzevFlRUVEuocxDDz0ki8WizZs3Oyxv166d7cRUuhiuVK5c2TYErziFQz0K
denSRdWrV9dnn33mV+3Vq1d3OMmKiYmxdTsU2rlzp86cOaN7773XYaLl7t27u3Q5rV+/XvXq1VPd
unV1+vRp27/WrVvLarXq66+/9rlOX2p157LLLlNOTo7XQ/bcqV27tk9zrhR2nRTq37+/IiMj/fo7
+WLz5s264oorbCfC0sU5lwYNGqTs7GyXK1R169bNYaLm66+/XlarVX/88Yck2eZR+vrrr70aylSc
nTt36tSpUxowYIBDwNKhQwfVq1dPn376qcvP9O/fv8SvK3m3723YsEG33nqrzGazw/bbvn17ZWZm
ateuXT6/ri/veYVKe/u5cOGCJLkNuWJiYpSbm+vx5wOxT3mjJJ8B3u4LZfW7AEA4omNIF4cjNGrU
SPfcc4+GDh3q888XtuE/9NBDmjJlis6fP6+JEydq6NChWrFiRSlUDACBYTKZ9OKLL+rqq69WVFSU
Lr/8cttQAWf2J0LSxTkfcnJyVLduXZfHJiYmymKx6OjRo0pMTNThw4fVrFkzl8d5GsZTnAMHDuj2
22/3++edHT58WDVq1HDowpAuDZlwnuPkyiuvdHmOyy67TGfPnvXq9a6++mq3y/z5UuHw4cNun895
/R4+fFgmk8llqFdkZKTL3/f333/Xvn371LZtW5fnNZlMtgmJS6tWdwYMGKCPP/5Yjz32mGrUqKH2
7dura9euuummm7x+fftAoTgmk8ml1ooVK6p69eql/uXP4cOH3e5b9erVk9VqdXl9+24vSbYumcLt
sUKFCho5cqRee+01tWvXTs2aNdMtt9yinj176oorrvCrPpPJVGSN3333ncOyyMhIlxr9Vdy+l5GR
oXPnzmnZsmW2OaTs+bv9+vKeV/g6pb39FA7Js5/3q1DhxOqeBGKf8kZJPgO83RfK6ncBgHBEMKSL
Qw1uvvlmSe6vhJGXl6d//vOf+uijj5SZmakGDRpoxIgRuuGGGyRJu3btksVicbhixEMPPaSnnnpK
ZrOZq94AKNeSk5Nd5qdwp6g5QcpKsC4tX5Si3tsDeUWloq4EZLFYSv2zxWKxqEGDBho9erTb38nd
yXlpq1atmlatWqUtW7Zo8+bN2rx5s1asWKG7775bkyZN8uo5SjKvla/Kcpv1Znt84IEH1LFjR23c
uFGff/65UlNTNXPmTM2fP19JSUmlWp+v82Z5UtzvWrje77rrLvXs2dPtYxs2bBiweoKpevXqslqt
OnHihMt9J06ccOj8dCcQ+5Q7wXi/Lq3fBQCMgKFkXnjppZf0/fffa/r06Vq9erW6dOmiRx99VAcO
HJAkNW7cWBEREXr//fdlsViUmZmpDz74QO3atSMUAhC2qlWrpri4OO3fv9/lvr179yoiIsLWIVCz
Zk399ttvLo/bt2+fy7KEhARlZmY6LMvPz3c58bnqqqv0yy+/eKzRl0ss16xZU8ePH1d2drbD8r17
99ruDyR36+P333936Nxxty4k1+6lmjVr2j6T7Dmv35o1a8pqtdomGC9kNptdOhiuuuoqnT17Vm3a
tFHbtm1d/tl/g+/revam1qJERUXplltu0dixY5Wenq6+fftq1apVtiFTgbystrt1lZ2drRMnThT7
d3K3zfq6njztM84dXt6qU6eOBg8erNmzZ+vDDz9Ufn6+2yvveVOf1Wp1u//v37+/RPtLSf+G1apV
U6VKlWQ2m91uu23btnWYzNrbGnx5z5O8335KokGDBoqKitLOnTsdlufn52v37t1q1KhRsc9Rkn3K
223fl88AZ77sC8X9LgAA9wiGinHkyBGtXLlSr7/+ulq0aKE6derowQcfVIsWLWyXPK1du7Zmz56t
adOmKTk5Wa1atdKxY8c0ffr0IFcPAKUnIiJC7du318aNGx2CipMnT+qjjz5Sy5YtValSJUkX5x35
/vvvHS6fnZGRoQ8//NDleevUqeMyf8rSpUtlNpsdlnXu3Fl79uxRenp6kTUWzuHjzZwqHTp0UEFB
gRYuXOiwfO7cuYqIiLB1lgbKBx984DAfybp163TixAl16NDBtqxOnTrasWOHCgoKbMs2bdqkI0eO
uNR+/PhxrV+/3rYsJydHy5cvd3jcddddpypVqmj58uUO3+ivXr3aZQhc165ddfToUS1btsyl9tzc
XNuV6aSLw2PcBVjueFurO2fOnHFZ1qBBA0mXhtLExcXJarUGZB4d6eK2Z7/+3333XZnNZpe/kzfb
rC+1dejQQSdPntTatWtty8xmsxYsWKBKlSr5PAnwhQsXXIYb1a5dW5UqVXI7DKk41113nS6//HIt
WbJE+fn5tuWfffaZ9u7d6zJ5vS982W/diYiIUOfOnfXJJ5+4DY8zMjKKfQ5327Qv73mFvNl+SqJy
5cpq27atVq9e7RBqr1q1Sjk5OeratavHny/pPuXttu/LZ4Azb/cFb34XAIB7DCUrxs8//yyz2azb
b7/doR07Pz9fVatWlXTxgOCFF15Qr1691K1bN50/f16vv/66hg4dqjlz5gSrdAAolrfDnop63PDh
w/XFF1+of//+GjBggCIiIrRs2TLl5+fr2WeftT3ukUce0QcffKBHHnlEAwcOVFxcnJYtW6ZatWrp
p59+cnjOe++9Vy+++KKGDRumdu3aac+ePfrPf/7j8g3/ww8/rPXr12v48OHq1auXGjdurDNnzmjT
pk0aP368GjZsqKuuukqXXXaZlixZoooVK6pixYpq2rSp22/rO3bsqNatW2v69Ok6ePCg7XL1mzZt
0uDBgx2uSBYICQkJGjBggHr16qWTJ09q/vz5qlu3ru0yy4XrYv369Xr44YfVtWtXHThwQKtXr3aZ
t6RPnz5atGiRnnvuOe3cudN2CXj7ya2li5ewHjp0qCZMmKBBgwapa9euOnjwoFasWKGrr77aoTOg
R48eWrduncaNG6evv/5aLVq0kNls1t69e/Xxxx/rnXfesQ1BbNy4sb744gvNnTtXNWrUUO3atV0u
2+1rre688MILOnv2rFq3bq0//elPOnTokBYtWqRGjRrZ5nVp1KiRIiMjNWvWLGVmZqpChQpq06ZN
sR0iRcnPz9fgwYPVtWtX7du3T4sXL9b111/vcEUpb7dZX2rr27evli5dqpSUFP3444+2S3Tv2LFD
zz//vMtcWMX57bff9MADD6hr166qX7++IiMjtWHDBp06dUp33nlnsT/v/B4QFRWlkSNHasyYMbr/
/vvVrVs3nTx5UgsWLLB1JfmrcePGslqt+uc//6k77rhD0dHR6tixo0/DWUeOHKlvvvlGffr00b33
3qv69evrzJkz2rVrl7766qtiJ08vapv29j2vkDfbT1FmzJghk8mkX3/91XaFtW3btkmSnnjiCdvj
nn76afXv31/333+/+vTpoyNHjmju3Lm68cYb1b59e4+vUdJ9yttt35fPAGfe7gve/C4AAPcIhoqR
lZWlqKgorVy50uEKLpJsH0SLFi1SfHy8RowYYbtvypQp6tChg3744YciD44BINi8HbJR1OPq16+v
d999V1OnTtXMmTNlsVjUrFkzTZ06VcnJybbHVa9eXQsWLNDLL7+st99+W1WqVFH//v11xRVX6IUX
XnB4zj59+ujQoUN677339Pnnn6tVq1Z65513NHjwYIc6KlasqHfffVepqalKT0/XqlWrdPnll6tt
27a24RxRUVF69dVXNW3aNI0bN05ms1mTJk2yBUP2z2cymfSvf/1LqampWrt2rVauXKlatWpp1KhR
Lie5Ra0Pk8nk1To1mUz661//qp9++kmzZs1SVlaW2rVrpxdffNFhDpwbb7xRKSkpmjt3riZNmqTk
5GTNnDlTkyZNcnid2NhYzZs3Ty+//LIWLlyouLg43XXXXbrpppv0yCOPOLx24eW833nnHb322mtq
0KCB3nrrLf3jH/9weG2TyaQZM2Zo7ty5WrVqldLT0xUbG2s76bcfSpaSkqKxY8fq9ddf14ULF9Sz
Z88iP/t8qdV5Xffo0UNLly7VkiVLdO7cOduViuwvi37FFVdo/Pjxmjlzpl544QWZzWbNnz/fdqLq
y9/OZDLp73//u9asWaPU1FQVFBSoe/fuev755x0e5+0260ttMTExWrBggaZOnaoPPvhA58+f1zXX
XKNJkya5zJtT1HZnv/xPf/qTunfvri+//FKrV69WVFSU6tWrp9dff12dOnVyu06cn8vZ3Xffrbi4
OM2cOVNTp05VXFycOnfubLu6YXE/X5Tk5GQNHz5cS5Ys0ZYtW2SxWLRx40bVrFnT67/f5ZdfruXL
l2vGjBlKT0/X4sWLVaVKFf35z392G+A4K2qb9vY9r7Amb7afoqSmptp+J5PJZLugiclkcgiGrr32
Ws2ZM0dTpkzRK6+8okqVKunee+/VM888U+xrlHSf8nbb9+UzoPB3LOTtvuDN7wIAcM9kDeQsmWEg
KSlJb775pu3yx7/99pu6du2qhQsXqmXLlm5/5tVXX9X27du1ZMkS27Ljx4/r5ptv1pIlS9xehQEA
gPLCarWqTZs2uv322/XSSy8Fuxwg5K1cuVJjxozRe++959Xk/gAABFPIzjGUlpampKQkh3933HGH
X8+VnZ2tPXv2aPfu3ZKkP/74Q3v27NGRI0dUt25d3XnnnRo1apQ2bNiggwcP6ocfftDMmTP12Wef
SZKtM+jNN9/U77//rl27dmn06NGqXbu2rr322oD9zgAAlJS7uTZWrlxpG4IBAAAAYwnpoWR//vOf
NW/ePNu4d3+vALZz504NGjTI1ob86quvSpJ69uypSZMm6ZVXXtFbb72lV199VceOHVPVqlXVrFkz
2/jwNm3aaMqUKXr77bc1e/ZsxcXFqVmzZpo1a1ZAL88KAEBJ7dixQ5MmTVKXLl1UpUoV7dq1S++/
/74aNmyo22+/PdjlAWGDpnwAQKgI6WAoKirK78kk7d1www3as2dPkfdHRkZqyJAhHsco33HHHX53
LAEAUFZq1aqlK6+8UgsWLNDZs2eVkJCgu+++W88884yiokL6sAAoV3yZVwkAgGAK2TmG0tLSNHv2
bFWuXFkxMTFq1qyZRowYoSuvvDLYpQEAAAAAAISEkA2GPv/8c2VnZ+uaa67RiRMn9MYbb+j48eP6
8MMPfb6EKwAAAAAAgBGFbDDkLDMzU7feeqtGjx6t3r17e/UzVquVNl8AAAAAAGBYYTOZQHx8vOrW
rasDBw54/TMZGVmKiCAYAgAAAAAA4aVq1UpePS5sgqGsrCwdOHBAPXv29PpnLBarLJawaJgCAAAA
AADwWcgGQ6+++qo6duyomjVr6tixY3rjjTcUFRWlbt26Bbs0AAAAAACAkBCywdCxY8c0YsQInTlz
RtWqVVPLli21dOlSVa1aNdilAQAAAAAAhISwmXzaHydOZAa7BAAAAAAAgICrXj3eq8dFlHIdAAAA
AAAAKKcIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADAoAiGAAAAAAAADIpgCAAA
AAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADAoAiGAAAAAAAADIpgCAAA
AAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADAoAiGAAAAAAAADIpgCAAA
AAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADAoAiGAAAAAAAADIpgCAAA
AAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADAoAiGAAAAAAAADIpgCAAA
AAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADAoAiGAAAAAAAADIpgCAAA
AAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIaAMHHo0EGNHz9GH3/8YbBLAQAAAACECIIhIEwsXDhX
v/zysxYunBvsUgAAAAAAIYJgCAgTP/64I9glAAAAAABCDMEQAAAAAACAQREMAQAAAAAAGBTBEAAA
AAAAgEERDAEAAAAAABgUwRAAAAAAAIBBEQwBAAAAAAAYFMEQAAAAAACAQREMAQAAAAAAGBTBEAAA
AAAAgEERDAEAAAAAABgUwRAAAAAAAIBBEQwBAAAAAAAYFMEQAAAAAACAQREMAQAAAAAAGBTBEAAA
AAAAgEERDAEAAAAAABgUwRAAAAAAAIBBEQwBAAAAAAAYFMEQAAAAAACAQREMAQAAAAAAGBTBEAAA
AAAAgEERDAFhyGq1BrsEAAAAAEAIIBgCwhDBEAAAAADAGwRDQFgiGAIAAAAAFI9gCAAAAAAAwKAI
hgAAAAAAAAyKYAgIQ0wxBAAAAADwBsEQAAAAAACAQREMAWGIq5IBAAAAALxBMASEIZPJFOwSAAAA
AAAhgGAIAAAAAADAoAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgIQ8w9DQAAAADwBsEQ
AAAAAACAQREMAWGJliEAAAAAQPEIhgAAAAAAAAyKYAgIQyYmGQIAAAAAeIFgCAhDBEMAAAAAAG8Q
DAEAAAAAABgUwRAAAAAAAIBBEQwBAAAAAAAYFMEQAAAAAACAQREMAQAAAAAAGBTBEAAAAAAAgEER
DAEAAACpV4VxAAAgAElEQVQAABgUwRAAAAAAAIBBEQwBAAAAAAAYFMEQAAAAAACAQYVFMDRz5kwl
JSVp0qRJwS4FAAAAAAAgZIR8MPTDDz9o6dKlSkpKCnYpAAAAAAAAISWkg6GsrCw9++yzmjBhguLj
44NdDgAAAAAAQEgJ6WDopZdeUseOHdW2bdtglwIAAAAAABByooJdgL8++ugj7d69W++//36wSwEA
AAAAAAhJIRkMHT16VBMnTtScOXMUHR3t9/NERJgUEWEKYGVA+RAVFdLNgAAAAACAMhKSwdDOnTuV
kZGhXr16yWq1SpLMZrO2bdumRYsW6ccff5TJVHzgU61aJa8eB4SaqlUrBbsEAAAAAEAICMlgqF27
dlqzZo3DspSUFCUmJuqxxx7zOuzJyMiiYwhh6fTprGCXAAAAAAAIIm8bBkIyGKpYsaLq16/vsCwu
Lk5VqlRRYmKi189jsVhlsVgDXR4QdAUFlmCXAAAAAAAIAWEzEQlDwgAAAAAAAHwTkh1D7syfPz/Y
JQAAAAAAAISUsOkYAgAAAAAAgG8IhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
oAiGAAAAAAAADIpgCAAAAAAAwKAIhgAAAAAAAAyKYAgAAAAAAMCgCIYAAAAAAAAMimAIAAAAAADA
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
"
>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>
</body>
</html>
