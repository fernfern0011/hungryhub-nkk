## 🧞 How to setup the project

Run the two following commands accordingly

| Command       | Action                                      |
| :------------ | :------------------------------------------ |
| `npm install` | Installs dependencies                       |
| `npm run dev` | Starts local dev server at `localhost:4321` |

## 🚀 Implementation Approach and Decisions made

```
1. BaseLayout.astro is a reusable page template that takes in BaseHead.astro and wrapped all the files in pages folder
2. The components that need logic will be written in Vue. There are 3 Vue files in this project; HamburgerMenu, ItemCard and LoginForm

Decisions made
1. I have created 'styles' folder to organize css files to follow best practices
2. At first I had a separate Filter.vue in which I intended to pass the selectedSort value to ItemCard.vue. However, I couldn't find a way to do so. Thus, I combined them into one file (ItemCard.vue)
3. Login Page works as intended for demonstration purpose (accept 'standard_user' as the username and 'secret_sauce' as the password). Thus, I didn't implement the session for this assessment.
4. Inventory Page is only able to display the item list based on the sort selected. 'Add to cart' button has no function.
```
