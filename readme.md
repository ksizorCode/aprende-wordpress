# Aprende Wordpress





## Plantilla tipica

| codigo                | que hace                                                  |
|-----------------------|-----------------------------------------------------------|
| ```get_header();```   | inserta el fragmento de código de la cabecera del HTML    |
| ```get_footer();```   | inserta el fragmento de código de la cabecera del HTML    |
| ```get_sidebar();```  | inserta el fragmento de código para el sidebar            |




### get_header


```
<?php
if ( is_home() ) :
	get_header( 'home' );   // → carga header-home.php
elseif ( is_404() ) :
	get_header( '404' );    // → carga header-404.php
else :
	get_header();           // → carga header.php (la cabecera por defecto)
endif;
?>

```


### IS y Classes
```<article id="post-<?php the_ID(); ?>" <?php post_class('single-post'); ?>>```



## Plantillas Single
Las que sólo muestran un articulo, post, apartado o elemento


Dentro de el bucle (The loop):

# 📊 Tabla comparativa de funciones en el Loop de WordPress

| Información              | Imprime directamente (`the_...`) | Devuelve valor (`get_the_...`) |
|--------------------------|----------------------------------|--------------------------------|
| **Título**               | `the_title()`                   | `get_the_title()`              |
| **Contenido**            | `the_content()`                 | `get_the_content()`            |
| **Extracto**             | `the_excerpt()`                 | `get_the_excerpt()`            |
| **Enlace permanente**    | `the_permalink()`               | `get_the_permalink()`          |
| **Imagen destacada**     | `the_post_thumbnail()`          | `get_the_post_thumbnail()`     |
| **Categorías**           | `the_category()`                | `get_the_category()`           |
| **Etiquetas**            | `the_tags()`                    | `get_the_tags()`               |
| **Autor**                | `the_author()`                  | `get_the_author()`             |
| **Meta del autor**       | `the_author_meta()`             | `get_the_author_meta()`        |
| **Fecha de publicación** | `the_date()`                    | `get_the_date()`               |
| **Hora de publicación**  | `the_time()`                    | `get_the_time()`               |
| **Fecha modificada**     | `the_modified_date()`           | `get_the_modified_date()`      |
| **Hora modificada**      | `the_modified_time()`           | `get_the_modified_time()`      |
| **ID del post**          | `the_ID()`                      | `get_the_ID()`                 |
| **GUID** (enlace único)  | `the_guid()`                    | *(no existe, usar `get_post()->guid`)* |


## ✅ Diferencias entre función the y get_the...
|Función                | ¿Devuelve o muetra?       | ¿Requiere ``ècho```?      | Contexto de uso ideal     |
|-----------------------|---------------------------|-------------------------- |---------------------------|
|```the_title()```      | Muestra el título         | ❌ Ya hace ```echo```     | Dentro del Loop           |
|```get_the_title()```  | Devuelve el título        | ✅ Necesita ```echo```    | Dentro del Loop           |

```php
<?php>
if(have_posts()):  // Si tiene posts
    while (have_posts()): the_post();
    the_title(); //Muestrame el titulo directamente
        
    $titulo = get_the_title();
    if($titulo=="Puxarra"){     // Si el título es Puxarra escribirá "Mecagonmimaquina!!!"
        echo "Mecagonmimaquina!!!";
    }

    echo '<h1 id="titulo_'.$titulo.'">'.$titulo.'</h1>';  //<h1>

    endwhile;
endif;
?>

<h3>Otros articulos:</h3>

<?php
$post_id = 123;
echo get_the_title($post_id);
?>


```



### Funciones de apoyo
has_post_thumbnail() → verifica si tiene imagen destacada.
get_the_title() → devuelve el título (en vez de imprimirlo).
get_the_content() → devuelve el contenido.
get_the_excerpt() → devuelve el extracto.
get_the_permalink() → devuelve la URL.
get_the_category() → devuelve las categorías como array.
get_the_tags() → devuelve las etiquetas como array.



```php
<?php if ( have_posts() ) : ?>
    <?php while ( have_posts() ) : the_post(); ?>
        <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
        <?php the_post_thumbnail(); ?>
        <p><?php the_excerpt(); ?></p>
        <p>Publicado por <?php the_author(); ?> el <?php the_date(); ?></p>
    <?php endwhile; ?>
<?php endif; ?>
```

## Plantillas archive
Muestran un listado de elementos a modo de indide de contenidos







## Otras funciones interesantes y Tips



```php
$titulo = 'Hola Mundo, esto es un titulo con Ñ y acentos á';
satitize_title($titulo); 
// hola-mundo-esto-es-un-titulo-con-n-y-acentos-a
```


get_post_field();
Obtiene cualquier campo de un post.
$title = get_post_field('post_title',$post_id);
$slug = get_post_field('post_name, $post_id');


wp_trim_words
$excerpt = wp_trim_words(get_the_content(),20,'…');




get_template_part()
//incluye fragmentos de plantilla reutilizables
get_template_part('partical/content','single'); // carga: partials/content-single.php


get_post_meta();
//obtiene campos personalizados (CF - Custom Fields)
$valor = get_post_meta($post_id, 'mi_campo', true);


add_action / add_filter


# Condiciones para saber donde estás
is_page()
is_sinble()
is_home()
is_front_page()

# Thumbnail
has_post_thumbnail()
get_the_post_thumbnail()


# Muestra un menú de wodpress previamente registrado
wp_nav_menu();
wp_nav_menu(array('theme_location'=>'menu-principal'));




Evita XSS al imprimir datos

esc_html()
esc_attr()
wp_kses()


#URLs limpias
query_vars

register_post_types() // Custom Post Types

register_taxonomy() // categorías personalizadas

add_shortcodes()    // shortcodes


## iAs
- DeepSeek
- Google Firebase studio
- Github Copilot
- Chatbot arena
- Copilot
- Gemini Gems


ATS Sistema de selecicón automatica Slashmobility "aplica ATS a mi CV para esta oferta"