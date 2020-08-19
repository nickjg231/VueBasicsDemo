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
              missing files cause compilation errors, etc).
            </li>
            <li>assets -</li>
            <li>components -</li>
            <li>views -</li>
            <li>main.ts -</li>
            <li>router.ts -</li>
            <li>store.ts -</li>
            <li>other/config files -</li>
          </ol>
        </div>
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
          <b>Data:</b> Variables usable within the scope of a component
          <code-snippet :code="clickerCode"></code-snippet>
          <clicker></clicker>
        </li>
        <li>
          <b>Prop:</b> Variables or values that can be passed from the parent<br>
          <code-snippet :code="shortHelloWorld"></code-snippet><br><br>
          <code-snippet :code='componentCode'></code-snippet><br>
          <hello-world msg="Hello World Message"></hello-world>
        </li>
        <li>
          <b>Methods:</b> Functions defined in the component to manipulate data<br>
          <code-snippet :code="fontSizeCode"></code-snippet><br><br>
          <font-size></font-size>
        </li>
        <li>
          <b>Computed:</b> Getter function that computes a value after detecting a change in whatever properties are used within the function body<br>
          <reverse-text></reverse-text>
        </li>
        <li>
          <b>Watchers:</b><br>
        </li>
      </ul>
    </section-component>
    <!--    <div id='nav'>-->
    <!--      <router-link to='/'>Home</router-link>-->
    <!--      |-->
    <!--      <router-link to='/about'>About</router-link>-->
    <!--    </div>-->
    <!--    <router-view/>-->
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

@Component({
  components: {ReverseText, FontSize, Clicker, SectionComponent, CodeSnippet, HelloWorld}
})
export default class App extends Vue {
  private layoutCode = `<template>\n    <div class='hello'>\n       <h1>{{ msg }}</h1>\n    </div>\n</template>\n\n\n\n<script lang="ts">\nimport { Component, Prop, Vue } from 'vue-property-decorator';\n\n@Component({})\nexport default class HelloWorld extends Vue {\n   @Prop()\n   private msg!: string;\n}\n<\/script>\n\n\n\n<style scoped lang="scss">\nh1 {\n    background-color: green;\n    color: white;\n}\n</style>`;
  private componentCode = `<template>\n  <hello-world msg="Hello World Message"></hello-world>\n</template>`;
  private clickerCode = `<template>\n    <div>\n        <button @click="firstCounter++">You clicked me {{firstCounter}} times</button>\n        <button @click="secondCounter++">You clicked me {{secondCounter}} times</button>\n    </div>\n</template>\n\nexport default class Clicker extends Vue {\n    private firstCounter: number = 0;\n    private secondCounter: number = 0;\n}`;
  private shortHelloWorld = `<template>\n    <div class='hello'>\n       <h1>{{ msg }}</h1>\n    </div>\n</template>\n\n\nexport default class HelloWorld extends Vue {\n   @Prop()\n   private msg!: string;\n}`;
  private fontSizeCode = `<template>\n  <div>\n    <div :style="{ fontSize: fontSizePx + 'px' }">font size: {{fontSizePx}}px</div>\n    <button @click="increaseFontSize">Increase font size</button>\n    <button @click="fontSizePx = 10">Reset</button>\n  </div>\n</template>\n\n\nexport default class FontSize extends Vue {\n  private fontSizePx = 10;\n\n  private increaseFontSize() {\n    const fontIncrease = Math.floor(this.fontSizePx * 0.1);\n    this.fontSizePx += fontIncrease;\n  }\n}`;
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
  margin: 0 auto;
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
  }
}
</style>