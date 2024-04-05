# UM Gamipress
Addition of UM Members Directory to the "Gamipress Ultimate Member Integration".

The code snippet which will create the HTML required by UM is using the "gamipress_ultimate_member_after_header_meta" function from the "Gamipress Ultimate Member Integration".
https://gamipress.com/add-ons/ultimate-member-integration/

## Customization
For each of the Members Directory templates ( `members-grid.php`, `members-list.php` ) you must add `{{{user.gamipress}}}` to the templates where you want the Gamipress User points displayed.
 
Example for `members-grid.php` is after `{{{user.hook_just_after_name}}}`

Customized templates must be saved for update safety at your active Theme's `ultimate-member` folder.
https://docs.ultimatemember.com/article/1516-templates-map

## Code Snippet

<code>
add_filter( 'um_ajax_get_members_data', 'um_ajax_get_members_data_gamipress', 10, 3 );
function um_ajax_get_members_data_gamipress( $data_array, $user_id, $directory_data )  {
    ob_start();
    gamipress_ultimate_member_after_header_meta( $user_id, array() );
    $data_array['gamipress'] = wp_kses( ob_get_clean(), UM()->get_allowed_html( 'templates' ) );
    return $data_array;
}
</code>


Install by adding the code snippet to your active theme’s functions.php file or use the “Code Snippets” Plugin https://wordpress.org/plugins/code-snippets/
