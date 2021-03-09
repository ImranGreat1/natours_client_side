// The two basic fundamentals of responsive design is deciding whether to build your
website or app using mobile-first or desktop-first approach.

// Most of the times people build their application using desktop-first approach because it
is simpler to grasp and also scale down your website/app to adapt to smaller screens or viewport.

// Breakpoints => these are the viewport width we defined to set where we want to change or add new
styles for a certain viewport.




// Desktop-first approach
1. We use the max-width media query property to set breakpoints for smaller viewports

2. To add a media query for devices under 600px we use:
   @media (max-width: 600px) {
        // The styles inside this will apply to all viewport less than or equal 600px
   }


// Mobile-first approach
1. We use the min-width media query property to set breakpoints for larger viewports

2. To add a media query for devices over 600px we use:
   @media(min-width: 600px) {
        // The styles here will apply to all devices equal and over 600px
   }


//NOTE: media queries do not add any importance or specificity to styles we write, what matters
is the order in which they appear in the code. In a case where two media queries match the
current viewport, the styles in the media query that comes last in the code applies.
Example of such case is given that our current viewport is 500px:
Case 1:
// Both queries matched, but the one that appear last is the applied style, in this case
the browser will use the 900px query
@media(max-width: 600px) {
    html {
        font-size: 45%
    }
}

@media(max-width: 900px) {
    html {
        font-size: 50%
    }
}

Case 2:
// The correct and intended arrangement is to make the smaller pixel media query appear
last, this way the 900px only applies when the query is greater than 600px

@media(max-width: 900px) {
    html {
        font-size: 50%
    }
}

@media(max-width: 600px) {
    html {
        font-size: 45%
    }
}


// PROS of Mobile-first approach
1. 100% optimised for the mobile experience
2. Reduces website and apps to absolute essentials
3. Results in smaller, faster and more efficient products
4. Prioritizes content over aesthetic design, which may be
desirable


// CONS of Mobile-first approach
1. The desktop version might feel overly empty and simplistic
2. More difficult and counterintuitive to develop
3. Less creative freedom, making it more difficult to create
distinctive products
4. Clients are use to seeing a desktop version of the site as a protoype
5. Do your users even use the mobile internet? What's the purpose of your website?


// NO MATTER WHAT YOU DO ALWAYS KEEP BOTH DESKTOP AND MOBILE IN MIND.

// SOME MEDIA QUERIES TIPS
1. In media queries we should always use em units for font-size because they are said to be
more consistent than rem.

2. Media queries doesn't use our defined root font-size, it always use the root font-size.
The default font-size in every media query will always be the browser font-size which is 16px
even if we define the root font-size in the html or body tag

3. We should use em unit to specify our breakpoints in the media query function because they
are more consistent across browsers.

// Tips on the order in which we write our media queries
Order: Base + typography > general layout + grid > page layout > component



// RESPONSIVE IMAGES

The philosophy behind responsive images is to serve the right image to the right screen
size, in order to avoid downloading unnecessary large images on smaller screens. We achieve
this using different techniques in HTML and CSS.


// When to use responsive images: The 3 use cases

1. Resolution Switching: is to serve up the same image for a smaller screen but with a different
resolution.

2. Density Switching: It is actually the same case with resolution switching but here the screen
size doesn't matter but the screen pixel density does instead. Pixel density is the amount of
pixel found in an inch or a centimeter. What matters to use is that we have high and low resolu-
tion screen, low resolution screens are typical PC screens, high resolution screens are usually
found in smartphones and some more than PCs like the macbooks with retina display. Low resolution
screen can be called 1x screen because they use 1 pixel to display 1 pixel of our design e.g If
we say our image should be 100px high, it will use 100px physical pixel to display that image
in our device. In order case high res screen use 2px to display 1px pixel of our design, in this
case a 100px image will be displayed using 200px physical pixels in our device. If we want our
image to be sharp in high-res screen them we will have to server an image that double the resol-
ution of our original image.

3. Art Direction: This is when we server a whole different image for a different screen size




// DENSITY SWITCHING AND ART DIRECTION IN PRACTICE
<picture class="footer__logo">
    <source 
        srcset="./img/logo-green-small-1x.png 1x, ./img/logo-green-small-1x.png 2x"
        media="(max-width: 37.5em)"
        src="./img/logo-green-small-1x.png"
        alt="Full green logo"
        >
    <img
        srcset="./img/logo-green-1x.png 1x, ./img/logo-green-2x.png 2x"
        alt="Full green logo"
        src="./img/logo-green-1x.png"
        >
</picture>

1. We use the picture element to load a different image based on the device/viewport

2. In the viewport we can have one or more source

3. The media attribute is where we want to specify at which viewport should that image render

4. Using srcset intead of src, we can provide different images for different display density. To
that you will seperate each image path by a comma and at the end of each path there should be the
display density for either 1x or 2x based on your target density.

5. img tag we specify is the default image, when the media query didn't match. We can also specify
srcset attribute to display different image for different display density

6. We can also add a src attribute to specify a fallback image for older browsers that doesn't
understand the srcset attribute.


// RESOLUTION SWITCHING IN PRACTICE
<img
    srcset="./img/nat-1.jpg 300w, ./img/nat-1-large.jpg 1000w"
    sizes="(max-width: 75em) 22vw, (max-width: 56.25em) 20vw, (max-width: 37.5em) 30vw, 300px"
    class="composition__photo composition__photo--p1"
    alt="Photo 1"
    src="./img/nat-1.jpg"
    >

1. In the srcset attribute we specify the images that we want to use based on the resolution.
At the end of each image path we specify the width of the image we are using.e.g 300px => 300w

2. In the sizes attribute we specify some breakpoints at which we want the browser to decide which
image should be use, at the end of each breakpoint we also give the current width of that image in
our viewport so that the browser will choose the right image to display in the browser.

3. The browser uses the width of the images, the current viewport and the current size of the image
in the viewport to determine what image to use.

4. 300px is the default width of the images when not in any media query. When not in any media query
the browser will use the viewport width and screen density to determine which image to use.




// NOTE:
HTML  <meta name="viewport" content="width=device-width, initial-scale=1.0"> is very
essential for responsive design, it is basically saying that the width of our web page
should be the device width. We must include it if we want our responsive design to work.