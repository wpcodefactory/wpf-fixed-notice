# WPFactory Promoting Notice

### Description
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
		'url_requirements'              => array(
			'page_filename' => 'admin.php',
			'params'        => array( 'page' => 'wc-settings', 'tab' => 'alg_wc_ev' ),
		),
		'enable'                        => true, // Probably you should apply some custom filter here that only returns true on free version
		'optimize_plugin_icon_contrast' => true // Use true here if the plugin icon is blurry
		'template_variables'     => array(
			'%pro_version_url%'    => 'https://wpfactory.com/item/email-verification-for-woocommerce/',
			'%plugin_icon_url%'    => 'https://ps.w.org/emails-verification-for-woocommerce/assets/icon-128x128.png',
			'%pro_version_title%'  => __( 'Email Verification for WooCommerce Pro', 'emails-verification-for-woocommerce' ),
			//'%main_text%'          => __( 'Disabled options can be unlocked using <a href="%pro_version_url%" target="_blank"><strong>%pro_version_title%</strong></a>', 'emails-verification-for-woocommerce' ),
			//'%btn_call_to_action%' => __( 'Upgrade to Pro version', 'emails-verification-for-woocommerce' ),
		),		
	) );
	$promoting_notice->init();
}
```


### Arguments

Parameter | Default value | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Description &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
------------ | ------------- | ------------
enable | `true` |  Enables the notice or not
notice_template | `'<div id="message" class="%notice_class%"><p class="wpfactory-pan-p">%content_template%</p></div>'` | The whole notice template
lib_dirname | `dirname( __FILE__, 2 )` | The directory of the project
highlight_notice_on_disabled_opt_click | `true` | Makes the disabled features that may get clicked point to the promoting notice
template_variables | [Documentation](https://github.com/wpcodefactory/wpf-promoting-notice/wiki/Template-variable-parameters) | Template variables you can use
optimize_plugin_icon_contrast | `false` | Improves the plugin icon img contrast

### See it in action
https://user-images.githubusercontent.com/70968619/119685412-b8473180-be1b-11eb-829d-216e1895c8da.mp4
