# polymerNote
    记录我的polymer学习之旅，总结遇到的问题；



## 1.对polymer的基本认识
    更多信息参照官网： https://www.polymer-project.org/3.0/docs/devguide/feature-overview
1.1 polymer的概念
    Polymer是一个用于构建封闭，可复用web组件的的框架，构建的web组件可以像标准html元素一样工作，唯一的区别在于使用之前，需要引入组件的定义；

1.2 如何使用
(1) 注册自定义组件
```
    import {PolymerElement} from '@polymer/polymer/polymer-element.js';

    // Define the class for a new element called custom-element
    class CustomElement extends PolymerElement {
      constructor() {
        super();
        this.textContent = 'I\'m a custom-element.';
      }
    }
    // Register the new element with the browser
    customElements.define('custom-element', CustomElement);
```

(2)Add shadow DOM
    为组件添加dom节点来实现组件的UI展示和行为；Polymer提供了模版来为自定义组件添加dom树；
```
    import {PolymerElement, html} from '@polymer/polymer/polymer-element.js'

    // Define the class for a new element called custom-element
    class DomElement extends PolymerElement {

      static get template () {
        return html`
          <p>I'm a DOM element. This is my shadow DOM!</p>

          <!-- TODO: Try adding some other html elements inside the
               template. For example, add <h1>A heading!</h1> or
               <a href="stuff.html">A link!</a>
          -->
        `;
      }
    }
    // Register the new element with the browser
    customElements.define('dom-element', DomElement);
```

(3) Compose with shadow DOM
组件的组合，类似与react中的（children）子元素；
```
    import {PolymerElement, html} from "@polymer/polymer/polymer-element.js"

    class PictureFrame extends PolymerElement {
      static get template() {
        return html`
        <!-- scoped CSS for this element -->
        <style>
          div {
            display: inline-block;
            background-color: #ccc;
            border-radius: 8px;
            padding: 4px;
          }
        </style>
        <div>
          <!-- any children are rendered here -->
          <slot></slot>
        </div>
        `;
      }
    }
    customElements.define('picture-frame', PictureFrame);

    <picture-frame>
      <img src="https://www.polymer-project.org/images/logos/p-logo-32.png">
    </picture-frame>
```

(4) Use data binding
    数据绑定，dom模版通过类似mustache的语法绑定元素的实例属性；
```
import {PolymerElement, html} from "@polymer/polymer/polymer-element.js"

class NameTag extends PolymerElement {
  constructor() {
    super();

    /* set this element's owner property */
    this.owner = 'Daniel';
  }
  static get template() {
    return html`
      <!-- bind to the "owner" property -->
      This is <b>{{owner}}</b>'s name-tag element.
    `;
  }
}
customElements.define('name-tag', NameTag);
```

(5) Declare a property
声明组件的属性；属性是组件非常重要的一个公有api;

```
import {PolymerElement, html} from '@polymer/polymer/polymer-element.js'

class ConfigurableNameTag extends PolymerElement {
  static get properties () {
    return {
      // Configure owner property
      owner: {
        type: String,
          value: 'Daniel',
      }
    };
  }
  static get template () {
    return html`
      <!-- bind to the "owner" property -->
      This is <b>[[owner]]</b>'s name-tag element.
    `;
  }
}
customElements.define('configurable-name-tag', ConfigurableNameTag);

<configurable-name-tag owner="Scott"></configurable-name-tag>
```


(6) Bind to a property
    属性不仅能绑定文本内容，还可以绑定属性值；
```
    import {PolymerElement, html} from '@polymer/polymer/polymer-element.js';
    import '@polymer/iron-input/iron-input.js';

    class EditableNameTag extends PolymerElement {
      static get properties () {
        return {
          owner: {
            type: String,
            value: 'Daniel'
          }
        };
      }
      static get template () {
        return html`
          <!-- bind to the 'owner' property -->
          <p>This is <b>[[owner]]</b>'s name-tag element.</p>

          <!-- iron-input exposes a two-way bindable input value -->
          <iron-input bind-value="{{owner}}">
            <input is="iron-input" placeholder="Your name here...">
          </iron-input>
        `;
      }
    }

    customElements.define('editable-name-tag', EditableNameTag);
```




(7) Using

## 构建组件



## 构建应用
