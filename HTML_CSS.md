## Box model
basic technique in CSS 
Margin
Border
Padding
Content
## Seclector
Select element
## Cascade
 algorithm that defines how to combine property values originating from different sources. 
 - user-agent
 -author
## Specificity
greater level of specificity, and therefore CSS will be applied.
- Inline styles
- IDs
- Classes, attributes and pseudo-class
- Elements and pseudo-elements
## Clean code
- clamp function :
```css
.article{
    width: clamp(200px, 50%, 600px)
}

// min, preference, max
```

```css
.article{
    width = 50%
}

@media only screen and (max-Width:600px)
    .article{
        width: 200px
    }
@media only screen and (max-Width:1200px)
    .article{
        width: 800px
    }
```

