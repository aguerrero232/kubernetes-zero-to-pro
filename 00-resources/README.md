# <img src="img/k8s.png" width="30px"> **Kubernetes** - ***Section 0:*** `Resources` 🗃️

## ***Table*** *of* ***`Contents`*** 📜

* 🏠 [**home**](https://github.com/aguerrero232/kubernetes-zero-to-pro/blob/main/README.md)
* 🗃️ **resources**
  * 🖼️ [**images**](img/)
  * 📝 [**markdown blueprints**](md-samples/)
  * 📁 [**pdfs**](pdfs/)
    * 👩🏽‍🏫 [**udemy course pdfs**](pdfs/udemy-course/)
    * 📖 [**kubernetes up and running book**](pdfs/kubernetes-up-and-running.pdf)
  * 🔗 **links**:
    * 🎓 [***certified kubernetes application developer test***](https://www.cncf.io/certification/ckad/)
    * 💪 [**exercises for CKAD**](https://github.com/dgkanatsios/CKAD-exercises)
    * 🙇🏻‍♀️ [**study materials for CKAD**](https://github.com/lucassha/CKAD-resources)
    * 🤔 [***kubernetes concepts***](https://kubernetes.io/docs/concepts/)
    * 📓 [***candidate handbook***](https://www.cncf.io/certification/candidate-handbook)
    * 💡 [***exam tips***](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)

<br />

## **Description** 👀

Resources for the `Kubernetes` ***Zero to Pro Guide***. Has images, pdfs, and links to other resources.

<br />

## **Helpful** `Content` 📌

## ***Nano*** 📝

`Nano` is a *text editor* that is installed by default on most Linux distributions. It is a simple text editor that is easy to use and has a lot of features. During the `CKAD` exam, you will be **asked to edit a file using Nano or Vim**.

* 🗎 [***nano documentation***](https://www.nano-editor.org/)

### ***Initial `Setup`*** 🛠️

* `nano` config file, ***~/.nanorc***

    ```bash
    set tabsize 4
    set tabstospaces
    ```

  * `tabsize` - sets the number of spaces that a tab will be replaced with

  * `tabstospaces` - replaces tabs with spaces

  * if ***~/.nanorc*** *does not exist*, **create** it

      ```shell
      touch ~/.nanorc
      ```

<br>

### ***Keyboard `Shortcuts`*** ⌨️

<!-- Ctrl\+[A-z0-9]{1,} -->
<!-- Alt\+[A-z0-9]{1,} -->

* **editing**
  * `Ctrl+K`    Cut current line into cutbuffer
  * `Alt+6` Copy current line into cutbuffer
  * `Ctrl+U` Paste contents of cutbuffer
  * `Alt+T` Cut until end of buffer
  * `Ctrl+]` Complete current word
  * `Alt+3` Comment/uncomment line/region
  * `Alt+U` Undo last action
  * `Alt+E` Redo last undone action

* **search** *and* **replace**
  * `Ctrl+Q`    Start backward search
  * `Ctrl+W` Start forward search
  * `Alt+Q` Find next occurrence backward
  * `Alt+W` Find next occurrence forward
  * `Alt+R` Start a replacing session

* **deletion**
  * `Ctrl+H` Delete character before cursor
  * `Ctrl+D` Delete character under cursor
  * `Alt+Bsp` Delete word to the left
  * `Ctrl+Del`    Delete word to the right
  * `Alt+Del` Delete current line

* **moving around**
  * `Ctrl+B`    One character backward
  * `Ctrl+F` One character forward
  * `Ctrl+← `One word backward
  * `Ctrl+→ `One word forward
  * `Ctrl+A` To start of line
  * `Ctrl+E` To end of line
  * `Ctrl+P` One line up
  * `Ctrl+N` One line down
  * `Ctrl+↑ `To previous block
  * `Ctrl+↓ `To next block
  * `Ctrl+Y` One page up
  * `Ctrl+V` One page down
  * `Alt+\` To top of buffer
  * `Alt+/ `To end of buffer

<br>

## ***YAML***  <img src="img/yaml.png" width="29px">

`YAML` is a ***human-readable data serialization language***. It is commonly used for *configuration files* and in applications where data is being stored or transmitted. `YAML` is stored in **key value pairs** and can be used to serialize data structures such as *maps, sequences, and scalars*.

### `YAML` **Syntax**

* `YAML` is case sensitive
* Comments are created using the # symbol

<br>

### **Examples** 🧩

* key value pairs

  ```yaml
  Fruit: Apple
  Vegetable: Carrot
  Liquid: Water
  Meat: Chicken
  ```

* arrays / lists

  ```yaml
  Fruits:
    - Orange
    - Apple
    - Banana

  Vegetables:
    - Carrot 
    - Cauliflower
    - Tomato
  ```

* dictionary / map

  ```yaml
  Banana:
      Calories: 105
      Fat: 0.4g
      Carbs: 27g

  Grapes:
      Calories: 62
      Fat: 0.3g
      Carbs: 16g
  ```

* key value / dictonary / lists

  ```yaml
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

***Notice the alignment, this is important in yaml.***

* You can *either* set a value or a list/dictonary/map but *not both*

* `Dictionaries` are an *unordered collection* while `lists` are *ordered*
