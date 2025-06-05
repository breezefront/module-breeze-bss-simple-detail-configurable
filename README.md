# Bss Simple Details on Configurable Product Breeze Frontend Integration

Integration done for the module version 1.5.3

## Installation

```bash
composer require swissup/module-breeze-bss-simple-detail-configurable
bin/magento setup:upgrade --safe-mode=1
```

## Required patches

Bss_Simpledetailconfigurable/js/configurable_control.js:

```diff
@@ -109,7 +109,7 @@
                 }
             }

-            var url = $(location).attr('href');
+            var url = location.href;
             if (url.split('+').pop() === 'sdcp-redirect') {
                 window.paramRedirect = url.split('+').slice(0, -1);
                 window.paramRedirect.shift();
@@ -524,7 +524,7 @@
         _UpdateActiveTab: function () {
             $('.data.item.title').removeClass("active");
             $('.data.item.content').css('display', 'none');
-            if ($(window.location).attr('hash') == '') {
+            if (window.location.hash == '') {
                 $('.data.item.title:not(.' +this.options.sdcp_classes.hiddenTab+ ')').first().addClass('active');
                 $('.data.item.content:not(.' +this.options.sdcp_classes.hiddenTab+ ')').first().css('display', 'block');

@@ -903,7 +903,7 @@
         _UpdateUrl: function ($parentUrl, $customUrl, $config, $suffix) {
             if ($config > 0 && $('.checkout-cart-configure').length == 0) {
                 $customUrl = $customUrl.replace(/[`!@#$%^&*()|\;:'",.<>\{\}\[\]\\\/]/g,'');
-                $customUrl = $.trim($customUrl);
+                $customUrl = $customUrl.trim();
                 while ($customUrl.indexOf(' ') >= 0) {
                     $customUrl = $customUrl.replace(" ", "~");
                 }
@@ -929,7 +929,7 @@
         _UpdateSelected: function ($options, $widget) {
             var config = $options.jsonModuleConfig,
                 data = $options.jsonChildProduct,
-                customUrl = $(location).attr('href').replace(config.url_suffix, ''),
+                customUrl = location.href.replace(config.url_suffix, ''),
                 selectingAttr = [],
                 attr,
                 selectedAttr = customUrl.split('+'),
@@ -982,7 +982,7 @@
                             + '"] .swatch-attribute-options').children().is('div')) {
                             $('.swatch-attribute[' + swSelector + 'attribute-code="' + $code + '"] .swatch-attribute-options .swatch-option').each(function () {
                                 var optionLable = $(this).attr(swSelector + 'option-label').replace(/[~`!@#$%^&*()|\;:'",.<>\{\}\[\]\\\/]/g,'').replace(/\s/g,'');
-                                optionLable = $.trim(optionLable);
+                                optionLable = optionLable.trim();
                                 if (optionLable == $value) {
                                     $(this).trigger('click');
                                     return false;

```
