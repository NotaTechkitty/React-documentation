# Function Tips and Tricks

## Array to Object :

```javascript
const createObjectList = (list = []) => {
  let map = {};
  list.forEach((menu) => {
    map[menu.id] = menu;
  });
  return map;
};
```

## create a tree for nested object ( parent_id based )

```javascript


const createTreeFromList (list, objectList) = {
    let root = [];
    list.forEach((item)=>{
        let rootNode = createNodeFromItemsList();
        rootNode && root.push(rootNode);
    })
    return root
}

// create a children list for each list element

const createNodeFromItemsList = ( node = {}, list) => {
  if (!node.parent_id) {
    return node;
  }
  !list[node.parent_id].children.includes(node) &&
    list[node.parent_id].children.push(node);

  createNodeFromItemsList(root, list[node.parent_id], list);
};

```
