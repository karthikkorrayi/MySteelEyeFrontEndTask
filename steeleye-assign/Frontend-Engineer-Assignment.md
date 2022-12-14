# React Component Code Review

## Introduction

Based on the code below answer the following queries:
1. Explain what the simple `List` component does.

In React, Generally a component that makes it easier to recognize where things changed or added or been taken away. Lists can be created in a regular JavaScript in which this component is independent and reusable bit of code. This is the kind of same purpose as JavaScript functions as it works in isolation. We can extract to standalone component that only care about its concerns.

2. What problems / warnings are there with code?

By looking at the give code that how it generating a list with React, On fulfilling this, where we will traverse the column element using column element using map() code and its neighbour surround modifications in square brackets. The parts and components are involved in which then assigned to ListItems and finally, it displays this list on the Web by putting it among the ul> and /ul> components.

3. Please fix, optimize, and/or modify the component as much as you think is necessary.

Inorder to build lists of pieces, it must be use the character and the characteristic "key" as specified in the React documentation. To determine whether items in the list which has already been modified or added or destroyed, The React needs so many keys. Here, an individual identifier is required for each object and the ID about on entity can usually works nicely for all of React's components list creation work.
Whenever making lists of components in JavaScript, user must use a special word attribute called "key", where that React uses keys to indicate whether additional burdens have been modified or removed or altered or to put it in an another way, were the designers may say that keywords are applied to identify the components in collections.
Coming to my modification part, I added an arrow function to Onclickhandler. I changed the syntax from setSelectedIndex from selectedIndex and its vice-verse from const and I added marks in the ItemList to check and added a key function and return with === operator to check the items removed from the function for an array and changed some mistakes in WrappedListcomponent

##  Code

```javascript

import React, { useState, useEffect, memo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
  index,
  isSelected,
  onClickHandler,
  text,
}) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [selectedIndex, setSelectedIndex] = useState();

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = index => {
    setSelectedIndex(index);
  };

  return (
    <ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          key={item.id}
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={selectedIndex === index}
        />
      ))}
    </ul>
  )
};

WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};

WrappedListComponent.defaultProps = {
  items: null,
};

const List = memo(WrappedListComponent);

export default List;

//root file
import{appendFile} from "fs";
import React from "react";
import List from "./";
const App=()=>{
  const.items=[
    {id:1, text:"one"},
    {id:2, text:"two"},
    {id:3, text:"three"},
    {id:4, text:"four"},
    {id:5, text:"five"}
  ];
  return(
    <div className="App">
    <List items={items}/>
    </div>
  );
};
exportdefault App;
```
