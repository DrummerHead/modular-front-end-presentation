slide de bill murray "this slide intentionally bill murray"... puede ser, yo que se

titulo, tema, twitter, url de la charla


como es la cosa en el pasado, te preguntan por "un sitio con 4 páginas", puede seguir pasando, cualquier cosa puede pasar, los bancos siguen usando cobol, 

Ejemplos de querer agarrar algo de una pagina y usarlo en otro lado, y cuando lo pones en ese otro lado de repente no anda nada, y entonces bla bla

Related subjects (but not for today)

Una slide puede ser "related subjects", y aca tendría que encajar: web components, bower, (angular, ember, js paterns, etc) cosas que estan relacionadas, que son importantes pero que no son exactamente de lo que voy a hablar

hablar acerca de como no hay un "right way" while discussing bower (pluginism vs too custom, slow app (fat app impression)), la pelicula separation, passion

lo mejor que uno puede hacer es usar buen criterio y documentar las decisiónes que uno tomó


Esta relacionado mas bien al dia a dia de escribir html y css, y no les voy a mostrar ninguna técnica nueva ni les voy a vender ningun framework, sino que vamos a ver como usar lo que ya tenemos para hacer cosas mas mantenibles, intercambiables, etc

primero mostrar interfaces y analizarlas... no no no, primero hablar del tema de que ... voy al ba˜õ; hablar del tema de proceso de diseño de coso, de modular sicodelia... perá


Bien, primero arranquemos hablando del proceso de diseño de una aplicación. No voy a hacer un review de todas las metodologías de trabajo existentes, porque esta fuera del tema, pero simplifiquemos el tema diciendo de que tenemos casos en el que el diseño visual se genera antes de crear la aplicación (icono de pdf  > icono html) y tenemos casos en el que el proceso de diseño es mas organico (icono wireframe > icono brain thinking > icono html > icono diseño, iteración loop loco) [ir slide para atras y mostrar primer caso]

En este caso es muy normal recibir un PDF monolítico por decirlo de alguna forma que muestra varias páginas, y nosotros alegremente nos ponemos a arquitecturear la cosa en base a estas páginas. Podemos por ejemplo recibir algo como esto [[mostrar mock]], ahora, lo que nosotros vamos a hacer, es pedir que también nos manden un archivo detallando cada uno de los componentes del mock anterior, algo como esto [[mostrar el otro coso]], que es una pequeña guia de estilo, mas que nada detallando componentes asociados al mock anterior. Ahora, lo bueno de este archivo, es que le vamos a pedir al diseñador visual (si es que tienne a alguien exclusivamente para el diseño) que vaya aumentando este archivo a medida que diseña nuevas páginas.

Ahora, ustedes pueden pensar "nah, esta todo muy lindo pero si pedimos eso nos dicen que no, o no le da la cabeza", pero el asunto que tenemos que tener en cuenta y recordar es que hay una gran diferencia entre un diseñador y un decorador. Un decorador es alguien que hace que las cosas se vean lindas. Un diseñador razona, analiza el problema (tanto de comunicación o interacción) y encuentra la forma de casar la identidad del producto con la funcionalidad requerida. Como resúmen, el diseñador no es ningún banana, y no lo asumen. Y saben qué, si tienen un diseñador que ustedes consideran que es terrible banana, exiganlo igual, y se pueden sorprender de lo que pueden lograr. O lo pueden despedir también.

Los beneficios de requerir que esto se haga es que ya desde un principio no solo nosotros tenemos una demostración mas explicita de que no es una página sino una serie de componentes, sino que ahora el diseñador también esta pensando en esos términos, e idealmente crea componentes basados en lo que ya existe. Después que tenes un psd lleno de componentes, es mucho mas facil hacer un mock de una página nueva, se convierte en algo natural usarlo.


ahora en el segundo caso [[hint a front-end style guides de lo que voy a ahblar despues]]



Organización de nuestro código



TODO: quedé por acá



About SASS...

No usar selector nesting, directamente no usar


#about {
}

#about {
  h1 {
    font-size: 5em;
  }
}

#about {
  h1 {
    font-size: 5em;
    > span {
      margin-top: .5em;
    }
  }
}

