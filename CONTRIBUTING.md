# Contribution Guide
If you're reading this you want to contribute to this Mojang API documentation. Good for you! We welcome contributions.

This guide will go over how to contribute and our project structure.

**NOTE:** This guide is incomplete and is a bit rushed. If you have any questions about contributing don't hesitate to make an issue at 88/mojang-api-discussion.

### Project Structure
We use [`mdBook`](https://github.com/rust-lang/mdBook) to create the HTML files we serve to show the documentation. The documentation itself is written in Markdown. 

The `src` folder holds SUMMARY.md, which must be edited if you are adding a new page to the API documentation.

The `book` folder holds the HTML that is built.

The file `TODO.md` holds a list of all pages that need to be worked on still.

### Endpoint Template
Template files for new endpoints are located in `ENDPOINT_TEMPLATE.md`.

### Building new HTML
Make sure you have `mdBook` installed. Click [here](https://github.com/rust-lang/mdBook) to see a guide on installing & using mdBook.

Then, navigate to the folder where you have stored this Git repository and run `mdbook build`.

The output files will be located in the `book` folder.

### What do I do when I'm done with a new update?
Make a pull request. We will merge it or ask for some changes to be made to fit the project structure / add more detail if needed.

### End
Thanks for taking the time to read this and contribute to these docs! Your contributions are very much appreciated.
