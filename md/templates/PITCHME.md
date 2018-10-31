---?color=linear-gradient(to right, #c02425, #f0cb35)
@title[Title Card]

@snap[west span-70]
Title Card Content
@snapend

@snap[south-west byline text-white]
Some byline stuff
@snapend

---?image=template/img/bg/black.jpg&position=right&size=50% 100%
@title[Split List]

@snap[west split-screen-heading text-black span-50]

Split List Heading

@snapend

@snap[east text-white span-45]
@ol[split-screen-list](false)
- Lorem ipsum dolor sit amet, consectetur elit
- Ut enim ad minim veniam, quis exercitation
- Duis aute irure dolor in reprehenderit in voluptate
@olend
@snapend

---
@title[Code Walkthrough]

```javascript
import React from 'react';

const Hello = (props) => (
    <div className="hello">
        {props.name}
    </div>
);

export default Hello;
```

@[1](Import React code)
@[3](blah)
@[4-6](some JSX stuff)
@[9](Export!)

---