#about {
  h1 {
    font-size: 5em;
    > span {
      margin-top: .5em;
    }
  }
  form#contact {
    .form-group {
      border-top: 1px solid #ccc;
      input[type="text"] {
        font-family: sans-serif;
      }
    }
  }
}



#about h1 {
  font-size: 5em;
}
#about h1 > span {
  margin-top: .5em;
}
#about form#contact .form-group {
  border-top: 1px solid #ccc;
}
#about form#contact .form-group input[type="text"] {
  font-family: sans-serif;
}


Ustedes pueden pensar "pero me estas diciendo que deje de usar algo que fue diseñado para que yo no me tenga que esforzar extra" y el tema es, si estas escribiendo selectores asi de largos, y te das cuenta que es engorroso escribir selectores así de largos, es bueno que sufras. Porque no tendrías que estar escribiendo selectores así de largos.

[[explicar code smell]] y a veces pre-procesadores como sass pueden remover ese code smell que a veces es necesario, porque esto no es CSS mejorado, esto es un pre-procesador. Lo que puede mejorar es tu experiencia escribiendo CSS, pero no necesariamente el output de todo lo que escribiste sea mejor CSS que si lo escribieses directamente.











Ahora, en el segundo caso en el que tenemos primero una arquitectura y después el diseño, podemos hacer algo bastante parecido pero un poco más interactivo, guias de estilo front-end, como por ejemplo la de github
https://github.com/styleguide/css/1.0
o mailchimp
https://ux.mailchimp.com/patterns/grids
o salesforce
http://sfdc-styleguide.herokuapp.com/

Ahora, ustedes las estarán mirando y pensando... hmm... son bastante parecidas a 
http://getbootstrap.com/css/
boostrap, no? O mi favorito foundation
http://foundation.zurb.com/docs/components/grid.html

Esto es porque los dos son guias de estilo. Claro, son estilos muy basicos no definen una identidad específica, esto es porque es nuestro trabajo hacer que estos sistemas sean identificables como algo único y diferencaible. O no, podemos no usar zurb ni bootstrap ni inserte framework name here y hacer nuestro propio framewor, hecho a medida para los problemas especificos que nuestra aplicación tiene.

De hecho zurb foundation nació de una guia de estilo basica que ellos estaban usando como base para clientes nuevos. Y de ahí dijeron "bue, si estamos usando esto para todos los clientes nuevos, y es re util... y lo hacemos open source!"

Es decir, vean que estamos hablando de todo esto antes de tocar código en lo absoluto, porque el tener un front-end modular es algo que parte de una necesidad, de resolver un problema. No es simplemente una particularidad técnica o un framework trendy o algo por el estilo.


Bueno, framework o no framework?


framework
pro 
bueno para equipos grandes con muchas manos
cantidad de cosas ya resueltas, no tener que razonar

cons
mas complejidad
mas kb de descarga


custom
pro
especificamente creado para las necesidades del proyecto
tantos kb como los necesarios y no mas

cons
cierto nivel de reinventar la rueda
mas tiempo de aprendizaje para alguien nuevo



en cualquiera de los dos casos, vamos a tener que pensar en nuestro front-end de forma modular y tener en cuenta estas good practices












por algun lado poner que un buen ejercicio es tratar de hacer tu propio bootstrap, o foundation, {{insert framework name here}}, despues de hacerlo por favor no ponerlo en ningún lado porque ya esta saturado el mercado de opciones y mejor hacer un pull request  que hacer mi propio framework, pero tratar de hacer su propio bootstrap los va a poner en el estado mental correcto para tratar de hacer sistemas modulares. NOTA: capaz esto lo puedo poner mas al final cerca del tema de bem y todo eso.

pero mejor aún como ejercicio y algo que de hecho les puede servir para algo, es hacer una style guide de su front-end (mostrar ejemplos de style guides, quizas un link a una) ya que esto les sirve para el futuro y además en el procesod de crearla vos razonas tu aplicación diferente y seguro vas a encontrar lugares en los que puedas optimizar lo que esta pasando (bla bla)





sicodelia

conclusión


vamos a freeform un cacho. Yo quiero dar una charakkkk`kkkkk


Al final encajar que estaría bueno que vicharan http://smacss.com/ y http://bem.info/


https://github.com/adactio/Pattern-Primer
