# wpf-promoting-notice

## Description
A little library that does 2 things:
1. Adds an admin notice only on the plugin's settings page advertising about the Pro version of the plugin
2. Makes all the disabled features from the free version that eventually may get clicked point to the promoting notice

### Screenshot

![promoting-notice-only](https://user-images.githubusercontent.com/70968619/119685463-c301c680-be1b-11eb-8753-d146c3ba3601.png)

### Installation

Add this to your composer.json

```json
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/wpcodefactory/wpf-promoting-notice"
    }
  ],
  "require": {
    "wpfactory/wpf-promoting-notice":"dev-master"
  },
```

Don't forget to require the `autoload.php` to your project, as it's required for any composer library and to run `composer install`, of course :)


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


### Parameters

Parameter | Default value | Description
------------ | ------------- | ------------
**enable** | `true` |  Enables the notice or not
**woocommerce_section_id** | `''` | WooCommerce section id
**notice_template** | `'<div id="message" class="%dynamic_notice_class% wpf-promoting-notice notice notice-info inline"><p class="wpf-pan-p">%content_template%</p></div>'` | The whole notice template
**lib_dirname** | `dirname( __FILE__, 2 )` | The directory of the project
**highlight_notice_on_disabled_opt_click** | `true` | Makes the disabled features that may get clicked point to the promoting notice
**template_variables** | `array()` | Template variables you can use


`template_variables` parameters

Parameter | Default value | Description
------------ | ------------- | ------------
**%dynamic_notice_class%** | `isset( $args['woocommerce_section_id'] ) ? $args['woocommerce_section_id'] . '-notice' : ''` |  Dynamic notice class
**%pro_version_title%** | `__( 'Awesome plugin Pro', 'wpf-promoting-notice' )` |  Pro version title
**%pro_version_url%** | `'https://wpfactory.com/item/awesome-plugin/'` |  Pro version URL
**%plugin_icon_url%** | `'https://pluginfactory-tastystakes.netdna-ssl.com/img/site/plugin_icon.png'` |  Plugin icon URL
**%plugin_icon_style%** | `'width:38px;margin-right:10px;vertical-align:middle'` |  Plugin icon style
**%btn_icon_class%** | `wpf-pan-btn-icon dashicons-before dashicons-unlock` |  Button icon class
**%btn_icon_style%** | `position:relative;top:3px;margin:0 2px 0 -2px;` |  Button icon style
**%btn_style%** | `vertical-align:middle;display:inline-block;margin:0` |  Button style
**%btn_call_to_action%** | `__( 'Upgrade to Pro version', 'wpf-promoting-notice' )` |  Button call to action
**%main_text%** | `__( 'Disabled options can be unlocked using <a href="%pro_version_url%" target="_blank"><strong>%pro_version_title%</strong></a>', 'wpf-promoting-notice' )` |  Main text
**%main_text_style%** | `'vertical-align: middle;margin:0 14px 0 0;'` |  Main text style
**%content_template%** | `'<img class="wpf-pan-plugin-icon" src="%plugin_icon_url%"/>' . '<span class="wpf-pan-main-text">%main_text%</span>' . '<a target="_blank" class="wpf-pan-button button-primary" href="%pro_version_url%"><i class="%btn_icon_class%"></i>%btn_call_to_action%</a>'` |  Main content of the notice

### See it in action
https://user-images.githubusercontent.com/70968619/119685412-b8473180-be1b-11eb-829d-216e1895c8da.mp4
