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

# Listado de Funciones PHP


| Función | Descripción | Ejemplo |
| --- | --- | ---|
| `echo` | Imprime información en la pantalla | `echo "Hola mundo"` |
| `print_r()` | Imprime información sobre una variable | `print_r($variable)` |
| `is_string()` | Comprueba el valor es un String (texto) | `is_string($texto)` |
| `is_int()` | Comprueba el valor es un Int (numero entero) | `is_int($numero)` |
| `is_float()` | Comprueba el valor es un Float (número) | `is_float($decimal)` |
| `is_array()` | Comprueba el valor es un Array (lista) | `is_array($lista)` |
| `is_bool()` | Comprueba el valor es un Bool (true/false) | `is_bool($booleano)` |
| `htmlspecialchars` | Convierte caracteres especiales en entidades HTML | `htmlspecialchars($texto)` |
| `str_replace` | Reemplaza una cadena por otra | `str_replace($cadena_a_reemplazar, $cadena_de_reemplazo, $texto)` |



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









----


# 🚀 Guía de Desarrollo PHP para WordPress

## 📋 Índice
1. [Estructura básica de plantillas](#estructura-básica-de-plantillas)
2. [Funciones de plantilla principales](#funciones-de-plantilla-principales)
3. [The Loop - El bucle de WordPress](#the-loop---el-bucle-de-wordpress)
4. [Plantillas Single](#plantillas-single)
5. [Plantillas Archive](#plantillas-archive)
6. [Funciones condicionales](#funciones-condicionales)
7. [Funciones de utilidad](#funciones-de-utilidad)
8. [Seguridad y buenas prácticas](#seguridad-y-buenas-prácticas)
9. [Custom Post Types y Taxonomías](#custom-post-types-y-taxonomías)

---

## 🏗️ Estructura básica de plantillas

### Funciones fundamentales de inclusión

| Función | Descripción | Archivo que carga |
|---------|-------------|-------------------|
| `get_header()` | Inserta la cabecera del HTML | `header.php` |
| `get_footer()` | Inserta el pie de página | `footer.php` |
| `get_sidebar()` | Inserta la barra lateral | `sidebar.php` |

### Uso avanzado de get_header()

```php
<?php
// Cargar diferentes cabeceras según el contexto
if (is_home()) :
    get_header('home');     // → carga header-home.php
elseif (is_404()) :
    get_header('404');      // → carga header-404.php
elseif (is_page('contacto')) :
    get_header('contact');  // → carga header-contact.php
else :
    get_header();           // → carga header.php (por defecto)
endif;
?>
```

### Clases dinámicas en artículos

```php
<!-- Añade clases automáticas y personalizadas al artículo -->
<article id="post-<?php the_ID(); ?>" <?php post_class('mi-clase-personalizada'); ?>>
    <!-- Contenido del artículo -->
</article>
```

---

## 🔧 Funciones de plantilla principales

### Comparativa: Funciones `the_` vs `get_the_`

| Información | Imprime directamente | Devuelve valor | Notas |
|-------------|---------------------|----------------|-------|
| **Título** | `the_title()` | `get_the_title()` | |
| **Contenido** | `the_content()` | `get_the_content()` | |
| **Extracto** | `the_excerpt()` | `get_the_excerpt()` | |
| **URL** | `the_permalink()` | `get_the_permalink()` | |
| **Imagen destacada** | `the_post_thumbnail()` | `get_the_post_thumbnail()` | |
| **Categorías** | `the_category()` | `get_the_category()` | get_ devuelve array |
| **Etiquetas** | `the_tags()` | `get_the_tags()` | get_ devuelve array |
| **Autor** | `the_author()` | `get_the_author()` | |
| **Fecha** | `the_date()` | `get_the_date()` | |
| **Hora** | `the_time()` | `get_the_time()` | |
| **ID del post** | `the_ID()` | `get_the_ID()` | |

### ✅ Cuándo usar cada tipo

| Función | Uso | Requiere `echo` | Ejemplo |
|---------|-----|-----------------|---------|
| `the_title()` | Mostrar directamente | ❌ | `<?php the_title(); ?>` |
| `get_the_title()` | Procesar antes de mostrar | ✅ | `<?php echo get_the_title(); ?>` |

---

## 🔄 The Loop - El bucle de WordPress

### Estructura básica del Loop

```php
<?php
if (have_posts()) : 
    while (have_posts()) : the_post();
        // Aquí va el contenido de cada post
        ?>
        <article>
            <h2><?php the_title(); ?></h2>
            <?php the_content(); ?>
        </article>
        <?php
    endwhile;
else :
    echo '<p>No hay contenido disponible.</p>';
endif;
?>
```

### Ejemplo práctico con procesamiento

```php
<?php
if (have_posts()) :
    while (have_posts()) : the_post();
        
        // Obtener el título para procesarlo
        $titulo = get_the_title();
        
        // Ejemplo de procesamiento condicional
        if ($titulo == "Artículo Especial") {
            echo '<div class="destacado">';
        }
        
        // Crear ID único para el artículo
        echo '<h1 id="titulo_' . sanitize_title($titulo) . '">' . $titulo . '</h1>';
        
        // Mostrar contenido
        the_content();
        
        if ($titulo == "Artículo Especial") {
            echo '</div>';
        }
        
    endwhile;
endif;
?>
```

---

## 📄 Plantillas Single

Para mostrar un solo artículo, post o elemento.

### Ejemplo completo de single.php

```php
<?php get_header(); ?>

<main class="contenido-principal">
    <?php if (have_posts()) : ?>
        <?php while (have_posts()) : the_post(); ?>
            <article id="post-<?php the_ID(); ?>" <?php post_class('articulo-single'); ?>>
                
                <!-- Título del artículo -->
                <header class="entrada-header">
                    <h1 class="titulo-entrada"><?php the_title(); ?></h1>
                    
                    <!-- Meta información -->
                    <div class="meta-entrada">
                        <span class="autor">Por: <?php the_author(); ?></span>
                        <span class="fecha"><?php the_date(); ?></span>
                        <span class="categorias"><?php the_category(', '); ?></span>
                    </div>
                </header>
                
                <!-- Imagen destacada -->
                <?php if (has_post_thumbnail()) : ?>
                    <div class="imagen-destacada">
                        <?php the_post_thumbnail('large'); ?>
                    </div>
                <?php endif; ?>
                
                <!-- Contenido -->
                <div class="contenido-entrada">
                    <?php the_content(); ?>
                </div>
                
                <!-- Etiquetas -->
                <?php if (has_tag()) : ?>
                    <div class="etiquetas">
                        <?php the_tags('<span class="etiquetas-titulo">Etiquetas: </span>', ', ', ''); ?>
                    </div>
                <?php endif; ?>
                
            </article>
            
            <!-- Navegación entre posts -->
            <nav class="navegacion-posts">
                <?php
                previous_post_link('<div class="nav-anterior">%link</div>', '← %title');
                next_post_link('<div class="nav-siguiente">%link</div>', '%title →');
                ?>
            </nav>
            
        <?php endwhile; ?>
    <?php endif; ?>
</main>

<?php get_sidebar(); ?>
<?php get_footer(); ?>
```

---

## 📚 Plantillas Archive

Para mostrar listados de contenido (índices).

### Ejemplo de archive.php

```php
<?php get_header(); ?>

<main class="contenido-principal">
    
    <!-- Título del archivo -->
    <header class="archivo-header">
        <?php if (is_category()) : ?>
            <h1>Categoría: <?php single_cat_title(); ?></h1>
            <?php echo category_description(); ?>
        <?php elseif (is_tag()) : ?>
            <h1>Etiqueta: <?php single_tag_title(); ?></h1>
        <?php elseif (is_author()) : ?>
            <h1>Autor: <?php the_author(); ?></h1>
        <?php elseif (is_date()) : ?>
            <h1>Archivo por fecha: <?php the_archive_title(); ?></h1>
        <?php else : ?>
            <h1><?php the_archive_title(); ?></h1>
        <?php endif; ?>
    </header>
    
    <!-- Loop para mostrar posts -->
    <?php if (have_posts()) : ?>
        <div class="lista-posts">
            <?php while (have_posts()) : the_post(); ?>
                <article id="post-<?php the_ID(); ?>" <?php post_class('post-resumen'); ?>>
                    
                    <h2 class="titulo-post">
                        <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
                    </h2>
                    
                    <?php if (has_post_thumbnail()) : ?>
                        <div class="imagen-miniatura">
                            <a href="<?php the_permalink(); ?>">
                                <?php the_post_thumbnail('medium'); ?>
                            </a>
                        </div>
                    <?php endif; ?>
                    
                    <div class="extracto">
                        <?php the_excerpt(); ?>
                    </div>
                    
                    <div class="meta-post">
                        <span class="fecha"><?php the_date(); ?></span>
                        <span class="autor">por <?php the_author(); ?></span>
                        <span class="categorias"><?php the_category(', '); ?></span>
                    </div>
                    
                    <a href="<?php the_permalink(); ?>" class="leer-mas">Leer más →</a>
                    
                </article>
            <?php endwhile; ?>
        </div>
        
        <!-- Paginación -->
        <nav class="paginacion">
            <?php
            the_posts_pagination(array(
                'prev_text' => '← Anterior',
                'next_text' => 'Siguiente →',
            ));
            ?>
        </nav>
        
    <?php else : ?>
        <p>No se encontraron publicaciones.</p>
    <?php endif; ?>
    
</main>

<?php get_sidebar(); ?>
<?php get_footer(); ?>
```

---

## ❓ Funciones condicionales

### Principales funciones de contexto

```php
// Páginas y posts
is_home()           // Página de inicio del blog
is_front_page()     // Página principal del sitio
is_page()           // Cualquier página estática
is_page('about')    // Página específica (por slug)
is_page(123)        // Página específica (por ID)
is_single()         // Cualquier post individual
is_single('hello-world') // Post específico

// Archivos
is_category()       // Archivo de categoría
is_tag()           // Archivo de etiquetas
is_author()        // Archivo de autor
is_date()          // Archivo por fecha
is_archive()       // Cualquier archivo

// Otros
is_search()        // Página de resultados de búsqueda
is_404()           // Página de error 404
is_admin()         // Panel de administración
```

### Ejemplo de uso en plantillas

```php
<?php
// Diferentes comportamientos según el contexto
if (is_home()) {
    echo '<h1>Últimas publicaciones</h1>';
} elseif (is_page('contacto')) {
    echo '<h1>Contáctanos</h1>';
} elseif (is_single()) {
    echo '<nav class="breadcrumb">Estás leyendo un artículo</nav>';
}
?>
```

---

## 🛠️ Funciones de utilidad

### Manipulación de texto

```php
// Limpiar título para URL
$titulo = 'Hola Mundo, esto es un título con Ñ y acentos á';
$slug = sanitize_title($titulo); 
// Resultado: hola-mundo-esto-es-un-titulo-con-n-y-acentos-a

// Recortar texto
$extracto = wp_trim_words(get_the_content(), 20, '...');

// Obtener campos específicos de un post
$titulo = get_post_field('post_title', $post_id);
$slug = get_post_field('post_name', $post_id);
$contenido = get_post_field('post_content', $post_id);
```

### Inclusión de plantillas parciales

```php
// Incluir fragmentos reutilizables
get_template_part('partials/content', 'single');  // carga: partials/content-single.php
get_template_part('partials/hero');               // carga: partials/hero.php
get_template_part('components/card', 'producto'); // carga: components/card-producto.php
```

### Campos personalizados (Custom Fields)

```php
// Obtener un campo personalizado
$valor = get_post_meta($post_id, 'mi_campo_personalizado', true);

// Verificar si existe
if (get_post_meta($post_id, 'mi_campo', true)) {
    echo get_post_meta($post_id, 'mi_campo', true);
}

// Obtener todos los campos personalizados
$campos = get_post_meta($post_id);
```

### Imágenes destacadas

```php
// Verificar si tiene imagen destacada
if (has_post_thumbnail()) {
    // Mostrar en diferentes tamaños
    the_post_thumbnail('thumbnail');  // 150x150
    the_post_thumbnail('medium');     // 300x300
    the_post_thumbnail('large');      // 1024x1024
    the_post_thumbnail('full');       // Tamaño original
    
    // Con clases CSS personalizadas
    the_post_thumbnail('medium', array('class' => 'mi-clase-imagen'));
}

// Obtener URL de la imagen
$imagen_url = get_the_post_thumbnail_url($post_id, 'large');
```

### Menús de navegación

```php
// Mostrar menú registrado
wp_nav_menu(array(
    'theme_location' => 'menu-principal',
    'menu_class'     => 'navegacion-principal',
    'container'      => 'nav',
    'container_class'=> 'menu-contenedor'
));

// Menú con más opciones
wp_nav_menu(array(
    'theme_location'  => 'menu-footer',
    'depth'          => 2,
    'fallback_cb'    => false,
    'walker'         => new Mi_Walker_Personalizado()
));
```

---

## 🔒 Seguridad y buenas prácticas

### Escapar datos de salida

```php
// Para contenido HTML
echo esc_html($texto_usuario);

// Para atributos HTML
echo '<div class="' . esc_attr($clase_dinamica) . '">';

// Para URLs
echo '<a href="' . esc_url($enlace_dinamico) . '">Enlace</a>';

// Para contenido HTML permitido
echo wp_kses($contenido_html, array(
    'a' => array('href' => array(), 'title' => array()),
    'br' => array(),
    'em' => array(),
    'strong' => array(),
));

// Para JavaScript
echo '<script>var miVariable = ' . wp_json_encode($data) . ';</script>';
```

### Verificación de permisos

```php
// Verificar capacidades del usuario
if (current_user_can('edit_posts')) {
    echo '<a href="' . get_edit_post_link() . '">Editar</a>';
}

// Verificar nonce en formularios
if (wp_verify_nonce($_POST['mi_nonce'], 'mi_accion')) {
    // Procesar formulario de forma segura
}
```

---

## 🎨 Custom Post Types y Taxonomías

### Registrar Custom Post Type

```php
function registrar_productos() {
    register_post_type('producto', array(
        'public'      => true,
        'label'       => 'Productos',
        'labels'      => array(
            'name'          => 'Productos',
            'singular_name' => 'Producto',
            'add_new_item'  => 'Añadir nuevo producto',
            'edit_item'     => 'Editar producto',
        ),
        'supports'    => array('title', 'editor', 'thumbnail', 'excerpt'),
        'has_archive' => true,
        'rewrite'     => array('slug' => 'productos'),
        'show_in_rest'=> true, // Para Gutenberg
    ));
}
add_action('init', 'registrar_productos');
```

### Registrar taxonomía personalizada

```php
function registrar_marca_productos() {
    register_taxonomy('marca', 'producto', array(
        'public'       => true,
        'label'        => 'Marcas',
        'hierarchical' => true, // Como categorías (false = como etiquetas)
        'rewrite'      => array('slug' => 'marca'),
        'show_in_rest' => true,
    ));
}
add_action('init', 'registrar_marca_productos');
```

### Shortcodes personalizados

```php
function mi_shortcode_personalizado($atts) {
    $atts = shortcode_atts(array(
        'titulo' => 'Título por defecto',
        'color'  => 'azul',
    ), $atts);
    
    return '<div class="mi-shortcode ' . esc_attr($atts['color']) . '">' 
           . '<h3>' . esc_html($atts['titulo']) . '</h3>'
           . '</div>';
}
add_shortcode('mi_shortcode', 'mi_shortcode_personalizado');

// Uso: [mi_shortcode titulo="Hola Mundo" color="rojo"]
```

---

## 🚀 Hooks: Actions y Filters

### Actions comunes

```php
// Ejecutar código cuando se inicializa WordPress
add_action('init', 'mi_funcion_init');

// Añadir estilos y scripts
add_action('wp_enqueue_scripts', 'mi_funcion_scripts');
function mi_funcion_scripts() {
    wp_enqueue_style('mi-estilo', get_template_directory_uri() . '/style.css');
    wp_enqueue_script('mi-script', get_template_directory_uri() . '/script.js', array('jquery'));
}

// Ejecutar código al guardar un post
add_action('save_post', 'mi_funcion_guardar_post');
```

### Filters comunes

```php
// Modificar el extracto
add_filter('excerpt_length', function() { return 30; });
add_filter('excerpt_more', function() { return '...'; });

// Modificar el título
add_filter('the_title', function($title) {
    if (is_admin()) return $title;
    return strtoupper($title);
});
```

---

## 🎯 Consejos adicionales

### URLs limpias con query_vars

```php
function agregar_query_vars($vars) {
    $vars[] = 'mi_parametro';
    return $vars;
}
add_filter('query_vars', 'agregar_query_vars');

// Uso: ejemplo.com/mi-pagina?mi_parametro=valor
// Obtener: get_query_var('mi_parametro');
```

### Depuración y desarrollo

```php
// Mostrar información de debug
if (WP_DEBUG) {
    error_log('Mi mensaje de debug');
    var_dump($variable);
}

// Obtener información del post actual
global $post;
echo '<pre>' . print_r($post, true) . '</pre>';
```

---

## 📚 Recursos adicionales

### Herramientas de IA útiles
- **DeepSeek** - Asistente de código
- **GitHub Copilot** - Autocompletado inteligente
- **ChatGPT/Claude** - Consultas y debugging
- **Cursor** - Editor con IA integrada

### Documentación oficial
- [WordPress Codex](https://codex.wordpress.org/)
- [Developer Handbook](https://developer.wordpress.org/)
- [Template Hierarchy](https://developer.wordpress.org/themes/basics/template-hierarchy/)

---

*💡 **Tip final**: Siempre escapa los datos de salida, verifica permisos de usuario y utiliza las funciones nativas de WordPress para mantener la compatibilidad y seguridad.*
