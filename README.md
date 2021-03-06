# drag-tabs

> This component provides the infrastructure needed to move tabs around by dragging.

[![Build Status](https://travis-ci.org/bpmn-io/drag-tabs.svg?branch=master)](https://travis-ci.org/bpmn-io/drag-tabs)

It's not this component's responsibility to the actual moving of the tab, but exposing an event based
interface that communicates when and where the tab dragging should happen.

It makes sure all the tabs inside the intended container are draggable,
ignoring the ones that are declared as so.

The component is an event emitter and it emits the following events:
- 'drag' is fired every time there is a new position
- 'end' is always fired at the end of the drag
- 'cancel' is only fired when the dragging is canceled

The three events are emitted with the following context:

```js
var context = {
	 dragTab: {HTMLElement},
	 newIndex: {Number}
};
```

## How to use

### Provide a tab container

```javascript
var $el = (
  <div>
    <ul class="my-tabs-container">
      <li class="my-tab"></li>
      <li class="my-tab"></li>
      <li class="my-tab ignore-me"></li>
    </ul>
  </div>
);
```

### Initialize dragTabs

```javascript
var drager = dragTabs($el, {
  selectors: {
    tabsContainer: '.my-tabs-container',
    tab: '.my-tab',
    ignore: '.ignore-me'
  }
});
```

### Listen to the drag event

```javascript
drager.on('drag', function(context) {
    var dragTab = context.dragTab,
        newIdx = context.newIdx;

  // move the tab to the new position
});

// move the tab to the initial position
drager.on('cancel', function(context) {});
```

### Update dragger

Every time tabs change, update the dragger:

```javascript
dragger.update();
```

## How to test

```
npm run test
```

## License

MIT
