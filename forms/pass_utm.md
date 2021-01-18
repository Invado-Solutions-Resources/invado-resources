# Passing URL parameters from browser to iframe + iframe-resizer

### Layout Template for form

Layout Template which will be used for form should have `iframeResizer.contentWindow.js` file, see example below:

```
<!DOCTYPE html>
<html>
    <head>
        <base href="https://engage.invadosolutions.com" >
        <meta charset="utf-8"/>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
        <meta name="viewport" content="width=device-width,initial-scale=1">
        <meta name="description" content="%%description%%"/>
        <title>%%title%%</title>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/iframe-resizer/4.3.1/iframeResizer.min.js" integrity="sha512-ngVIPTfUxNHrVs52hA0CaOVwC3/do2W4jUEJIufgZQicmY27iAJAind8BPtK2LoyIGiAFcOkjO18r5dTUNLFAw==" crossorigin="anonymous"></script>
    </head>
    <body>
        %%content%%
    </body>
</html>
```

### Page where form will be displayed

Form recipient page should contain code below:

```
<noscript>
 <iframe src="PARDOT_FORM_URL" width="100%" height="500" type="text/html" frameborder="0" allowTransparency="true" style="border: 0"></iframe>
</noscript>
<script src="https://cdnjs.cloudflare.com/ajax/libs/iframe-resizer/4.3.1/iframeResizer.min.js" integrity="sha512-ngVIPTfUxNHrVs52hA0CaOVwC3/do2W4jUEJIufgZQicmY27iAJAind8BPtK2LoyIGiAFcOkjO18r5dTUNLFAw==" crossorigin="anonymous"></script>

<script type="text/javascript">
    var form = 'PARDOT_FORM_URL';
    var params = window.location.search;
    var thisScript = document.scripts[document.scripts.length - 1];
    var iframe = document.createElement('iframe');

    iframe.setAttribute('src', form + params);
    iframe.setAttribute('width', '100%');
    iframe.setAttribute('style', 'border:0;width:1px;min-width:100%;');
    iframe.setAttribute('class', 'pardot-form-iframe');
    iframe.setAttribute('height', 500);
    iframe.setAttribute('type', 'text/html');
    iframe.setAttribute('frameborder', 0);
    iframe.setAttribute('allowTransparency', 'true');

    thisScript.parentElement.replaceChild(iframe, thisScript);
    iFrameResize( { log: false }, '.pardot-form-iframe' );
</script>
```

What this code does:
1. `<noscript>` part is a fallback for browsers where user disables javascript, in this case browser wouldn't pass UTM parameters.
2. Script from CDN which loads `iframeResizer.min.js` file needed to change height of iframe with form.
3. Script which creates iframe html tag with needed parameters, please update `PARDOT_FORM_URL`.

Links:
- [Passing URL parameters from browser to iframe](https://help.salesforce.com/articleView?id=000317377&type=1&mode=1)
- [iframe-resizer cdn](https://cdnjs.com/libraries/iframe-resizer)
- [iframe-resizer documentation](http://davidjbradshaw.github.io/iframe-resizer/)
- [iframe-resizer basic setup](https://github.com/davidjbradshaw/iframe-resizer#typical-setup)
