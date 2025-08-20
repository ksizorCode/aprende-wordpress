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