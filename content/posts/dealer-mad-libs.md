---
date: 2021-05-21
tags:
- uchicago
title: Making Mad-Libs 
---

We played with an write-your-own-article / Mad-libs format a couple times of times at the [_The Dealer_](https://chicagoshadydealer.com/) this year -- see examples [here](https://chicagoshadydealer.com/index.php/2021/05/10/mad-libs-write-a-thinker-article/) and [here](https://chicagoshadydealer.com/index.php/2020/11/03/candidate-wins-presidency/) -- and it's really nice illustration of basic jQuery functionality. This is a small tutorial of the code behind those articles. Major credits to [R.E.](https://re-stern.com/) for pioneering the form.

A run-of-the-mill input is pretty straight forward in HTML. (In the Dealer's Wordpress backend, you can write HTML using the text tab on the classic editor.) For example:

```html 
In response to tonight’s dramatics, 
<input type="text" placeholder="social network" /> 
has set itself on fire.
``` 
Renders as: 

In response to tonight's dramatics, 
<input type="text" placeholder="social network" /> 
has set itself on fire.

The jQuery comes in when we want multiple inputs to change together. In that case, we need to assign IDs and classes to identical inputs. Take the following example: 

```html 
...it points to the broader persecution of 
<input id="1" class="priv" type="text" placeholder="privileged group" />. 
Why can’t 
<input id="2" class="priv" type="text" placeholder="privileged group" /> ... 
```
Here we want the both inputs to change when either is given an input. Note that using both classes and IDs is useful because you can keep track of both the type of the input (privileged group, noun, verb, ordinal number etc.) with the class, and count occurances with the ID. 

The following jQuery-inflected Javascript binds the values of both inputs together. 

```javascript 
$(document).ready(()=>{ 
  $('.priv#1').change(function() {
    $('.priv#2').val($('.priv#1').val());
  });
  $('.priv#2').change(function() {
    $('.priv#1').val($('.priv#2').val());
   });
});
```
Note the two way binding -- you don't know which input the reader could try and enter first.  

In Wordpress, you can inject your code into the article by inputing a custom field, say with the name CODE, and the code (with appropriate `<script>` and/or `<style>` tags) as a value. Then just call `{{CODE}}` at the end of the article, and you're good to go. 