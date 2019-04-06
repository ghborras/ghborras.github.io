---
layout: post
title: Yaml file to Array
---

*{{ page.date | date: "%B %e, %Y" }}*


File to convert to string

~~~
#app/config/file.yml

    item1:
        prop1: xxxxxx
        prop2: xxxxxx
        prop3: xxxxxx
    item2:
        prop1: xxxxxx
        prop2: xxxxxx
        prop4: 
            sub-item1:
                prop1: xxxxxx
                prop2: xxxxxx
                prop3: xxxxxx
            sub-item2:
                prop1: xxxxxx
                prop2: xxxxxx
                prop3: xxxxxx
~~~

MenuExtension.php

~~~
#AppBundle/Twig/MenuExtension.php

    namespace AppBundle\Twig ;

    use Twig\Extension\AbstractExtension ;
    use Twig\TwigFunction ;
    use Symfony\Component\Yaml\Yaml;

    class MenuExtension extends AbstractExtension
    {
        public function getFunctions ()
        {
            return [
                new TwigFunction ( 'myFunction' , [ $this , 'ymlToArray' ]),
            ];
        }

        public function ymlToArray ()
        {
        return Yaml::parseFile('../app/config/file.yml');

        }
    }
~~~

services.yml

~~~
    .....

    AppBundle\Twig\:
        resource: '../../src/AppBundle/Twig'
        public: true

~~~

yourview.html.twig

    set variable = myFunction() 


[close]({{ site.baseurl }}/)
