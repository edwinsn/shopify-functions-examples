## Process of creating a custom discount function using Shopify Functions. 

* Creating a new Shopify app, generating a discount function, deploying the function 
* Ensuring the necessary permissions are in place.
* Step-by-Step Guide

Links to documentation:  
  Function result: https://shopify.dev/docs/api/functions/reference/product-discounts/graphql/functionresult
  Function Input: https://shopify.dev/docs/api/functions/reference/product-discounts/graphql/input


1. Create a New Shopify App

First, we need to create a new Shopify app where the discount function will reside.

    Open your terminal.
    Run the following command to create a new Shopify app:

    bash

    npm init @shopify/app@latest

    Follow the prompts to configure your new app.

2. Create a Discount Function

Once your app is created, you need to generate a discount function extension.

    Navigate to your app directory:

    bash

cd your-app-directory

Run the command to generate a new extension:

bash

    npm run shopify app generate extension

    Select "Function" when prompted for the type of extension.
    Follow the prompts to configure your discount function. This will create a new directory for your function within your app.

2.5 Start the project

   npm run dev

3. Develop Your Discount Function

    Navigate to the function directory created by the previous command.
    Open the src/index.js or src/index.ts file (depending on your setup) to start coding your discount logic.

Here's a basic example of a discount function:

javascript

export default (input) => {
  const { discount } = input;

  // Apply a 10% discount
  discount.value = discount.price * 0.10;

  return discount;
};

4. Add the Permission to the Scope

Before deploying, make sure to add the necessary permissions to your app's scope. Open your shopify.app.toml file and ensure the required permissions are included, such as:

toml

[scopes]
functions = "write_discounts"

deploy function config 

   app config use

5. Deploy the Function

Deploy your discount function to Shopify.

    In your terminal, run:

    bash

    npm run deploy

    Follow the prompts to deploy your function.

6. Activate the discount using the graphql app

 ` # query {
  #   shopifyFunctions(first:25){
  #     nodes{
  #     	id
  #     	app {
  #         title
  #       }
  #     apiType
  #     title
  #   	}
  #   }
  # }
  # cadf722f-92f5-49a8-b05e-647d0898be07
  mutation {
    discountAutomaticAppCreate(automaticAppDiscount:{
      title: "No recharge subscription Discount"
      functionId: "cadf722f-92f5-49a8-b05e-647d0898be07"
      startsAt: "2024-03-28T00:00:00"
    }) {
      automaticAppDiscount {
        discountId
      }
      userErrors {
        field
        message
      }
    }
  }`
