# Twig Syntax
template engine for PHP
- Fast
- Secure
- Flexible
## Installation
```twig
composer require "twig/twig:^3.0"
```

## Synopsis
A template contains variables or expressions
- {% ... %} is used to execute statements such as for-loops 动作
- {{ ... }} is the result of an expression 打印一些东西
- {# ... #} comment something 
```twig
<!DOCTYPE html>
<html>
    <head>
        <title>My Webpage</title>
    </head>
    <body>
        <ul id="navigation">
        {% for item in navigation %}
            <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
        {% endfor %}
        </ul>

        <h1>My Webpage</h1>
        {{ a_variable }}
    </body>
</html>
```
集成开发环境 IDE： Visual Studio Code   
  

## Variables

```twig
{{ foo.bar }} //Variables
```
### Global Variables
_self: references the current template name;  引用当前模板名称；

_context: references the current context;  引用当前上下文；

_charset: references the current charset.  引用当前字符集。

### Setting Variables 设置变量
```
{% set foo = 'foo' %}
{% set foo = [1, 2] %}
{% set foo = {'foo': 'bar'} %}
```

## Filters
变量可以通过过滤器进行修改。过滤器通过管道符号 (|) 与变量隔开。
```twig
{{ name|striptags|title }} // removes all HTML tags from the name and title-cases
```
```twig
{{ list|join(', ') }} //
接受参数的过滤器在参数周围有括号。此示例通过逗号连接列表的元素
```
```twig
{% apply upper %}
    This text becomes uppercase
{% endapply %}
//要对一段代码应用过滤器，请使用 apply 标记对其进行包装
```

## Functions
```twig
{% for i in range(0, 3) %}
    {{ i }},
{% endfor %}
```

## Named Arguments 命名参数
```twig
{% for i in range(low=1, high=10, step=2) %}
    {{ i }},
{% endfor %}
```

## Control Structure
```
{% if users|length > 0 %}
    <ul>
        {% for user in users %}
            <li>{{ user.username|e }}</li>
        {% endfor %}
    </ul>
{% endif %}
```
## Template Inheritance
```
<!DOCTYPE html>
<html>
    <head>
        {% block head %}
            <link rel="stylesheet" href="style.css"/>
            <title>{% block title %}{% endblock %} - My Webpage</title>
        {% endblock %}
    </head>
    <body>
        <div id="content">{% block content %}{% endblock %}</div>
        <div id="footer">
            {% block footer %}
                &copy; Copyright 2011 by <a href="http://domain.invalid/">you</a>.
            {% endblock %}
        </div>
    </body>
</html>
```

## Comparisons
```
{% if 'Fabien' starts with 'F' %}
{% endif %}

{% if 'Fabien' ends with 'n' %}
{% endif %}
```

## Containment Operator
```
{% if 1 not in [1, 2, 3] %}
```

## Test Operator
```
{{ name is odd }}
```

## Other Operators
|: Applies a filter.  

..: Creates a sequence based on the operand before and after the operator
```
{{ 1..5 }}
```
~: Converts all operands into strings and concatenates them. {{ "Hello
" ~ name ~ "!" }} would return (assuming name is 'John') Hello
John!.
., []: Gets an attribute of a variable.
?:: The ternary operator:
```
{{ foo ? 'yes' : 'no' }}
{{ foo ?: 'no' }} is the same as {{ foo ? foo : 'no' }}
{{ foo ? 'yes' }} is the same as {{ foo ? 'yes' : '' }}
```

??: The null-coalescing operator:

{# returns the value of foo if it is defined and not null, 'no' otherwise #}
```
{{ foo ?? 'no' }}
```
## Tags
### embed 嵌入
Embed 标签结合了 Include 和 Extends 的行为。它允许您包含另一个模板的内容，就像 Include 一样。但它也允许您覆盖包含的模板中定义的任何块，例如扩展模板。
将嵌入式模板视为“微布局骨架”。
```twig
{% embed "teasers_skeleton.twig" %}
    {# These blocks are defined in "teasers_skeleton.twig" #}
    {# and we override them right here:                    #}
    {% block left_teaser %}
        Some content for the left teaser box
    {% endblock %}
    {% block right_teaser %}
        Some content for the right teaser box
    {% endblock %}
{% endembed %}
```


Frage:
1. Muss ich erste Twig installieren? Drupal
2. Wir benutzen Drupal8(twig1) oder 9(twig2)? 9
3. #40 wie Vue? Daten wurden von Backend kommen?
4. implementation: Wo kommt getBar, isBar, hasBar? Sind sie PHP?  

    <https://twig.symfony.com/doc/3.x/templates.html>
    ![Alt-Text](twig-image/implementation.png)
5.  sort ist nach Alphabate sortiert
    ![Alt-Text](twig-image/sort.png)
6. tailwind.config.js  

    remCalc(4) bedeutet ?  

    ![Alt-Text](twig-image/remCalc.png)
7. Was bedeutet is-active und megalayer-active?
    ![Alt-Text](twig-image/plugin.png)
8. Wo kann man margin-bottom lesen?
    ![Alt-Text](twig-image wie
9. {# Template #}  Template?  

    {# Defaults #}    
    {% set attributes = attributes|default(create_attribute()) %}  //module  

    {# Classes #}  :class 动态样式

    {% set meta={} %}  
     <Script>
        data() {
        return {
            meta:{
                
            }
            }
        }
    </Script>
------------------------------------------
{% include 'footer.html' %}
wie Vue Component  
include wie import {} from ' '
```
<script>
import ButtonCounter from './ButtonCounter.vue'

export default {
  components: {
    ButtonCounter
  }
}
</script>

<template>
  <ButtonCounter />
</template>
```
10. teaser #19: wo kommt 'basic-teaser group',
11. @apply ich benutze die Tempelate  
    @layer selber style definieren
12. only funktion    
 ![Alt-Text](twig-image/only.png)
包含模板时，它可以访问包含模板中可用的所有变量。如果出于某种原因您不希望这样做，请使用only关键字。

当我需要它时，我没有遇到过这种情况，但除了性能之外，可能还有其他原因。例如，您可以在某些情况下使用它来避免命名冲突。
Frage: 
1. Drupal.md #15 welche sprache?
2. Welche Funktion ist das .jsx Datei? React 