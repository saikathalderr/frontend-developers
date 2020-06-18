## Love, Bonito VueJs Developer
 
 
If you are here means that you want to work at Love, Bonito. 


During these exercises, we are going to try to understand your Skills. We want to use real case scenarios instead of riddles. 


We are going to [Vue Storefront](https://www.vuestorefront.io/), this is a Headless solution for Magento, but today we are only going to focus on your Frontend Skills, so don't worry about Magento. 

[Architecture of VueStoreFront Application
](https://medium.com/the-vue-storefront-journal/vue-storefront-how-to-install-and-integrate-with-magento2-227767dd65b2)

![](https://miro.medium.com/max/1400/1*S5vdUEw-sb5Anl6K9LO1DQ.png)


### Before you start 

1. Create a fork of this repository, it's important that you don't do Merge Request to this repository, you will do it over your fork

2. Every Challenge should be 1 open Merge Request, so when you do the Challenge one you will create a Merge Request to `master` and you will leave it open. At then you will have one open Merge Request per Challenge. If your code depends in other Merge Request you will point the MR to the dependant branch instead of `master`

3.  At then you need to share the link of the repository to pablo.morales@lovebonito.com and aman.agarwal@lovebonito.com and remember to let Celeste knows that you finish


### Extra considerations

* Testing is an important part of our development process. Unit test and functional test are required
* Be sure that your code applies the VueStorefront code style  



### Challenges
-

#### Challenge 1
When we are on an item page and we want to add an item to the cart we don't have a clear way to see what's going on, the `Add to cart` button becomes disable and after a while, we can see a green ugly notification. We need to improve this behavior 

*Acceptance Criteria*

* Add a spinner in the `Add to Cart` button
* Remove the Green Notification
* After the Item is added to the cart leave open the Cart. and change the text of the `Add to Cart` button to `Added`



#### Challenge 2 
It's time for the Micro-interactions

This hamburger menu should have a symbol when is open and another one when is close, and the transition between symbols should be animated, please go creative and use whatever you think will work
git 

*Acceptance Criteria*

* Create a micro-interaction over the hamburger menu


#### Challenge 3

The product page requires some modifications in mobile to increase our conversion rate

*Acceptance Criteria*
* In Mobile make the button `Add to Cart` stick to the footer of the page view
* The number of items you want, should be a drop-down base on the current stock of the Variants selected
* When I click in the button `Add to Cart` without yet select a variant I should notify properly to the user


#### Challenge 4

Lastly, we need to add the colors of products in our PLP, Product Listing Page, in this case, we can use the current Love Bonito catalog to see how this work. 


*Acceptance Criteria*

* Show the Colors of the variants for each product in the catalog

 
