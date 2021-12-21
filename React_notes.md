# Notes
## Common mistakes
import properly
## Clean code
### Define frequent variables :
Instead of 

```javascript
if (layout === 'vertical'){...}
...
layout === 'vertical' ? vertical : horizontal
...
layout !== 'vertical'
...

```

Use this

```javaScript
const isVertical = layout === 'vertical'

if ( isVertical ){...}

isVertical ? vertical : horizontal

!isVertical

```