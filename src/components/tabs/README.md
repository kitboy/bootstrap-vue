# Tabs

> Create tabbable panes of local content.


## Basic usage

```html
<b-tabs>
  <b-tab title="first" active>
    <br>I'm the first fading tab
  </b-tab>
  <b-tab title="second" >
    <br>I'm the second tab content
  </b-tab>
  <b-tab title="disabled" disabled>
    <br>Disabled tab!
  </b-tab>
</b-tabs>

<!-- basic.vue -->
```

## Cards Integration

Tabs support integrating with bootstrap cards. Just add the `card` property to
`<b-tabs>`. Note that you should add `no-body` prop on `<b-card>` element in order
to propertly decorate the card header and remove the extra padding introduced
by `card-body`.

```html
<b-card no-body>
    <b-tabs card>
        <b-tab title="Tab 1" active>
            Tab Contents
        </b-tab>
        <b-tab title="Tab 2">
            Tab Contents 2
        </b-tab>
    </b-tabs>
</b-card>

<!-- with-card.vue -->
```


## Pills variant

Tabs use the `tabs` styling by default. Just add `pills` property to `<b-tabs>` for
the pill style variant.

```html
<b-card no-body>
    <b-tabs pills card>
        <b-tab title="Tab 1" active>
            Tab Contents
        </b-tab>
        <b-tab title="Tab 2">
            Tab Contents 2
        </b-tab>
    </b-tabs>
</b-card>

<!-- tabs-pills.vue -->
```

## Bottom placement of tab controls

Visually move the tab controls to the bottom by setting the prop `end`

```html
<b-card no-body>
    <b-tabs pills card end>
        <b-tab title="Tab 1" active>
            Tab Contents
        </b-tab>
        <b-tab title="Tab 2">
            Tab Contents 2
        </b-tab>
    </b-tabs>
</b-card>

<!-- tabs-bottom.vue -->
```

**Caveats:**
- Bottom placement visually works best with the `pills` variant. When using the default 
`tabs` vairiant, you may want to provided your own custom styling classes, as Bootstrap
V4 CSS assumes the tabs will always be placed on the top of the tabs content.
- To provide a better user experience with bottom palced controls, ensure that the
content of each tab pane is the same height and fits completely within the visible
viewport, otherwise the user will need to scroll up to read the start of the tabed content.

**Note:** _the `bottom` prop has been deprecated in favor of the `end` prop._


## Vertical tabs

Have the tab controls placed on the lefthand side by setting the `vertical` prop to `true`.

```html
<b-card no-body>
    <b-tabs pills card vertical>
        <b-tab title="Tab 1" active>
            Tab Contents
        </b-tab>
        <b-tab title="Tab 2">
            Tab Contents 2
        </b-tab>
        <b-tab title="Tab 3">
            Tab Contents 3
        </b-tab>
    </b-tabs>
</b-card>

<!-- tabs-vertical.vue -->
```

Visually move the tab controls to the right hand side by setting the `end` prop:

```html
<b-card no-body>
    <b-tabs pills card vertical end>
        <b-tab title="Tab 1" active>
            Tab Contents
        </b-tab>
        <b-tab title="Tab 2">
            Tab Contents 2
        </b-tab>
        <b-tab title="Tab 3">
            Tab Contents 3
        </b-tab>
    </b-tabs>
</b-card>

<!-- tabs-vertical-end.vue -->
```

