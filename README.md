# Shopify snippet for automatically render responsive images

The snippet accepts Image object or asset name and renders responsive image for given list of breakpoints, and for retina 2x and 3x.
Use the biggest image you have, snippet will resize it for specified breakpoints.

Params:

**img** - Image object or string with asset name

**width** - required. Default width of the image. Number value, or string of size with x ("100x80")

**breakpoints** - string with array of breakpoints "breakpointx.image_size.crop", divided by whitespaces.
Example: "750.600x500.center 400.350x300"

First parametr is a breakpoint, represents "max-width" query.

Second - image size on that breakpoint. You can specify height after x charachter or not.

Third parameter, crop, when specified, will crop image to needed ratio with specified way. 
More about crop - https://shopify.dev/api/liquid/filters/media-filters#img_url

**alt** - alt text to be used in image. If not set, alt from Image object will be used(if presented)

**selector** - if set, output will result not as Picture tag, but as a list of CSS media queries referring to given selector.

**lazy** - if true, image tags will be developed for lazy loading with lazysizes.js

Example: 
`{% render "responsive-img" with img: "tatoo-drawing.jpg", width:300, breakpoints: "700.300x 500.200x200.center 375.150x150.top", alt:"img", lazy: false %}`

Output:

```
<picture>
   <source media="(max-width: 700px)" srcset="//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x.jpg?v=15743099930555500971 1x, //cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x@2x.jpg?v=15743099930555500971 2x, //cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x.jpg?v=15743099930555500971 3x">
   <source media="(max-width: 500px)" srcset="//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_200x200_crop_center.jpg?v=15743099930555500971 1x, //cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_200x200_crop_center@2x.jpg?v=15743099930555500971 2x, //cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_200x200_crop_center.jpg?v=15743099930555500971 3x">
   <source media="(max-width: 375px)" srcset="//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_150x150_crop_top.jpg?v=15743099930555500971 1x, //cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_150x150_crop_top@2x.jpg?v=15743099930555500971 2x, //cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_150x150_crop_top.jpg?v=15743099930555500971 3x">
   <img src="//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x.jpg?v=15743099930555500971" alt="img">
</picture>
```

Using selector:
`{% render "responsive-img" with img: "tatoo-drawing.jpg", selector: ".my-image", width:300, breakpoints: "700.300x 500.200x200.center 375.150x150.top", alt:"img", lazy: false %}`

Output:

```
.my-image{
    background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x.jpg?v=15743099930555500971);
}
@media (max-width: 375px){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_150x150_crop_top.jpg?v=15743099930555500971);
    }
}
@media (max-width: 375px) and (-webkit-min-device-pixel-ratio: 2) and (min-resolution: 192dpi){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_150x150_crop_top@2x.jpg?v=15743099930555500971);
    }
}
@media (max-width: 375px) and (-webkit-min-device-pixel-ratio: 3) and (min-resolution: 250dpi){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_150x150_crop_top@3x.jpg?v=15743099930555500971);
    }
}
@media (max-width: 500px){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_200x200_crop_center.jpg?v=15743099930555500971);
    }
}
@media (max-width: 500px) and (-webkit-min-device-pixel-ratio: 2) and (min-resolution: 192dpi){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_200x200_crop_center@2x.jpg?v=15743099930555500971);
    }
}
@media (max-width: 500px) and (-webkit-min-device-pixel-ratio: 3) and (min-resolution: 250dpi){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_200x200_crop_center@3x.jpg?v=15743099930555500971);
    }
}
@media (max-width: 700px){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x.jpg?v=15743099930555500971);
    }
}
@media (max-width: 700px) and (-webkit-min-device-pixel-ratio: 2) and (min-resolution: 192dpi){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x@2x.jpg?v=15743099930555500971);
    }
}
@media (max-width: 700px) and (-webkit-min-device-pixel-ratio: 3) and (min-resolution: 250dpi){
    .my-image {
        background-image:url(//cdn.shopify.com/s/files/1/0555/5385/1542/t/1/assets/tatoo-drawing_300x@3x.jpg?v=15743099930555500971);
    }
}
```
