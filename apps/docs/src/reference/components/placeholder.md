# Placeholder

> Placeholders are components that indicate that something may still be loading

## Basic Usage

At the placeholder core, you have the `b-placeholder` component:

<b-placeholder />
<b-placeholder width="65" variant="danger" />
<b-placeholder cols="6" variant="info" />

```html
<b-placeholder cols="7" />
<b-placeholder width="65" />
<b-placeholder cols="6" />
```

## Width

You can adjust the width using props `width` and `cols`. Cols is a number value 1-12, whereas width is a percentage. Width takes priority over cols

<b-placeholder width="30" cols="12" />
<b-placeholder width="75%" variant="danger" />
<b-placeholder width="12" variant="warning" />
<b-placeholder :cols="6" variant="info" />
<b-placeholder cols="8" variant="info" />

```html
<b-placeholder width="30" cols="12" />
<b-placeholder width="75%" variant="danger" />
<b-placeholder width="12" variant="warning" />
<b-placeholder :cols="6" variant="info" />
<b-placeholder cols="8" variant="info" />
```

## Placeholder Animations

Bootstrap supports two types of animations, `wave` and `glow`

* Note: when using `<b-placeholder-card>`, the image does not inherit an animation

<b-placeholder-card style="max-width: 20rem; " animation="glow" />
<b-placeholder-card style="max-width: 20rem; " animation="wave" />
<b-placeholder animation="glow" />

```html
<b-placeholder-card style="max-width: 20rem; " animation="glow" />
<b-placeholder-card style="max-width: 20rem; " animation="wave" />
<b-placeholder animation="glow" />
```

## Sizing

You can adjust the sizing of a placeholder by using the `size` prop. Acceptable values are 'xs', 'sm', or 'lg'

<b-placeholder size="lg" />
<b-placeholder size="sm" />
<b-placeholder size="xs" />

```html
<b-placeholder size="lg" />
<b-placeholder size="sm" />
<b-placeholder size="xs" />
```

## Helper Components

`b-placeholder` has several wrapper components to quickly create larger component sets, such as `b-placeholder-card`, `b-placeholder-table`, and `b-placeholder-button`

### Placeholder Wrapper

