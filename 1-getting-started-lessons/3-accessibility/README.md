# 创建无障碍网页

![All About Accessibility](../../sketchnotes/webdev101-a11y.png)
> 手绘笔记作者 [Tomomi Imura](https://twitter.com/girlie_mac)

## 课前测验
[课前测验](https://ff-quizzes.netlify.app/web/)

> Web 的力量在于其普遍性。无论是否残疾，每个人都能访问是一个重要方面。
>
> \- 蒂姆·伯纳斯-李爵士，W3C 主任和万维网发明者

这句话完美地强调了创建无障碍网站的重要性。一个无法被所有人访问的应用程序从定义上来说就是排他性的。作为 Web 开发者，我们应该始终考虑无障碍性。通过从一开始就关注这一点，您将能够确保每个人都能访问您创建的页面。在这节课中，您将学习可以帮助确保您的 Web 资源具有无障碍性的工具以及如何在考虑无障碍性的前提下进行构建。

> 您可以在 [Microsoft Learn](https://docs.microsoft.com/learn/modules/web-development-101/accessibility/?WT.mc_id=academic-77807-sagibbon) 上学习本课程！

## 使用的工具

### 屏幕阅读器

最著名的无障碍工具之一是屏幕阅读器。

[屏幕阅读器](https://en.wikipedia.org/wiki/Screen_reader)是视力障碍者常用的客户端。当我们花时间确保浏览器正确传达我们希望分享的信息时，我们也必须确保屏幕阅读器也能做到这一点。

最基本的情况下，屏幕阅读器会从上到下有声地朗读页面。如果您的页面全是文本，阅读器将以与浏览器类似的方式传达信息。当然，网页很少是纯文本的；它们会包含链接、图形、颜色和其他视觉组件。必须注意确保屏幕阅读器能够正确地朗读这些信息。

每个 Web 开发者都应该熟悉屏幕阅读器。如上所述，这是您的用户将使用的客户端。就像您熟悉浏览器的工作方式一样，您也应该学习屏幕阅读器的工作方式。幸运的是，大多数操作系统都内置了屏幕阅读器。

一些浏览器还具有内置工具和扩展，可以大声朗读文本或甚至提供一些基本的导航功能，例如[这些以无障碍性为重点的 Edge 浏览器工具](https://support.microsoft.com/help/4000734/microsoft-edge-accessibility-features)。这些也是重要的无障碍工具，但功能与屏幕阅读器大不相同，不应将它们误认为屏幕阅读器测试工具。

✅ 尝试使用屏幕阅读器和浏览器文本阅读器。在 Windows 上默认包含 [Narrator](https://support.microsoft.com/windows/complete-guide-to-narrator-e4397a0d-ef4f-b386-d8ae-c172f109bdb1/?WT.mc_id=academic-77807-sagibbon)，还可以安装 [JAWS](https://webaim.org/articles/jaws/) 和 [NVDA](https://www.nvaccess.org/about-nvda/)。在 macOS 和 iOS 上，默认安装了 [VoiceOver](https://support.apple.com/guide/voiceover/welcome/10)。

### 缩放

另一个视力障碍者常用的工具是缩放。最基本的缩放类型是静态缩放，通过 `Control + 加号 (+)` 或降低屏幕分辨率来控制。这种类型的缩放会导致整个页面调整大小，因此使用[响应式设计](https://developer.mozilla.org/docs/Learn/CSS/CSS_layout/Responsive_Design)对于在增加缩放级别时提供良好的用户体验非常重要。

另一种缩放依赖于专门的软件来放大屏幕的一个区域并平移，就像使用真正的放大镜一样。在 Windows 上，[放大镜](https://support.microsoft.com/windows/use-magnifier-to-make-things-on-the-screen-easier-to-see-414948ba-8b1c-d3bd-8615-0e5e32204198)是内置的，[ZoomText](https://www.freedomscientific.com/training/zoomtext/getting-started/) 是具有更多功能和更大用户群的第三方放大软件。macOS 和 iOS 都有一个名为 [Zoom](https://www.apple.com/accessibility/mac/vision/) 的内置放大软件。

### 对比度检查器

网站上的颜色需要仔细选择，以满足色盲用户或难以看到低对比度颜色的人的需要。

✅ 使用浏览器扩展（例如 [WCAG 的颜色检查器](https://microsoftedge.microsoft.com/addons/detail/wcag-color-contrast-check/idahaggnlnekelhgplklhfpchbfdmkjp?hl=en-US&WT.mc_id=academic-77807-sagibbon)）测试您喜欢使用的网站的颜色使用情况。您学到了什么？

### Lighthouse

在浏览器的开发者工具区域，您会找到 Lighthouse 工具。该工具对于首次查看网站的无障碍性（以及其他分析）非常重要。虽然不完全依赖 Lighthouse 很重要，但 100% 的分数作为基准非常有帮助。

✅ 在浏览器的开发者工具面板中找到 Lighthouse，并对任何网站运行分析。您发现了什么？

## Designing for accessibility

Accessibility is a relatively large topic. To help you out, there are numerous resources available.

- [Accessible U - University of Minnesota](https://accessibility.umn.edu/your-role/web-developers)

While we won't be able to cover every aspect of creating accessible sites, below are some of the core tenets you will want to implement. Designing an accessible page from the start is **always** easier than going back to an existing page to make it accessible.

## Good display principles

### Color safe palettes

People see the world in different ways, and this includes colors. When selecting a color scheme for your site, you should ensure it's accessible to all. One great [tool for generating color palettes is Color Safe](http://colorsafe.co/).

✅ Identify a web site that is very problematic in its use of color. Why?

### Use the correct HTML

With CSS and JavaScript it's possible to make any element look like any type of control. `<span>` could be used to create a `<button>`, and `<b>` could become a hyperlink. While this might be considered easier to style, it conveys nothing to a screen reader. Use the appropriate HTML when creating controls on a page. If you want a hyperlink, use `<a>`. Using the right HTML for the right control is called making use of Semantic HTML.

✅ Go to any web site and see if the designers and developers are using HTML properly. Can you find a button that should be a link? Hint: right click and choose 'View Page Source' in your browser to look at underlying code.

### Create a descriptive heading hierarchy

Screen reader users [rely heavily on headings](https://webaim.org/projects/screenreadersurvey8/#finding) to find information and navigate through a page. Writing descriptive heading content and using semantic heading tags are important for creating an easily navigable site for screen reader users.

### Use good visual clues

CSS offers complete control over the look of any element on a page. You can create text boxes without an outline or hyperlinks without an underline. Unfortunately removing those clues can make it more challenging for someone who depends on them to be able to recognize the type of control.

## The importance of link text

Hyperlinks are core to navigating the web. As a result, ensuring a screen reader can properly read links allows all users to navigate your site.

### Screen readers and links

As you would expect, screen readers read link text in the same way they'd read any other text on the page. With this in mind, the text demonstrated below might feel perfectly acceptable.

> The little penguin, sometimes known as the fairy penguin, is the smallest penguin in the world. [Click here](https://en.wikipedia.org/wiki/Little_penguin) for more information.

> The little penguin, sometimes known as the fairy penguin, is the smallest penguin in the world. Visit https://en.wikipedia.org/wiki/Little_penguin for more information.

> **NOTE** As you're about to read, you should **never** create links which look like the above.

Remember, screen readers are a different interface from browsers with a different set of features.

### The problem with using the URL

Screen readers read the text. If a URL appears in the text, the screen reader will read the URL. Generally speaking, the URL does not convey meaningful information, and can sound annoying. You may have experienced this if your phone has ever audibly read a text message with a URL.

### The problem with "click here"

Screen readers also have the ability to read only the hyperlinks on a page, much in the same way a sighted person would scan a page for links. If the link text is always "click here", all the user will hear is "click here, click here, click here, click here, click here, ..." All links are now indistinguishable from one another.

### Good link text

Good link text briefly describes what's on the other side of the link. In the above example talking about little penguins, the link is to the Wikipedia page about the species. The phrase *little penguins* would make for perfect link text as it makes it clear what someone will learn about if they click the link - little penguins.

> The [little penguin](https://en.wikipedia.org/wiki/Little_penguin), sometimes known as the fairy penguin, is the smallest penguin in the world.

✅ Surf the web for a few minutes to find pages that use obscure linking strategies. Compare them with other, better-linked sites. What do you learn?

#### Search engine notes

As an added bonus for ensuring your site is accessible to all, you'll help search engines navigate your site as well. Search engines use link text to learn the topics of pages. So using good link text helps everyone!

### ARIA

Imagine the following page:

| Product      | Description        | Order        |
| ------------ | ------------------ | ------------ |
| Widget       | [Description]('#') | [Order]('#') |
| Super widget | [Description]('#') | [Order]('#') |

In this example, duplicating the text of description and order make sense for someone using a browser. However, someone using a screen reader would only hear the words *description* and *order* repeated without context.

To support these types of scenarios, HTML supports a set of attributes known as [Accessible Rich Internet Applications (ARIA)](https://developer.mozilla.org/docs/Web/Accessibility/ARIA). These attributes allow you to provide additional information to screen readers.

> **NOTE**: Like many aspects of HTML, browser and screen reader support may vary. However, most mainline clients support ARIA attributes.

You can use `aria-label` to describe the link when the format of the page doesn't allow you to. The description for widget could be set as

``` html
<a href="#" aria-label="Widget description">description</a>
```

✅ In general, using Semantic markup as described above supersedes the use of ARIA, but sometimes there is no semantic equivalent for various HTML widgets. A good example is a Tree. There's no HTML equivalent for a tree, so you identify the generic `<div>` for this element with a proper role and aria values. The [MDN documentation on ARIA](https://developer.mozilla.org/docs/Web/Accessibility/ARIA) contains more useful information.

```html
<h2 id="tree-label">File Viewer</h2>
<div role="tree" aria-labelledby="tree-label">
  <div role="treeitem" aria-expanded="false" tabindex="0">Uploads</div>
</div>
```

## Images

It goes without saying screen readers are unable to automatically read what's in an image. Ensuring images are accessible doesn't take much work - it's what the `alt` attribute is all about. All meaningful images should have an `alt` to describe what they are.
Images that are purely decorative should have their `alt` attribute set to an empty string: `alt=""`. This prevents screen readers from unnecessarily announcing the decorative image.

✅ As you might expect, search engines are also unable to understand what's in an image. They also use alt text. So once again, ensuring your page is accessible provides additional bonuses!

## The keyboard

Some users are unable to use a mouse or trackpad, instead relying on keyboard interactions to tab from one element to the next. It's important for your web site to present your content in logical order so a keyboard user can access each interactive element as they move down a document. If you build your web pages with semantic markup and use CSS to style their visual layout, your site should be keyboard-navigable, but it's important to test this aspect manually. Learn more about [keyboard navigation strategies](https://webaim.org/techniques/keyboard/).

✅ Go to any web site and try to navigate through it using only your keyboard. What works, what doesn't work? Why?

## Summary

A web accessible to some is not a truly 'world-wide web'. The best way to ensure the sites you create are accessible is to incorporate accessibility best practices from the start. While there are extra steps involved, incorporating these skills into your workflow now will mean all pages you create will be accessible.

---

## 🚀 Challenge

Take this HTML and rewrite it to be as accessible as possible, given the strategies you learned.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>
      Example
    </title>
    <link href='../assets/style.css' rel='stylesheet' type='text/css'>
  </head>
  <body>
    <div class="site-header">
      <p class="site-title">Turtle Ipsum</p>
      <p class="site-subtitle">The World's Premier Turtle Fan Club</p>
    </div>
    <div class="main-nav">
      <p class="nav-header">Resources</p>
      <div class="nav-list">
        <p class="nav-item nav-item-bull"><a href="https://www.youtube.com/watch?v=CMNry4PE93Y">"I like turtles"</a></p>
        <p class="nav-item nav-item-bull"><a href="https://en.wikipedia.org/wiki/Turtle">Basic Turtle Info</a></p>
        <p class="nav-item nav-item-bull"><a href="https://en.wikipedia.org/wiki/Turtles_(chocolate)">Chocolate Turtles</a></p>
      </div>
    </div>
    <div class="main-content">
      <div>
        <p class="page-title">Welcome to Turtle Ipsum. 
            <a href="">Click here</a> to learn more.
        </p>
        <p class="article-text">
          Turtle ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
        </p>
      </div>
    </div>
    <div class="footer">
      <div class="footer-section">
        <span class="button">Sign up for turtle news</span>
      </div><div class="footer-section">
        <p class="nav-header footer-title">
          Internal Pages
        </p>
        <div class="nav-list">
          <p class="nav-item nav-item-bull"><a href="../">Index</a></p>
          <p class="nav-item nav-item-bull"><a href="../semantic">Semantic Example</a></p>
        </div>
      </div>
      <p class="footer-copyright">&copy; 2016 Instrument</p>
    </div>
  </body>
</html>
```

## Post-Lecture Quiz
[Post-lecture quiz](https://ff-quizzes.netlify.app/web/en/)

## Review & Self Study

Many governments have laws regarding accessibility requirements. Read up on your home country's accessibility laws. What is covered, and what isn't? An example is [this government web site](https://accessibility.blog.gov.uk/).

## Assignment
 
[Analyze a non-accessible web site](assignment.md)

Credits: [Turtle Ipsum](https://github.com/Instrument/semantic-html-sample) by Instrument
