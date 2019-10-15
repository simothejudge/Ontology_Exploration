# Pizza-Ontology #

## Inconsistencies ##

Found two inconsistencies related to IceCream and CheesyVegetableTopping: 
   #### 1) IceCream 
   The class can have a fruit topping, but the domain for the property "hasTopping" is only Pizza. One solution can be to generalize the property, stating that IceCream is a subclass of: (hasIngredient some FruitTopping). The domain and the range for the property "hasIngredient" are both Food.
   #### 2) CheesyVegetableTopping 
   The class can include all those vegetables which are stuffed with some cheese, or any kind of creamy cheese with veggies inside. Therefore, it makes sense not to get rid of it, but to find a solution to include it in our Ontology. By simply delete the disjoint statement between VegetableTopping and CheeseTopping we can easily overcome the problem of inconsistency. 

## Redundancies ##

#### - NamedPizza: 
the definition of NamedPizza is redundant, it only groups pizzas based on the unique names, but there is no specific definition for those pizzas. NamedPizza has the same definition of Pizza which is (hasBase some PizzaBase). The class doesn’t really add anything to the ontology, therefore we can get rid of it.

#### - RealItalianPizza: 
In the comment it is specified that RealItalianPizza have only thin and crispy base. We don’t need to specify the statement hasBase only ThinAndCrispyBase for this class, if we simply leverage on the definition of ThinAndCrispyPizza: this class specifies this statement already. 
So RealItalianPizza is equal to: Pizza and (hasCountryOfOrigin value Italy) and it is subclass of: ThinAndCrispyPizza
With this statement it will be inferred that Real Italian Pizzas must have thin and crispy base.

#### - SpicyTopping and SpicyPizza: 
SpicyPizza and SpicyPizzaEquivalent are equivalent class,and we don’t need both of them. SpicyPizza specifies hasTopping some SpicyTopping, so it uses the definition of SpicyTopping, while SpicyPizzaEquivalent define a spicy pizza as something that hasSpiciness some Hot (doesn’t leverage on the SpicyTopping class). If we consider SpicyTopping as redundant class, we can get rid of SpicyPizza class as well. Every topping belonging to SpicyTopping class specifies already that it (hasSpiciness some Hot), so it becomes a subclass of SpicyTopping from inference. But every topping having this property doesn’t need to belong to a SpicyTopping class specifying again the same property. There is no need of grouping the spicy toppings under a specific class, because it wouldn’t add any information to the ontology. Of course, by getting rid of SpicyTopping class, we would also get rid of the SpicyPizza class, leaving the SpicyPizzaEquivalent class to include all those pizza whose spiciness is hot. 
Another solution would be just to delete the statement (haveSpiciness some Hot) for every hot ingredient, and just specify that it is a subclass of SpicyTopping. If we do so, we can get rid of SpicyPizzaEquivalent and keep SpicyPizza instead.

#### - VegetarianPizza:
The class is redundant with respect to VegetarianPizza1. It specifies that vegetarian pizza is whatever has no SeafoodTopping or MeatTopping. But it doesn’t specify that the pizza has any topping at all. Since we have a class of VegetarianTopping, we can use that to define what is a VegetarianPizza by saying that a vegetarian pizza is whatever pizza has a vegetarian topping. Since we have a definition of what is VegetarianTopping, we can use that to define VegetarianPizza as pizzas with any and only VegetarianTopping. So following this logic, we can exclude VegetarianPizza class, and keep VegetarianPizza1 as the right definition of a vegetarian pizza.

#### - VegetarianPizza2:
If we keep the definition of VegetarianTopping (consider that the class SpicyTopping would be deleted, so every non-meat&seafood topping would belong to the class VegetarianTopping), then we don’t need VegetarianPizza2 class, cause it would be redundant with respect to VegetarianPizza1. Notice: NonVegetarianPizza is defined as Pizza and(not(VegetarianPizza)), so we should actually define NonVegetarianPizza without using the definition of VegetarianPiazza. 
NonVegetarianPizza is equivalent to: Pizza and ((hasTopping some MeatTopping) or (hasTopping some SeafoodTopping))

#### - Unclosed Pizza:
Unclosed Pizza class cannot be inferred to be either a vegetarian or non vegetarian. We can't really infere anything from this class, also it is not easy to understand what kind of pizza we are talking about: an open pizza, so whatever is not a calzone?From the statements we can only know that it can have MozzarellaTopping among others, and that it is a Pizza. This class is redundant, because there is nothing that we can put on a pizza that can be different from vegetarian topping and non vegetarian topping at the same time. Wherever it doesn't contain meat or seafood, it goes under vegetarian pizza, otherwise it is not vegetarian. Therefore we don't need such class.

#### - Subclasses of VegetarianTopping:
All the (inferred) subclasses of VegetarianTopping (CheeseTopping, FruitTopping, HerbSpiceTopping, NutTopping, SauceTopping, VegetableTopping) are stated to be subclasses of PizzaTopping. If we declare that they are simply subclasses of VegetarianTopping, there is no need to specify that they are also subclasses of PizzaTopping, as VegetarianTopping has already that property.

#### - TomatoTopping: 
The class TomatoTopping is a sub class of: (hasSpiciness some Mild). This property is specified also for both the subclasses of TomatoTopping (SlicedTomatoTopping and SundriedTomatoTopping). This statement for the two subclasses is clearly redundant, because the two classes would inherit that property from the TomatoTopping parent. 

#### - Caprina Toppings: 
In the subclass of this class, it is specified that CaprinaPizza has SundriedTomatoTopping. It is also specified that it has some TomatoTopping, but this statement is redundant, because SundriedTomatoTopping is a subclass of TomatoTopping, so there is no need to declare that it has a generic tomato topping if we specify that it has sundried tomato topping. We also need to change the first statement to: hasTopping only (GoatsCheeseTopping or MozzarellaTopping or SundriedTomatoTopping).
NOTICE: this is true if Caprina has only dried tomatoes on top, BUT, if the pizza has both sundried tomatos and normal tomatos, then we need to keep both the statement.

#### - Giardiniera Toppings: 
Same logic is applicable for the Giardiniera tomatoes topping. If the Giardiniera has only sliced tomatoes on top, we can simplify the statements, otherwise we keep them as they are. This is something that only pizza experts could help us solve!

#### - hasTopping and isToppingOf property:
The two properties present the following characteristics: hasTopping is inverse functional, while isToppingOf is functional. These two characteristics are redundant. Two different pizzas can have the same topping and still be considered different (there are also other toppings on the pizzas, or the pizza base is different); additionally, a particular topping can be the topping of two different pizzas without them being the same pizza. 

#### - hasBase and isBaseOf property:
The property hasBase is defined as functional and inverse functional. It means that the relation between a particular pizza and its base should be 1 to 1. This is true if we only consider the two available base types that we have right now. However, bases can be of different types of flour (wholemeal, corn flour, wheat flour). If we take into account this bases, then the relation 1 to 1 doens't hold anymore and we need to get rid of these two characteristics. The same logic applies to isBaseOg property.


## Additional Redundancies created ##
Notice that the statements were added to the "cleaned" ontology: firstly, the redundancies found were deleted and then some different, additional statements were added as new redundancies. For every redundant statement, a comment was made to explain why the statement is considered redundant.

