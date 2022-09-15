# YAML

YAML is a human-readable data serialization language. It is commonly used for configuration files and in applications where data is being stored or transmitted. YAML is stored in **key value pairs** and can be used to serialize data structures such as maps, sequences, and scalars.

___

## Examples of yaml


* Key Value Pairs

    ```
        Fruit: Apple
        Vegetable: Carrot
        Liquid: Water
        Meat: Chicken
    ```

* Array/Lists

    ```
        Fruits:
        - Orange
        - Apple
        - Banana

        Vegetables:
        - Carrot 
        - Cauliflower
        - Tomato
    ```

* Dictionary/Map
    
    ```
        Banana:
            Calories: 105
            Fat: 0.4g
            Carbs: 27g

        Grapes:
            Calories: 62
            Fat: 0.3g
            Carbs: 16g
    ```

* Key Value/Dictonary/Lists

    ```
        Fruits:
            - Banana:
                Calories: 105
                Fat: 0.4g
                Carbs: 27g

            - Grapes:
                Calories: 62
                Fat: 0.3g
                Carbs: 16g
    ```


* ***Notice the alignment, this is important in yaml.***

* You can either set a value or a list/dictonary/map but not both

* Dictionaries are an unordered collection while lists are ordered
___


## YAML Syntax

* YAML is case sensitive
* Comments are created using the # symbol

