# Generate Dynamic Website Menus with Strapi

In this article, we'll explore how to create a dynamic website menu by leveraging *Strapi*, an open-source, Node.js based, headless CMS. Strapi is a fantastic platform for developing APIs quickly, which is perfect for feeding data to your website's front end. We'll walk through building a menu similar to Strapi's own, featuring drop-downs, headings, links, and buttons.

<img width="1603" alt="Screenshot 2023-12-10 at 3 11 37 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/ab4814e7-172b-4f58-9c05-4ff84c66fdb9">

## Setup

<img width="1606" alt="Screenshot 2023-12-10 at 3 14 02 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/0fa53ce3-029e-4f1c-884c-9810a73edf6b">

To begin, **please ensure that you have a fresh Strapi v4 project up and running**. We're going to create sections first, these will each form part of the large drop-down in the menu above. We will then create individual links and buttons.

## Creating Sections as Collection Types in Strapi

<img width="1613" alt="Screenshot 2023-12-10 at 3 14 44 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/dc903f4b-01d3-4028-92cd-3a9afa082c2e">

Navigate to the "Collection Types" in Strapi Admin and create a new one. Let's call it `Section`. In each section, we'll need a heading (the title to appear at the top) and a `Links` component (to be created shortly) encapsulating all the links inside the section.

<img width="1613" alt="Screenshot 2023-12-10 at 3 15 48 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/743d4c75-0406-40cc-969d-32b4ad18dba0">

While still creating the `Section`, add a component and name it `Link`. Create a category to place this component in, the category name does not matter. The component will be created as a repeatable component and should contain a `name` for the link and a `URL` for its destination.

<img width="1610" alt="Screenshot 2023-12-10 at 3 18 08 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/d23861ad-1a16-44cb-ac76-6fc50a29b9f1">

Additionally, we're going to add two fields: a `text (long)` type for description and an `icon`, which is an image (single-type media).

Hit `Save`. You can now go ahead and create several sections under the newly created `Section` collection by creating a section and adding links to it.

<img width="1612" alt="Screenshot 2023-12-10 at 3 19 36 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/f575e4e9-9e33-4d33-9c1e-0b0525585925">

## Creating Additional Components

Now that we have created a `Section` with internally nested `Link` components, let's create *menu links*, *buttons*, and *drop downs*. Menu links are straightforward additions for the top bar, buttons add interactivity, and dropdown menus improve organization by allowing us to group links based on themes or content.

### Creating the Dropdown Component

A dropdown menu houses multiple sections. In the Components area of Strapi’s admin, create a new component, name it `Dropdown`, and place it under the `Menu` category. Add a `title` field and a `Relation` field linked to `Sections`. Set the relation as 'has many sections', which means a dropdown can contain multiple sections.

<img width="1612" alt="Screenshot 2023-12-10 at 3 32 27 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/80bcdfb8-21ca-4386-85f7-15ebcdeb2a96">

### Creating the Menu Link Component

Next, let's create menu links. Call this component `Menu Link`, and place it under the `Menu` category. Add `title` and `URL` fields to store the link's name and destination.

<img width="1616" alt="Screenshot 2023-12-10 at 3 20 55 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/600851df-f1e8-4296-9445-c73cb342ac9a">

### Creating the Button Component

Finally, we'll create buttons for actions such as 'Sign Up', 'Contact Us', etc. Name this component `Button`, place it under the `Menu` category, and add a `title` and `URL`.

Additionally, let’s add an enumeration field, `Type`. This field hosts classes to style the button on the front end. For instance, we can have a `Primary` or `Secondary` class, which alters the button's look.

<img width="1610" alt="Screenshot 2023-12-10 at 3 21 53 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/781e317b-ba72-4f55-8860-589f577ccf18">

## Constructing the Menu

Now that we have all the building blocks in place, let's construct the menu.

Create a new single type called `Main Menu`. Inside it, add a Dynamic Zone named `Main Menu Items`. Add the components–`Dropdown`, `Menu Link`, and `Button` to this zone.

<img width="1609" alt="Screenshot 2023-12-10 at 3 33 02 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/8ae7c582-db64-49e6-bd1d-c69b89741d85">

In the content manager, you can add all three types of components to the Main Menu Items Dynamic Zone.

The Dropdown can be given a title (like 'Product') and sections (like 'Product' and 'Features'). You can add multiple dropdowns, each with a title and related sections.

<img width="1599" alt="Screenshot 2023-12-10 at 3 33 47 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/e7ba0f45-6b7a-400f-9afa-ef17d2f35bd5">

For Menu Links, you can add links like 'Docs' and 'Pricing' with their corresponding URLs.

<img width="1598" alt="Screenshot 2023-12-10 at 3 35 42 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/8b24c2e3-2366-4de3-9850-254a2ea9e975">

For the Button, you can create a button like 'Contact Sales' and provide a URL for it. Make sure to assign a class (`Primary` or `Secondary`) to it.

<img width="1601" alt="Screenshot 2023-12-10 at 3 34 42 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/c0732551-970f-41e5-b514-6078ee5ed296">

After adding all the sections, links, and buttons, save and publish your menu.

## Generating the JSON Data for Front End Access

Once you have published your menu, you need to ensure that the data is accessible on the front end.

Navigate to `Settings` -&gt; `Roles & Permissions` -&gt; `Public User`, and allow `Find` for `Main Menu` and `Sections`. Save the settings.

<img width="1601" alt="Screenshot 2023-12-10 at 3 36 27 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/77909273-ce74-4a2b-b7c1-d81180d6f106">

You can then access the menu configuration by making a get request to: `https://localhost:1337/api/main-menu?populate[0]=MainMenultems&populate[1]=MainMenultems.sections&populate[2]=MainMenultems.sections.links`

The data is returned in JSON format, which can be used to populate the content of your menu on the front end.

<img width="1609" alt="Screenshot 2023-12-10 at 3 37 19 PM" src="https://github.com/BraydenGirard/strapi-build-a-menu/assets/3247657/e0940f37-f071-4caf-aaae-e1b5a42aff3d">

That’s it! By using Strapi, we've created a flexible system for building out a menu dynamically. This is one of many powerful features Strapi provides and is a testament to its capabilities as one of the rising stars in the CMS space.
