# wpf-promoting-notice

## Description
A little library that does 2 things:
1. Adds an admin notice only on the plugin's settings page advertising about the Pro version of the plugin
2. Makes all the disabled features from the free version point to the promoting notice if clicked

### Usage

```php
add_action( 'admin_init', 'add_promoting_notice' );
function add_promoting_notice(){
	$promoting_notice = wpf_promoting_notice();
	$promoting_notice->set_args( array(
		'woocommerce_section_id' => 'alg_wc_ev',
		'enable'                 => true,
		'template_variables'     => array(
			'%pro_version_url%'   => 'https://wpfactory.com/item/email-verification-for-woocommerce/',
			'%plugin_icon_url%'   => 'https://ps.w.org/emails-verification-for-woocommerce/assets/icon-128x128.png',
			'%pro_version_title%' => __( 'Email Verification for WooCommerce Pro', 'emails-verification-for-woocommerce' ),
		),		
	) );
	$promoting_notice->init();
}
```
