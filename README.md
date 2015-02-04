# wp-donate-shortcode

// Donate TEXT Shortcode
function paypal_donate_shortcode($atts) {
    extract(shortcode_atts(array(
        'text' => 'Make a donation with PayPal',
        'account' => 'martin@khoury.net.au', // Your PayPal email
	'itemname' => '', // replace
	'itemnumber' => '', // replace
 	'amount' => '', // default donation
    ), $atts));

    global $post;
    global $authordata;
    $blogName = get_bloginfo('name');

    $via = str_replace(" ","+",$post->post_title);
    if (!$itemname) $itemname = str_replace(" ","+","$blogName");
    if (!$itemnumber) $itemnumber = str_replace(" ","+",$authordata->display_name);

    return '<a class="donateLink" href="https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business='.$account.'&item_name='.$itemname.'&item_number=Donation+for+'.$itemnumber.'+via+'.$via.'&amount='.$amount.'&currency_code=USD">'.$text.'</a>';
}
add_shortcode('donate', 'paypal_donate_shortcode');



// Donate IMAGE Shortcode
function paypal_image_shortcode($atts) {
    extract(shortcode_atts(array(
        'account' => 'martin@khoury.net.au', // Your PayPal email
	'itemname' => '', // replace
	'itemnumber' => '', // replace
 	'amount' => '', // default donation
 	'image' => 'http://www.internoetics.com/images/btn_donate_LG.gif',
    ), $atts));

    global $post;
    global $authordata;
    $blogName = get_bloginfo('name');

    $via = str_replace(" ","+",$post->post_title);
    if (!$itemname) $itemname = str_replace(" ","+","$blogName");
    if (!$itemnumber) $itemnumber = str_replace(" ","+",$authordata->display_name);

    return '<a href= "https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business='.$account.'&item_name='.$itemname.'&item_number=Donation+for+'.$itemnumber.'+via+'.$via.'&amount='.$amount.'&currency_code=USD"><img src='.$image.' border="0"></a>';
}
add_shortcode('donateimage', 'paypal_image_shortcode');
