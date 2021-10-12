<template>
  <div id='app'>
    <section-component>
      <template slot="title">Project Structure</template>
      <template slot="header">Vue projects can be created from a shell that has node and npm installed. The command:
        <br/><code>> vue create &lt;project-name&gt;</code><br/> will lead you through a process where you choose which
        features you'd like enabled (Test frameworks, CSS frameworks, Typescript, etc.). Vue projects will look similar
        to this:
      </template>
      <div class="two-columns">
        <div class="item">
          <img src="@/assets/filestructure.png" height="565" width="473" alt="filestructure"/>
        </div>
        <div class="item">
          <ol>
            <li>node_modules - The package.json file defines which libraries will be installed into this folder.</li>
            <li>public - Static assets that will not go through webpack (Scripts and Stylesheets won't be minified,
              missing files cause compilation errors, etc). Use this when you have a file you need to reference by name 
              (files bundled together won't have their original filename), thousands of images you need to reference 
              dynamically, etc.
            </li>
            <li>assets - icons, images, common/shared styles (such as a <code>stylebase.scss</code>, <code>printStyles.scss</code>
              etc.
            </li>
            <li>components - any custom components created for this project. For complex projects, use a folder
              hierarchy to keep related components together.
            </li>
            <li>views - these are the actual "pages" of your site - think of them as the templates on which all of your
              components are placed
            </li>
            <li>main.ts - instantiates the Vue instance and allows you to create / inject global functionality such as
              <code>filters</code>, interfaces, and more.
            </li>
            <li>router.ts - defines the router, its routes, and any meta data/restrictions associated with those
              routes.
            </li>
            <li>store.ts - defines the Vuex store - a convenient and powerful shared state management pattern</li>
            <li>other/config files - such as <code>shims</code> files - allow you to augment the typings / capabilities
              of Vue by importing other libraries.
            </li>
          </ol>
        </div>
      </div>
      <div>
        <b>NOTE</b> that if you are using a <b>Git Bash</b> terminal on Windows, the <code>vue create &lt;project-name&gt;</code>
        command's interactive menu system will not work. Instead, you will need to use the <code>winpty vue.cmd create
        &lt;project-name&gt;</code>
        command.
      </div>
    </section-component>
    <section-component>
      <template slot="title">Vue File Layout</template>
      <template slot="header">The basic setup for Vue files. Each .vue file contains:
        <ul>
          <li>A <code>&lt;template&gt;</code> tag for the layout containing Vue and Html components</li>
          <li>A <code>&lt;script&gt;</code> tag for Typescript code for your component's class</li>
          <li>A <code>&lt;style&gt;</code> tag for CSS (or preprocessor languages like SASS/LESS)</li>
        </ul>
      </template>
      <h5>Code for the HelloWorld.vue component:</h5>
      <code-snippet :code='layoutCode'></code-snippet>
      <h5>Code to implement the component in a parent template:</h5>
      <code-snippet :code='componentCode'></code-snippet>
      <h5>Resulting HelloWorld Component:</h5>
      <hello-world msg="Hello World Message"></hello-world>
    </section-component>
    <section-component>
      <template slot="title">Component Features</template>
      <template slot="header">Vue Components have many tools that help make them reusable and cohesive units</template>
      <ul class="spaced-list">
        <li>
          <b>Data:</b> Variables usable within the scope of a component<br><br>
          <code-snippet :code="clickerCode"></code-snippet>
          <br><br>
          <clicker></clicker>
        </li>
        <li>
          <b>Prop:</b> Variables or values that can be passed from the parent<br><br>
          <code-snippet :code="shortHelloWorld"></code-snippet>
          <br><br>
          <code-snippet :code='componentCode'></code-snippet>
          <br>
          <hello-world msg="Hello World Message"></hello-world>
        </li>
        <li>
          <b>Methods:</b> Functions defined in the component to manipulate data<br><br>
          <code-snippet :code="fontSizeCode"></code-snippet>
          <br><br>
          <font-size></font-size>
        </li>
        <li>
          <b>Computed:</b> Getter function that computes a value after detecting a change in whatever properties are
          used within the function body<br><br>
          <code-snippet :code="reverseTextCode"></code-snippet>
          <br><br>
          <reverse-text></reverse-text>
        </li>
        <li>
          <b>Watchers:</b> Function that is triggered when a "watched" variable changes values<br><br>
          <code-snippet :code="watcherCode"></code-snippet>
          <br>
          <watcher></watcher>
        </li>
      </ul>
    </section-component>
    <section-component>
      <template slot="title">Router</template>
      <template slot="header">Vue apps are often Single-page applications*. This means the application is rewritten dynamically
        from the client, rather than loading entirely new pages. The Vue router is in charge of determining what to
        render.
      </template>
      <h6>*Vue apps can be server-side rendered, however most often they are used to bundle an app with webpack, then run the app on the client-side.</h6>
      <h5>Routes are defined in router.ts. Generally, routes point to Vue components defined in the Views folder.</h5>
      <code-snippet :code="routerCode"></code-snippet>
      <h5>A &lt;router-link&gt; controls which route should show with the <code>to</code> attribute, similar to an &lt;a&gt; tag with the <code>href</code> attribute. The &lt;router-view&gt;
        displays the selected route.</h5>
      <code-snippet :code="routerViewCode"></code-snippet>
      <h5>Result</h5>
      <div id='nav'>
        <router-link to='/'>Home</router-link>
        |
        <router-link to='/about'>About</router-link>
      </div>
      <router-view/>
      <h5>When changing a route, the URL will reflect the path that is defined for that route in the router.ts file</h5>
    </section-component>
    <section-component>
      <template slot="title">List Rendering</template>
      <template slot="header">Arrays of items can be rendered in lists. This is done using the <code>v-for</code>
        attribute, which duplicates the component and all nested components for each item in the array
      </template>
      <h5>Given the following data:</h5>
      <code-snippet :code="listRenderData"></code-snippet>
      <h5>Using the following code:</h5>
      <code-snippet :code="listRenderCode"></code-snippet>
      <br><br>
      <list-rendering :list="listToRender"></list-rendering>
    </section-component>
    <section-component>
      <template slot="title">Conditional Rendering</template>
      <template slot="header">Items can be conditionally rendered using the <code>v-if</code> and <code>v-show</code>
        directives. Both will show the element if the directive evaluates to true, or will hide it if the directive
        evaluates to false. <br><br>The difference is that <code>v-show</code> will add <code>display: none;</code> to
        the element, but keep the element in the DOM, while <code>v-if</code> will completely remove the
        element:<br><br>
        <div class="two-columns">
          <div class="item"><img src="@/assets/conditionalimg.png"></div>
          <div class="item">
            <ol style="margin-top: 0">
              <li>v-if = true</li>
              <li>v-if = false</li>
              <li>v-show = true</li>
              <li>v-show = false</li>
            </ol>
          </div>
        </div>
        Generally speaking, <code>v-if</code> has higher toggle costs while <code>v-show</code> has higher initial
        render costs. So prefer <code>v-show</code> if you need to toggle something very often, and prefer
        <code>v-if</code> if the condition is unlikely to change at runtime.
        <br><br>
        <div>
          You can also use <code>else</code> clauses with <code>v-if</code> using the following syntax: <br>
          <code>v-if="condition1"</code>, <code>v-else-if="condition2"</code>, and <code>v-else</code>. There 
          are no else clause equivalents with <code>v-show</code>, so often <code>v-if</code> gets used because 
          an else clause is necessary.
        </div>
      </template>
      <h5>Example Code:</h5>
      <code-snippet :code="conditionalRenderCode"></code-snippet>
      <h5>Result:</h5>
      <conditional-rendering></conditional-rendering>
    </section-component>
    <section-component>
      <template slot="title">Lifecycle Hooks</template>
      <template slot="header">Vue provides access to certain events allowing you to execute code at specific times
        throughout a component's lifecycle.
      </template>
      <div class="two-columns">
        <div class="item"><code>beforeCreate()</code></div>
        <div class="item">
          Events and lifecycle are initialized, but reactivity is not. You may not have access to all of the
          data/functions at this point.
        </div>
      </div>
      <br/>
      <div class="two-columns">
        <div class="item"><code>created()</code></div>
        <div class="item">
          At this point you have access to all functions and data inside of the Vue component. <br/>
          It is common to make API calls to fetch data or do any other pre-rendering data manipulation at this point.
        </div>
      </div>
      <br/>
      <div class="two-columns">
        <div class="item"><code>beforeMount()</code></div>
        <div class="item">Called immediately before the <code>render</code> function is called for the first time.</div>
      </div>
      <br/>
      <div class="two-columns">
        <div class="item"><code>mounted()</code></div>
        <div class="item">At this point, the DOM has loaded and you have access to it - so if you need to get a specific
          HTML element for any reason, now is the time to do so. Note, however, that this does not mean that all <i>child</i> elements have been mounted.
          In situations where you specifically need to wait for all child components to render, you should use <code>Vue.nextTick()</code>.
        </div>
      </div>
      <br/>

      <div class="two-columns">
        <div class="item"><code>beforeUpdate()</code></div>
        <div class="item">Data has changed, but the DOM has not yet been updated. If you need to access the <i>existing</i> DOM before rendering an update (maybe to remove
          a manually added event listener) you would do it here.
        </div>
      </div>
      <br/>
      <div class="two-columns">
        <div class="item"><code>updated()</code></div>
        <div class="item">Data has changed, and the DOM has already updated. Note - if you need to react to data changes, this is not the place to do it. It's better to use 
          a <code>computed</code> property or a <code>watcher</code> in those situations.
        </div>
      </div>
      <br/>

      <div class="two-columns">
        <div class="item"><code>beforeDestroy()</code></div>
        <div class="item">At this point, Vue will clean up/tear down Watchers, child components, etc. If you have any
          manual cleanup to do, this is the time to do it.
          For example, if you're building a SPA where you've set up a <code>setInterval()</code> function, you'll need
          to run <code>clearInterval(intervalID)</code>
          at this point.
        </div>
      </div>
      <br/>
      <div class="two-columns">
        <div class="item"><code>destroyed()</code></div>
        <div class="item">The component and all child components have been destroyed. </div>
      </div>
    </section-component>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import CodeSnippet from '@/components/CodeSnippet.vue';
import SectionComponent from '@/components/SectionComponent.vue';
import HelloWorld from '@/components/HelloWorld.vue';
import Clicker from '@/components/Clicker.vue';
import FontSize from '@/components/FontSize.vue';
import ReverseText from '@/components/ReverseText.vue';
import Watcher from '@/components/Watcher.vue';
import ListRendering from '@/components/ListRendering.vue';
import ConditionalRendering from '@/components/ConditionalRendering.vue';

@Component({
  components: {
    ConditionalRendering,
    ListRendering, Watcher, ReverseText, FontSize, Clicker, SectionComponent, CodeSnippet, HelloWorld
  }
})
export default class App extends Vue {
  private layoutCode = `<template>\n    <div class='hello'>\n       <h1>{{ msg }}</h1>\n    </div>\n</template>\n\n\n\n<script lang="ts">\nimport { Component, Prop, Vue } from 'vue-property-decorator';\n\n@Component({})\nexport default class HelloWorld extends Vue {\n   @Prop()\n   private msg!: string;\n}\n<\/script>\n\n\n\n<style scoped lang="scss">\nh1 {\n    background-color: green;\n    color: white;\n}\n</style>`;
  private componentCode = `<template>\n  <hello-world msg="Hello World Message"></hello-world>\n</template>`;
  private clickerCode = `<template>\n    <div>\n        <button @click="firstCounter++">You clicked me {{firstCounter}} times</button>\n        <button @click="secondCounter++">You clicked me {{secondCounter}} times</button>\n    </div>\n</template>\n\nexport default class Clicker extends Vue {\n    private firstCounter: number = 0;\n    private secondCounter: number = 0;\n}`;
  private shortHelloWorld = `<template>\n    <div class='hello'>\n       <h1>{{ msg }}</h1>\n    </div>\n</template>\n\n\nexport default class HelloWorld extends Vue {\n   @Prop()\n   private msg!: string;\n}`;
  private fontSizeCode = `<template>\n  <div>\n    <div :style="{ fontSize: fontSizePx + 'px' }">font size: {{fontSizePx}}px</div>\n    <button @click="increaseFontSize">Increase font size</button>\n    <button @click="fontSizePx = 10">Reset</button>\n  </div>\n</template>\n\n\nexport default class FontSize extends Vue {\n  private fontSizePx = 10;\n\n  private increaseFontSize() {\n    const fontIncrease = Math.floor(this.fontSizePx * 0.1);\n    this.fontSizePx += fontIncrease;\n  }\n}`;
  private reverseTextCode = `<template>\n  <div>\n    <input v-model="message">\n    <p>Message: {{message}}</p>\n    <p>Reverse: {{reverseMessage}}</p>\n  </div>\n</template>\n\nexport default class ReverseText extends Vue {\n  private message: string = '';\n  \n  private get reverseMessage(): string {\n    return this.message.split('').reverse().join('');\n  }\n}`;
  private watcherCode = `<template>\n  <div>\n    <p>\n      Ask a question:\n      <input v-model="message">\n    </p>\n    <button :disabled="disabled">Submit</button>\n    <div v-show="disabled">Typing...</div>\n  </div>\n</template>\n\n\nimport {debounce} from 'lodash';\n\nexport default class Watcher extends Vue {\n  private message: string = '';\n  private disabled: boolean = false;\n  private debouncedGetAnswer: any;\n  \n  private created() {\n    this.debouncedGetAnswer = debounce(() => this.disabled = false, 500);\n  }\n  \n  @Watch('message')\n    private onQuestionChange(newValue: string, oldValue: string) {\n    this.disabled = true;\n    this.debouncedGetAnswer();\n  }\n}`;
  private routerCode = `import Vue from 'vue';\nimport Router from 'vue-router';\nimport Home from './views/Home.vue';\n\nVue.use(Router);\n\nexport default new Router({\n  mode: 'history',\n  base: process.env.BASE_URL,\n  routes: [\n    {\n      path: '/',\n      name: 'home',\n      component: Home,\n    },\n    {\n      path: '/about',\n      name: 'about',\n      component: () => import('./views/About.vue'),\n    },\n  ],\n});`;
  private routerViewCode = `<div id='nav'>\n  <router-link to='/'>Home</router-link>\n  |\n  <router-link to='/about'>About</router-link>\n</div>\n<router-view/>`;
  private listToRender = [{id: 1, name: 'Johnny', grade: 88}, {id: 2, name: 'Billy', grade: 69}, {
    id: 3,
    name: 'Bobby',
    grade: 97
  }];
  private listRenderCode = `<template>\n  <div>\n    <table>\n      <thead>\n        <tr>\n          <th @click="fieldToSort = 'id'">Id</th>\n          <th @click="fieldToSort = 'name'">Name</th>\n          <th @click="fieldToSort = 'grade'">Grade</th>\n        </tr>\n      </thead>\n      <tbody>\n        <tr v-for="item in listItems">\n          <td>{{ item.id }}</td>\n          <td>{{ item.name }}</td>\n          <td>{{ item.grade }}</td>\n        </tr>\n      </tbody>\n    </table>\n  </div>\n</template>\n\nexport default class ListRendering extends Vue {\n  @Prop()\n  private list!: any[];\n  private fieldToSort = 'id';\n  \n  private get listItems() {\n    return this.list.slice().sort((a, b) => {\n      return a[this.fieldToSort].toString().localeCompare(b[this.fieldToSort].toString());\n    });\n  }\n}`;
  private listRenderData = `[\n   {\n      "id":1,\n      "name":"Johnny",\n      "grade":88\n   },\n   {\n      "id":2,\n      "name":"Billy",\n      "grade":69\n   },\n   {\n      "id":3,\n      "name":"Bobby",\n      "grade":97\n   }\n]`;
  private conditionalRenderCode = `<template>\n  <div class="conditional-rendering">\n    <div>\n      <div v-if="isRendered">Rendered</div>\n      <button @click="isRendered = !isRendered">Toggle Rendered</button>\n    </div>\n    <div>\n      <div v-show="isShown">Shown</div>\n      <button @click="isShown = !isShown">Toggle Shown</button>\n    </div>\n    <div>\n      <div v-if="multipleConditionsValue === 0">First Condition</div>\n      <div v-else-if="multipleConditionsValue === 1">Second Condition</div>\n      <div v-else>Third Condition</div>\n      <button @click="multipleConditionsValue = (multipleConditionsValue + 1) % 3">Toggle Condition</button>\n    </div>\n  </div>\n</template>\n\nexport default class ConditionalRendering extends Vue {\n  private isRendered: boolean = true;\n  private isShown: boolean = true;\n  private multipleConditionsValue: number = 0;\n}`;
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Open+Sans:300,400,700');

#app {
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 800px;
  margin: 32px auto 128px;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.two-columns {
  display: flex;

  .item {
    flex: 1;
  }
}

code {
  background-color: #eff0f1;
  padding: 0 8px;
}

.spaced-list {
  li {
    padding-top: 12px;
    padding-bottom: 24px;
    border-bottom: 1px solid #2c3e50;

    &:last-child {
      border-bottom: none;
    }
  }
}
</style>