The width of the vertical tab controls will expand to fit the width of the tab title.
To control the width, set a [width utility class](/docs/reference/size-props#sizing-utility-classes)
via the prop `nav-wrapper-class`. You can use values such as `w-25` (25% width), `w-50` (50% width), etc.,
or column classes such as `col-2`, `col-3`, etc.

```html
<b-card no-body>
    <b-tabs pills card vertical nav-wrapper-class="w-50">
        <b-tab title="Tab 1" active>
            Tab Contents
        </b-tab>
        <b-tab title="Tab 2">
            Tab Contents 2
        </b-tab>
        <b-tab title="Tab 3">
            Tab Contents 3
        </b-tab>
    </b-tabs>
</b-card>

<!-- tabs-vertical-width.vue -->
```

Vertical placement visually works best with the `pills` variant. When using the default 
`tabs` vairiant, you may want to provided your own custom styling classes, as Bootstrap
V4 CSS assumes the tabs will always be placed on the top of the tabs content.

**Note:** _overflowing text may occur if your width is narrower than the tab title. You may need additional custom styling._


## Fade animation

Fade is enabled by default when changing tabs. It can disabled with `no-fade` property.
Note you should use the `<b-nav-item>` component when adding contentless-tabs to maintain
correct sizing and alignment. See the advanced usage examples below for an example.


## Add Tabs without content

If you want to add extra tabs that do not have any content, you can put them in `tabs` slot:

```html
<b-tabs>
  <!-- Add your b-tab components here-->
  <template slot="tabs">
      <b-nav-item to="#" @click="onClick">Another tab</b-nav-item>
  </template>
</b-tabs>
```


## Apply custom classes to the generated nav-tabs or pills

The tab selectors are based on Boostrap V4's `nav` markup ( i.e. `ul.nav > li.nav-item > a.nav-link`).
In some situations, you may want to add classes to the `<li>` (nav-item) and/or the
`<a>` (nav-link) on a per tab basis.   To do so, simply supply the classname to
the `title-item-class` prop (for the `<li>` element) or `title-link-class` prop (for the
`<a>` element).  Value's can be passed as a string or array of strings.

**Note:** _The `active` class is automatically applied to the active tabs `<a>` element. You may need to accomodate your custom classes for this._

```html
<template>
  <b-card no-body>
    <b-tabs card v-model="tabIndex">
      <b-tab title="Tab 1" :title-link-class="linkClass(0)">
        Tab Contents 1
      </b-tab>
      <b-tab title="Tab 2" :title-link-class="linkClass(1)">
        Tab Contents 2
      </b-tab>
      <b-tab title="Tab 3" :title-link-class="linkClass(2)">
        Tab Contents 3
      </b-tab>
    </b-tabs>
  </b-card>
</template>

<script>
export default {
  data () {
    return {
      tabIndex: 0
    }
  },
  methods: {
    linkClass (idx) {
      if (this.tabIndex === idx) {
        return ['bg-primary', 'text-light']
      } else {
        return ['bg-light', 'text-info']
      }
    }
  }
}
</script>

<!-- with-classes.vue -->
```


## Advanced Examples

### External controls

```html
<template>
  <div>
    <!-- Tabs with card integration -->
    <b-card no-body>
      <b-tabs small card v-model="tabIndex">
        <b-tab title="General">
          I'm the first fading tab
        </b-tab>
        <b-tab title="Edit profile">
          I'm the second tab
          <b-card>I'm the card in tab</b-card>
        </b-tab>
        <b-tab title="Premium Plan" disabled>
          Sibzamini!
        </b-tab>
        <b-tab title="Info">
          I'm the last tab
        </b-tab>
      </b-tabs>
    </b-card>

    <!-- Control buttons-->
    <div class="text-center">
      <b-button-group class="mt-2">
        <b-btn @click="tabIndex--">Previous</b-btn>
        <b-btn @click="tabIndex++">Next</b-btn>
      </b-button-group>
      <br>
      <span class="text-muted">Current Tab: {{tabIndex}}</span>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tabIndex: 0
    }
  }
}
</script>

<!-- tabs-controls.vue -->
```

### Dynamic Tabs

```html
<template>
  <div>
    <b-card no-body>
      <b-tabs card>
        <!-- Render Tabs -->
        <b-tab :title="`Tab ${i}`" v-for="i in tabs" :key="i">
          Tab Contents {{i}}
          <b-btn size="sm" variant="danger" class="float-right" @click="()=>closeTab(i)">
            Close tab
          </b-btn>
        </b-tab>

        <!-- New Tab Button (Using tabs slot) -->
        <b-nav-item slot="tabs" @click.prevent="newTab" href="#">
          +
        </b-nav-item>

        <!-- Render this if no tabs -->
        <div slot="empty" class="text-center text-muted">
          There are no open tabs
          <br> Open a new tab using + button.
        </div>
      </b-tabs>
    </b-card>

  </div>
</template>

<script>
export default {
  data () {
    return {
      tabs: [],
      tabCounter: 0
    }
  },
  methods: {
    closeTab (x) {
      for (let i = 0; i < this.tabs.length; i++) {
        if (this.tabs[i] === x) {
          this.tabs.splice(i, 1)
        }
      }
    },
    newTab () {
      this.tabs.push(this.tabCounter++)
    }
  }
}
</script>

<!-- dynamic-tabs.vue -->
```

## Component Reference
