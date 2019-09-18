---
layout: post
title: Using Stripe with React
image: img/callum-shaw-555357-unsplash.jpg
author: Pranay Aryal
date: 2019-08-10T10:00:00.000Z
tags:
  - React
---

I am going to be using React's functional components here

1. Import Stripe.js into your `index.html` file 
```html
<script src="https://js.stripe.com/v3/"></script>
```
2. Install `react-stripe-elements`
```bash
npm install --save react-stripe-elements
```
3. Create a component that will inject stripe like this. This will create a form with a button
```javascript
    import React from 'react';
    import { CardElement, injectStripe } from 'react-stripe-elements'

    const InjectedCardElement = props => {

        return (
            <div>
                <CardElement className="stripe-card" style={{base: {fontSize: '18px'}}}/>
                <button className="pay-with-stripe-button">Pay with credit card</button>
            </div>
        );
    }

    export default injectStripe(InjectedCardElement);
```
4. Create the main file which will take the injected file like this after importing it. This is where you put your stripe publishable test key
```javascript
    import React from 'react';
    import { StripeProvider, Elements, injectStripe, CardElement } from 'react-stripe-elements';
    import InjectedCardElement from './InjectedCardElement';

    const Card = () => {
        return (
                <div>
                    <br />
                        Test using this card:
                        <span className="cc-number">4242 4242 4242 4242</span>, and enter any 5 digits for the zip code

                        <StripeProvider apiKey="pk_test_j8asdfasdf8sdkjk2kjkjkj0">
                            <Elements>
                                <InjectedCardElement />
                            </Elements>
                        </StripeProvider>
                </div>
        );
    }

    export default Card;
```

5. You can handle your stripe logic in InjectedCardElement.js component given above. 

> 'Props' are available to you automatically.

```javascript
    import React from 'react';
    import { CardElement, injectStripe } from 'react-stripe-elements'

    const InjectedCardElement = props => {

        const handleSubmit = async(ev) => {
            //You automatically get the props
            let { token } = await props.stripe.createToken({ name: 'Name' });
            console.log(token)
        }

        return (
            <div>
                <CardElement className="stripe-card" style={{base: {fontSize: '18px'}}}/>
                <button className="pay-with-stripe-button">Pay with credit card</button>
            </div>
        );
    }

    export default injectStripe(InjectedCardElement);
```

6. Once you get the token, you can send it to your backend to create a charge with that token.
