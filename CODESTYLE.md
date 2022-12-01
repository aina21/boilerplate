# Ocean.io Development style guide

## Table of Contents

  1. [HTML](#html)

  1. [Styled-components](#styled-components)
  1. [Javascript](#javascript)
  1. [Typescript](#typescript)
  1. [Backend](#backend)
  1. [General](#general)
  1. [General Folder Structure](#general-folder-Structure)

## HTML

- [1.1](#html): use section for creating containers inside of a independent page

```HTML
    // bad
    <div>
        <div></div>
        <div></div>
        <div></div>
    </div>

    // good
    <section>
        <div></div>
        <div></div>
        <div></div>
    </section>
```

- [1.2](#html): For rendering a list always use a unordered or ordered list.

```HTML
    // bad
    <div>
        <div></div>
        <div></div>
        <div></div>
    </div>

    // good
    <ul>
        <li></li>
        <li></li>
        <li></li>
    </ul>
```

- [1.3](#html): use figure if you want to contain an image in a block

```HTML
    // bad
    <div>
        <img src={example.png} alt="example">
    </div>

    // good
    <figure>
        <img src={example.png} alt="example">
    </figure>
```

- [1.4](#html): Missing href on links

```HTML
    // bad
        <a onClick={...}>Click Here</a>

    // good
        <a onClick={...} href="#">Click Here</a>
```

- [1.5](#html): Don’t place Block elements within Inline elements: There are some old HTML tags and attributes which have been declared deprecated by W3C consortium. Although modern browsers currently support them, they might not in future. Check out this article that lists almost all of the deprecated elements.

```HTML
    // bad
        <a href="#"><h2>Block inside Inline</h2></a>


    // good
        <h2><a href="#">Inline inside Block</a></h2>

```

- [1.6](#html): If you want to show a list of things in bulleted or numbered order, never use line breaks. Use unordered list \<ul> or ordered list \<ol> tags for this purpose.

```HTML
    // bad
    1. Steve Jobs<br/>
    2. Bill Gates<br/>
    3. Linus Torvalds


    // good
    <ol>
        <li>Steve Jobs</li>
        <li>Bill Gates</li>
        <li>Linus Torvalds</li>
    </ol>
```

- [1.7](#html): If you want to show a list of things in bulleted or numbered order, never use line breaks. Use unordered list \<ul> or ordered list \<ol> tags for this purpose.

```HTML
    // bad
    1. Steve Jobs<br/>
    2. Bill Gates<br/>
    3. Linus Torvalds


    // good
    <ol>
        <li>Steve Jobs</li>
        <li>Bill Gates</li>
        <li>Linus Torvalds</li>
    </ol>
```

- [1.8](#html): Don’t use \<b> and \<i> for bolding and italicizing

```HTML
    // bad
    <b>This is bold but wrong!</b>

    // good
    <strong>This is bold and right!</strong>
```

- [1.9](#html): Don’t use multiple line breaks

```HTML
    // bad
    This is a line
    <br/>
    <br/>
    This is another line.

    // good
    <p>This is a line</p>
    <p>This is another line</p>
```

- [1.10](#html): Avoid Inline Styles and class names and use styled-components

```HTML
    // bad
   <h2 style={{color: red}}>Wrong</h2>
   <h2 className="red">Wrong</h2>

    // good
    <h2>Right</h2>
```

**[⬆ back to top](#table-of-contents)**

## Styled components

- [2.1](#styled-components): Always use color variables

```javaScript
    // bad
    const StyledAccountInfoDiv = styled.div`
      height: 280px;
      border-radius: 4px;
      background-color: white;
    `;

    // good
    const StyledAccountInfoDiv = styled.div`
      height: 280px;
      border-radius: 4px;
      background-color: ${white};
    `;
```

- [2.2](#styled-components): Always use rem Except if you specifically want the component to not scale when scaling font (example: border)

```javaScript
    // bad
    const StyledAccountInfoDiv = styled.div`
      height: 280px;
    `;

    // good
    const StyledAccountInfoDiv = styled.div`
      height: ${rem(280)};
    `;

    // bad
    const StyledAccountInfoDiv = styled.div`
      border: solid red ${rem(1)};
    `;

    // good
    const StyledAccountInfoDiv = styled.div`
      border: solid red 1px;
    `;
```

**[⬆ back to top](#table-of-contents)**

## Javascript

- [3.1](#javascript): Try to not use if and short if in render section

```javaScript
    // bad
    {showHeader ? (
        <h1>
            header
        </h1>
    ) : ''}

    // good
    {showHeader && (
        <h1>
            header
        </h1>
    )}

    // bad
    if(showHeader) {
        return (
            <h1>
                header
            </h1>
        )
    }

    // good
    {showHeader && (
        <h1>
            header
        </h1>
    )}
```

- [3.2](#javascript): Always import methods from library not library itself.

```javaScript
    // bad
    import React, { memo } from 'react';

    export const CompanyElement: React.FC<ICompanyElementProps> = memo(
        props => {}
    );

    // good
    import React, { memo, FC } from 'react';

    export const CompanyElement: FC<ICompanyElementProps> = memo(
        props => {}
    );
```

- [3.3](#javascript): Always wrap you react component inside of memo unless the component is connected to the Mobx.It means you have to make sure you are replacing object references and not modifying them. See https://reactjs.org/docs/shallow-compare.html

```javaScript
    // bad
    export const CompanyElement: FC<ICompanyElementProps> =
        props => {}
    ;

    // good
    export const CompanyElement: FC<ICompanyElementProps> = memo(
        props => {}
    );
```

- [3.4](#javascript): Always use camel case for naming props

```javaScript
    // bad
    <Social test-props="test" />

    // good
    <Social testProps="test />
```

- [3.4](#javascript): Always use camel case for naming props

```javaScript
    // bad
    <Social test-props="test" />

    // good
    <Social testProps="test />
```

**[⬆ back to top](#table-of-contents)**

## Typescript

- [4.1](#typescript): Never use any for defining a type.

```typescript
    // bad
    interface IHeadProps {
        title: any;
    }
  
    // good
    interface IHeadProps {
        title: string;
    }
```

- [4.2](#typescript): Do not define any type for children as a prop

```typescript
    // bad
   interface ICrmSettingSectionProps {
        statusText?: string;
        children?: JSX.Element | JSX.Element[];
    }
  
    // good
    interface ICrmSettingSectionProps {
        statusText?: string;
    }
```

**[⬆ back to top](#table-of-contents)**

## Backend

**[⬆ back to top](#table-of-contents)**

## General

- [1.1](#general): Never use camel case for naming folders and files instead use '-'

```typescript
    // bad
   - app
    - backendDevelopment
    - frontendDevelopment

    // good
    - app
    - backend-development
    - frontend-development
```

- [1.2](#general): Rules of React Hooks

    Hooks are JavaScript functions, but they impose two additional rules:
    Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.
    Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks. We’ll learn about them in a moment.)

- [1.3](#general): pages need to be without any logic and logic needs to be moved inside of components

**[⬆ back to top](#table-of-contents)**

## General folder structure

- app
  - backend
  - frontend

- website
  - backend
  
  - frontend
    - pages
    - src
    - static

- common
  - backend
  - data
  - models
  - styles
  - utils

**[⬆ back to top](#table-of-contents)**