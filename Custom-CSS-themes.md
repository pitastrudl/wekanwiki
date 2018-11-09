There will be upcoming Custom CSS feature with input box and Save button in Admin Panel / Layout.

[Policy about Wekan UI changes](https://github.com/wekan/wekan/wiki/FAQ#policy-about-wekan-ui-changes)

## Dark mode

[by @lonix1, info and screenshot](https://github.com/wekan/wekan/issues/1149)

lonix1 created some css overrides with Stylish. It's not complete but I'm happy with it. I work in swimlanes mode, so that is what I changed (not list mode or calendar mode).

Colors:
- adds dark mode, I used vscode as a reference

Other:
- hides various useless icons and things
- hides  "add card", "add swimlane", "add list" links, until hovered (I find these very "noisy")

```css
/* HIDE PERMANENTLY -------------------------------------------------- */

/* various */
.wekan-logo,
.close-card-details { display:none; }

/* header text */
#header-quick-access >ul >li:nth-child(1) >a { font-size:0; }
#header-quick-access >ul >li:nth-child(1) >a >.fa-home{ font-size:12px; margin:0; }

/* popup menu titles (boards, swimlanes, lists, cards, labels) */
.pop-over >.header { display:none; }

/* OPTIONAL 
   card fields: received, start, due, end, members, requested, assigned
   I rarely use these... uncomment if you want to hide them */
/*
.card-details-item.card-details-item-received,
.card-details-item.card-details-item-start,
.card-details-item.card-details-item-due,
.card-details-item.card-details-item-end,
.card-details-item.card-details-item-members,
.card-details-item.card-details-item-name { display:none; }
.card-details-items:empty { display:none; }
*/

/* HIDE UNTIL HOVER -------------------------------------------------- */

/* header "+" button */
#header-quick-access .fa-plus { display:none; }
#header-quick-access:hover .fa-plus { display:inherit; }

/* "add card" links (use visibility rather than display so items don't jump) */
                    .open-minicard-composer { visibility:hidden; }
.list.js-list:hover .open-minicard-composer { visibility:visible; }
                    .list-header-menu { visibility:hidden; }
.list.js-list:hover .list-header-menu { visibility:visible; }

/* "add list/swimlane" links (use visibility rather than display so items don't jump) */
.list.js-list-composer       >.list-header { visibility:hidden; }
.list.js-list-composer:hover >.list-header { visibility:visible; }

/* DARK MODE -------------------------------------------------- */

/* headers */
#header-quick-access, #header { background-color:rgba(0,0,0,.75) !important; }
#header .board-header-btn:hover { background-color:rgba(255,255,255,0.3) !important; }

/* backgrounds: swimlanes, lists */
.swimlane { background-color:rgba(0,0,0,1); }
.swimlane >.swimlane-header-wrap,
.swimlane >.list.js-list,
.swimlane >.list-composer.js-list-composer { background-color:rgba(0,0,0,.9); }

/* foregrounds: swimlanes, lists */
.list >.list-header, .swimlane-header { color:rgba(255,255,255,.7); }

/* minicards */
.minicard { background-color:rgba(255,255,255,.4); }
.minicard-wrapper.is-selected .minicard,
.minicard:hover,
.minicard-composer.js-composer,
.open-minicard-composer:hover { background-color:rgba(255,255,255,.8) !important; color:#000; }
.minicard, .minicard .badge { color:#fff; }
.minicard:hover .badge, .minicard-wrapper.is-selected .badge { color:#000; }

/* cards */
.card-details,
.card-details .card-details-header { background-color:#ccc; }

/* sidebar */
.sidebar-tongue, .sidebar-shadow { background-color:#666 !important; }
.sidebar-content h3, .sidebar-content .activity-desc { color:rgba(255,255,255,.7) !important; }
```

If anyone improves on this, please share here.