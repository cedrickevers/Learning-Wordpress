# Project Title
 
On ne touche pas au core de wordpress ( ex : wp-admin, wp-include)  car il est effacé à chaque MAJ
En période de développement Définir sur true =>  define(WP_DEBUG, true)   dans le fichier wp-config-sample.php pour avoir les infos du   debug afin de comprendre ou le code foire et comment remédier à ça.
Inserer ce commentaire dans l’index.php a la racine du dossier contenant le plugin pour empecher que des intrus viens chipoter dans le code
ABSPATH not define : si quelqu’un d’extérieur a notre site  ya  accest alors ca met fin au script ou sans les permissions wordpress
 




## Potection
 
 Dans  le fichier index. inserer le code suivant :
 

<?php
// Silence is golden.

 Autres alternatives 
Define or die 
If ( ! function_exists( ‘add_cations) {
Optionnel “Echo msg”;
Exit;

License Gnu requise pour publier officiellement son plugin dans wordpress
Qu’est- ce qu’un plugin ?

C’est du code qui étends les fonctionnalités du cœur, cela peut-être un simple fichier php par exemple regroupant les liens vers nos meilleur articles a orgniser dans un repertoire qui lui sont dédiés

Code Requis   à placer dans le header du fichier ou se trouve le code du  plug in 
https://developer.wordpress.org/plugins/plugin-basics/header-requirements/


Hooks: Actions and Filters #
https://developer.wordpress.org/plugins/plugin-basics/
Permets :
D’accéder à des endroits spécifiques afin de modifier le comportement de WordPress sans avoir à   toucher les fichiers principaux. (pas limiter aux plugins)

Action hooks
Permets d’ajouter des fonctionnalités

Filters hooks :

Permets de customiser l’affichage en choisissant une catégorie d’article par exemple.

Function permetant d’activer le plug in
 register_activation_hook( string $file, callable $function )

Parameters #Parameters
$file
(string) (Required) The filename of the plugin including the path.
$function
(callable) (Required) The function hooked to the 'activate_PLUGIN' action.
________________________________________
Top ↑
Source #Source
File: wp-includes/plugin.php
783
784
785
786	function register_activation_hook( $file, $function ) {
    $file = plugin_basename( $file );
    add_action( 'activate_' . $file, $function );
}



Comment creer un plugin

Avant de commencer quoique ce soit il faut vérifier que le nom que l’on compte donner au plug in n’est pas déjà pris ‘lancer une verif dans le hub Wordpress : pluigins-> search Result)

Créer un dossier avec plugin-nom plugins et a l’intérieur un fichier .php avec le nom exact du dossier contenant le plugin

Par defaut WordPress vérifie tous les fichiers a ‘linterieurs du dossier plugin et montre ceux contenant un fichier avec le meme nom que le dossier. Sinon wordpress ne detect pas qu’il s’agit d un environnement destiné aux plugins.
Wordpress declenche aussi  3 actions  par défaut  lorsqu’on utilise ses porpres plugins :
Ces mrthodes sont utiles pour updataer la database quand les utilisateur activent et desactive le plugin
Afin d être sur que le CPT ne s’activep as ou desactive pas par erreur et bien parce que c était intentionnel 

Cleanup de database en gros ?
// Activation
Register_activation_hooks( __FILE__, $function) :
__FIME__ précise que que ce hook ne s’applique que dans ce dossier
//Deactivation

Flush rewrite rules to tell wordpress not showing CPT once the plugin is no activated
// uninstal

Si on considère comme une database de post et pages

 Flush rewrite rules
Lorsque l’on modifie quelque chose ou qu’on interragi avec la base de donnée à l’activation d’un plugin  hook la méthode flush_rewrite_rules() a l’activation et a la desactivation de ce plugin
On peut l’appeler n’importe car c’est une fonction globale qui renvois du code procédurale

2 façons de faire pour supprimer les posts

La méthode wp_delete_post qui boucle sur chaque post
Plus puissante mais à manier avec précaution la global $wpdb qui accède directement a la base de donnée WordPress via requête SQL
 
