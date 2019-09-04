# -Load-JavaScript-only-on-specific-WordPress-pages


//Register hook to load scripts
add_action('wp_enqueue_scripts', 'my_theme_load_scripts');
 
//Load scripts (and/or styles)
function my_theme_load_scripts(){
   wp_enqueue_script('jquery');
   wp_enqueue_script('my_first_script', get_template_directory_uri() . '/includes/js/my_first_script.js');
   wp_enqueue_script('my_second_script', get_template_directory_uri() . '/includes/js/my_second_script.js');
 
   if(is_page()){ //Check if we are viewing a page
    global $wp_query;
 
        //Check which template is assigned to current page we are looking at
        $template_name = get_post_meta( $wp_query-&gt;post-&gt;ID, '_wp_page_template', true );
    if($template_name == 'slider-portfolio.php'){
           //If page is using slider portfolio template then load our slider script
       wp_enqueue_script('my_third_script', get_template_directory_uri() .'/includes/js/my_third_script.js');       
    }
   }
}
