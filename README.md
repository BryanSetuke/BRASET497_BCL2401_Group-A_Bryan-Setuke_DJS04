# [DJS04 Project] Book Connect - Web Components

## Overview
Book Connect is a web application designed to help users browse and discover books. Initially developed as part of the DJS03 project, this iteration focuses on transforming key functionalities into reusable Web Components, enhancing the modularity and maintainability of the application.

## Objectives
- **Convert Book Preview to Web Component**: Encapsulate the book preview feature into a self-contained Web Component.
- **Assess Other Components**: Identify other elements within the application that could benefit from being converted into Web Components.
- **Maintain Functionality**: Ensure that the application retains all its current functionalities after refactoring.

## Features
- Browse and search for books by title, author, and genre.
- View detailed information about each book.
- Dynamically load more books as you scroll.
- Toggle between light and dark themes.

## Web Components
### BookPreview Component
Encapsulates the book preview functionality into a reusable Web Component.

```javascript
class BookPreview extends HTMLElement {
    constructor() {
        super();
        this.attachShadow({ mode: "open" });
    }

    connectedCallback() {
        this.render();
    }

    static get observedAttributes() {
        return ["author", "title", "image"];
    }

    attributeChangedCallback(name, oldValue, newValue) {
        this.render();
    }

    render() {
        const author = this.getAttribute("author");
        const title = this.getAttribute("title");
        const image = this.getAttribute("image");

        this.shadowRoot.innerHTML = `
            <style>
                .preview {
                    border-width: 0;
                    width: 100%;
                    font-family: Roboto, sans-serif;
                    padding: 0.5rem 1rem;
                    display: flex;
                    align-items: center;
                    cursor: pointer;
                    text-align: left;
                    border-radius: 8px;
                    border: 1px solid rgba(var(--color-dark), 0.15);
                    background: rgba(var(--color-light), 1);
                }
                
                @media (min-width: 60rem) {
                    .preview {
                        padding: 1rem;
                    }
                }
                
                .preview_hidden {
                    display: none;
                }
                
                .preview:hover {
                    background: rgba(var(--color-blue), 0.05);
                }
                
                .preview__image {
                    width: 48px;
                    height: 70px;
                    object-fit: cover;
                    background: grey;
                    border-radius: 2px;
                    box-shadow: 0px 2px 1px -1px rgba(0, 0, 0, 0.2),
                        0px 1px 1px 0px rgba(0, 0, 0, 0.1), 0px 1px 3px 0px rgba(0, 0, 0, 0.1);
                }
                
                .preview__info {
                    padding: 1rem;
                }
                
                .preview__title {
                    margin: 0 0 0.5rem;
                    font-weight: bold;
                    display: -webkit-box;
                    -webkit-line-clamp: 2;
                    -webkit-box-orient: vertical;  
                    overflow: hidden;
                    color: rgba(var(--color-dark), 0.8)
                }
                
                .preview__author {
                    color: rgba(var(--color-dark), 0.4);
                }
            </style>
            <button class="preview" data-preview="${this.getAttribute("id")}">
                <img class="preview__image" src="${image}" />
                <div class="preview__info">
                    <h3 class="preview__title">${title}</h3>
                    <div class="preview__author">${author}</div>
                </div>
            </button>
        `;
    }
}

customElements.define("book-preview", BookPreview);
```

## Struggles
### Learning Curve
One of the major challenges was understanding and implementing Web Components from scratch. The concept of shadow DOM, custom elements, and encapsulation was new and required a lot of practice to get right.

### Maintaining Functionality
Ensuring that all existing functionalities were preserved during the transition to Web Components was another hurdle. It involved a lot of testing and debugging to make sure that the new components integrated seamlessly with the existing codebase.

### CSS Encapsulation
Dealing with CSS encapsulation in shadow DOM was tricky. Styles in the shadow DOM are isolated, which is great for preventing style leaks, but it also means you need to manage styles separately for each component.

### Performance Considerations
Optimizing the performance of dynamically created components was another important aspect. It required careful handling of the DOM to ensure that the application remained responsive and efficient.

## Lessons Learned
### Deep Understanding of Web Components
This project provided a deep dive into Web Components, teaching me how to create, use, and manage custom elements effectively. The encapsulation provided by shadow DOM is powerful for creating modular and maintainable code.

### Importance of Testing
Thorough testing is crucial when refactoring code, especially when transitioning to a new technology. It ensures that all functionalities work as expected and helps catch any issues early in the development process.

### CSS Management
Managing CSS within the shadow DOM taught me the importance of keeping component styles self-contained and modular. It also highlighted the need for a well-organized style strategy to avoid redundancy and conflicts.

### Performance Optimization
Working with dynamically created components emphasized the need for performance optimization, particularly in managing and updating the DOM efficiently.

## How to Use the Components
### Including BookPreview in HTML
To use the `book-preview` component, simply include it in your HTML file and set the necessary attributes.

```html
<book-preview id="1" author="J.K. Rowling" title="Harry Potter" image="path/to/image.jpg"></book-preview>
```

### Creating BookPreview Programmatically
You can also create and append the `book-preview` component programmatically in JavaScript.

```javascript
const container = document.getElementById("book-container");
const bookPreview = document.createElement("book-preview");
bookPreview.setAttribute("id", "1");
bookPreview.setAttribute("author", "J.K. Rowling");
bookPreview.setAttribute("title", "Harry Potter");
bookPreview.setAttribute("image", "path/to/image.jpg");

container.appendChild(bookPreview);
```

## Conclusion
Converting key functionalities of Book Connect into Web Components has significantly improved the modularity and reusability of the application. This project was a valuable learning experience, reinforcing the importance of modern web development practices and solidifying my understanding of Web Components.

---

Feel free to explore the code and use the components as needed. Contributions and feedback are always welcome!

Happy Coding!

[Bryan Setuke]
```

This README provides an overview of the project, highlights key components and features, shares struggles and lessons learned, and offers guidance on using the new Web Components.
