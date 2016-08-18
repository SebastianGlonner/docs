# Basics
- Set base font size, line-height and margin e.g. :

> Source: http://csswizardry.com/ (form one of his talks at a conference, I dont remember)

```
html {
     font-size: 16px;
     line-height: 24px; /* this becomes your base spacing unit */
}

h1, h2, h3, h4, h5, h6, hgroup,
ul, ol, dl,
blockquote, p, address,
table, fieldset,
figure, pre {
     margin: 0px;
     margin-bottom: 24px;
}

/* Now you have a fine, consistent base */
```

# Single Responsibility

> http://drewbarontini.com/articles/single-responsibility/

- Separating classes by its responsibility
- If we got a **.sidebar {...}** and a **.btn {...}**. If we want the button to live inside
the sidebar in a special way we use *context* classes which modifies the styling of our elements appropriately e.g. :
- **.sidebar__btn {}** to modify the button inside the sidebar
- **.has-sidebar__btn {}** to modify the sidebar if the button lives inside the bar

# Injecting Widgets
- Consider setting ``blockquote {all:initial;}`` to reset styles (http://www.brucelawson.co.uk/2014/css-all-initial-to-prevent-widgets-inheriting-css-from-a-host-page/)