The `b-placeholder-wrapper` is a renderless component that picks between a 'loading' component, and a 'finished' component. It is useful when you have to wait for loading to finish, before rendering the actual content. Depending on the use case, you may prefer to use [Suspense](https://vuejs.org/guide/built-ins/suspense.html) instead

<b-placeholder-wrapper :loading="loading"> 
  <template #loading>
    <b-placeholder-card style="max-width: 20rem;" no-footer />
  </template>
  <b-card
    title="Card Title"
    img-src="https://picsum.photos/600/300/?image=25"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-2"
  >
    <b-card-text>
      Some quick example text to build on the card title and make up the bulk of the card's content.
    </b-card-text>
    <b-button href="#placeholder-wrapper" variant="primary">Go somewhere</b-button>
  </b-card>
</b-placeholder-wrapper>
<b-button @click="startLoading">Restart</b-button>

```html
<b-placeholder-wrapper :loading="loading"> 
  <template #loading>
    <b-placeholder-card style="max-width: 20rem;" no-footer />
  </template>
  <b-card
    title="Card Title"
    img-src="https://picsum.photos/600/300/?image=25"
    img-alt="Image"
    img-top
    tag="article"
    style="max-width: 20rem;"
    class="mb-2"
  >
    <b-card-text>
      Some quick example text to build on the card title and make up the bulk of the card's content.
    </b-card-text>
    <b-button href="#placeholder-wrapper" variant="primary">Go somewhere</b-button>
  </b-card>
</b-placeholder-wrapper>
<b-button @click="startLoading">Restart</b-button>

<script setup lang="ts">
import {ref, onMounted, watchEffect} from 'vue'

const loading = ref(false)

watchEffect(() => {
  if(loading.value === true){
    setTimeout(() => {
      loading.value = false
    }, 5000)
  }
})

const startLoading = () => {
  if(loading.value === true) return
  loading.value = true
}

onMounted(startLoading)
</script>
```

### Placeholder Buttons

You can easily render a placeholder that has the button styling by using `b-placeholder-button`

<b-placeholder-button cols="3" />

```html
<b-placeholder-button cols="3" />
```

### Placeholder Cards

Placeholders have built-in support for rendering a placeholder card with `b-placeholder-card`

<b-placeholder-card style="max-width: 20rem" />

```html
<b-placeholder-card style="max-width: 20rem" />
```

### Placeholder Tables

You can also render a full placeholder table with `b-placeholder-table`

<b-placeholder-table />

```html
<b-placeholder-table />
```

### Advanced Helper Component Usage

#### Advanced Cards

Cards expose various props and slots to make them more personalized

You can adjust the image using various props, such as `imgBlankColor`, and `imgBottom`, or you can optionally use `imgSrc` to place a real image, rather than a blank

Each section of the `b-placeholder-card` exposes its slot elements, so you can easily override the defaults. Available slots are: `img`, `header`, `default`, and `footer`

The footer also exposes some props that you can use to adjust the behavior of a button. Most notably prop `noButton`. If set to true, it will convert it to a basic placeholder appearance. Alternatively, you can use the `noFooter` prop to remove it altogether

<b-placeholder-card img-src="https://picsum.photos/1024/480/?image=1" img-bottom no-header>
  <template #footer>
    Footer
  </template>
  <template #default>
    <b-placeholder />
    <b-placeholder width="65" variant="danger" />
    <b-placeholder cols="6" variant="info" />
  </template>
</b-placeholder-card>

```html
<b-placeholder-card img-src="https://picsum.photos/1024/480/?image=1" img-bottom no-header>
  <template #footer>
    Footer
  </template>
  <template #default>
    <b-placeholder />
    <b-placeholder width="65" variant="danger" />
    <b-placeholder cols="6" variant="info" />
  </template>
</b-placeholder-card>
```

#### Advanced Tables

`b-placeholder-table` comes with various props to adjust the number of rows, columns, header/footer, and their stylings

You can adjust the number of columns and rows using props `columns` and `rows` respectively. You can use `showFooter` to show the footer, or `hideHeader` to hide the header. Both the footer and header have cellWidth, size, animation, and variant adjustments by prepending the type with the styling, eg: `headerCellWidth`, `headerSize`, `footerAnimation`, `footerVariant`

Optionally, you can manually adjust any scope of the table using slots. The following slots are available: `thead`, `default`, and `tfoot`. Do note that the slots wrap the **entire** table scope, slot `thead` is the entire thead, and slot `default` is the entire tbody, so you will likely need to manually wrap your slot usages in these elements if you plan on using them

<b-placeholder-table 
  columns="3" 
  rows="2" 
  show-footer 
  footer-variant="info" 
  header-size="lg" 
  footer-size="xs" 
  footer-columns="1" 
  header-columns="4"
>
  <template #default>
    <tbody>
        <tr>
          <td>
            <b-placeholder size="lg" variant="secondary" />
            <b-placeholder size="sm" variant="secondary" />
            <b-placeholder size="xs" variant="secondary" />
          </td>
          <td>
            <b-placeholder variant="warning" />
            <b-placeholder animation="wave" variant="warning" />
          </td>
          <td>
            <b-placeholder animation="glow" variant="danger" />
          </td>
        </tr>
    </tbody>
  </template>
</b-placeholder-table>

```html
<b-placeholder-table 
  columns="3" 
  rows="2" 
  show-footer 
  footer-variant="info" 
  header-size="lg" 
  footer-size="xs" 
  footer-columns="1" 
  header-columns="4"
>
  <template #default>
    <tbody>
        <tr>
          <td>
            <b-placeholder size="lg" variant="secondary" />
            <b-placeholder size="sm" variant="secondary" />
            <b-placeholder size="xs" variant="secondary" />
          </td>
          <td>
            <b-placeholder variant="warning" />
            <b-placeholder animation="wave" variant="warning" />
          </td>
          <td>
            <b-placeholder animation="glow" variant="danger" />
          </td>
        </tr>
    </tbody>
  </template>
</b-placeholder-table>
```


  <ComponentReference></ComponentReference>


<script setup lang="ts">
import {ref, onMounted, watchEffect} from 'vue'

const loading = ref(false)

watchEffect(() => {
  if(loading.value === true){
    setTimeout(() => {
      loading.value = false
    }, 5000)
  }
})

const startLoading = () => {
  if(loading.value === true) return
  loading.value = true
}

onMounted(startLoading)
</script>
