# Sendicate Email Template Design Specs

Create gorgeous and flexible email templates with Sendicate's own custom syntax.

## Table of Contents

* [Section Blocks](#section-blocks)
* [Block Types](#block-types)
* [If Statements](#if-statements)
* [Variables](#variables)
* [Link Tag](#link-tag)
* [Images](#images)
* [Custom Settings for Appearance](#custom-settings-for-appearance)


## Section Blocks

Blocks used to style sections by content type. All blocks are referenced in the template.  If a block isn't included default code will be used.

    <html>
      <title></title>
      <body>
        {block:headline}
          {title}
        {/block:headline}
        <footer>Sendicate</footer>
      </body>
    </html>

### Block Types

There are 6 types of blocks for use in templates and composing.  Each section can have its own bespoke styling and layout allowing for flexible templates.  The 6 section blocks are:

* [One Column](#one-column)
* [Two Columns](#two-column)
* [Three Columns](#three-column)
* [Headline](#headline)
* [Image](#image)
* [Video](#video)

![Sections](https://github.com/Sendicate/sendicate-theme-docs/raw/master/src/sections.png)

### Block Variables

Each variable corresponds to a field in the Compose section.

In this Headline section example the variables are heading, subheading, link_url.

![Section Heading](https://github.com/Sendicate/sendicate-theme-docs/raw/master/src/section-heading.png)

#### One Column

The variables title, link_url, link_title, image, body are all accessible wrapped in {block:one_column} {/block:one_column} tags prefaced with "column1"

| Variable | Description |
| :----- | :----- |
| {block:one_column} {/block:one_column}  | Defines section |
| {column1:title} | Column one title |
| {column1:body} | Column one body |
| {column1:link_url} | Column one URL |
| {column1:link_title} | Column one URL title |
| {column1:image} | Column one image tag.  {link_title} is used for alt text |

#### Two Column

The variables title, link_url, link_title, image, body are all accessible wrapped in {block:two_column} {/block:two_column} tags prefaced with "column2"

| Variable | Description |
| :----- | :----- |
| {block:two_column} {/block:two_column}  | Defines section |
| {column1:title} | Column one title |
| {column1:body} | Column one body |
| {column1:link_url} | Column one URL |
| {column1:link_title} | Column one URL title |
| {column1:image} | Column one image tag.  {link_title} is used for alt text |
| {column2:title} | Column two title |
| {column2:body} | Column two body |
| {column2:link_url} | Column two URL |
| {column2:link_title} | Column two URL title |
| {column2:image} | Column two image tag.  {link_title} is used for alt text |


#### Three Column

The variables title, link_url, link_title, image, body are all accessible wrapped in {block:three_column} {/block:three_column} tags prefaced with "column3"

| Variable | Description |
| :----- | :----- |
| {block:three_column} {/block:three_column}  | Defines section |
| {column1:title} | Column one title |
| {column1:body} | Column one body |
| {column1:link_url} | Column one URL |
| {column1:link_title} | Column one URL title |
| {column1:image} | Column one image tag.  {link_title} is used for alt text |
| {column2:title} | Column two title |
| {column2:body} | Column two body |
| {column2:link_url} | Column two URL |
| {column2:link_title} | Column two URL title |
| {column2:image} | Column two image tag.  {link_title} is used for alt text |
| {column3:title} | Column three title |
| {column3:body} | Column three body |
| {column3:link_url} | Column three URL |
| {column3:link_title} | Column three URL title |
| {column3:image} | Column three image tag.  {link_title} is used for alt text |

#### Headline

The variables heading, subheading, link_url are accessible wrapped in {block:headline} {/block:headline} tags.

| Variable | Description |
| :----- | :----- |
| {block:headline} {/block:headline}  | Defines section |
| {heading} | Heading text |
| {subheading} | body text |
| {link_url} | URL |

#### Image

The variables image, link_url, and title are accessible wrapped in {block:image} {/block:image} tags.

| Variable | Description |
| :----- | :----- |
| {block:image} {/block:image}  | Defines section |
| {image} | Image tag.  {title} is used for alt text |
| {title} | Title text |
| {link_url} | URL |

#### Video

The variables title, link_url, image, body are accessible wrapped in {block:video} {/block:video} tags.  The app will take a URL from Vimeo or Youtube and automatically created a thumbnail image for use in the template.

| Variable | Description |
| :----- | :----- |
| {block:video} {/block:video}  | Defines section |
| {image} | Image tag auto-generated from video link.  {title} is used for alt text |
| {title} | Title text |
| {body} | Body text |
| {link_url} | URL to hosted video |


## IF statements

All methods can be used with {if} - {/if} tags. Example:

    {block:one_column}
      {if column1:link_url}
        <!-- show a link -->
        <a href="{link_url}">{column1:link_title}</a>
      {/if}
    {/block:one_column}

## Variables
| Variable | Description |
| :----- | :----- |
| {name} | subscriber name |
| {email} | subscriber email |
| {subject} | message subject |
| {twitter_link} | url to twitter profile |
| {facebook_link} | url to facebook profile |
| {twitter_like} | url to twitter follow page |
| {facebook_like} | url to facebook like page |
| {web_url} | view email in browser |
| {mail_id} | identifier for email, each recipient has a unique id |
| {message_id} | identifier for message, each message has a unique id |

### Date/Time variables

Assume that current time is Tuesday, 17 July 2012 09:54:45

| Variable | Description |
| :----- | :----- |
| {YYYY} | Year with century ("2012") |
| {YY} | Year without century ("12") |
| {MMMM} | Full month name ("July") |
| {MMM} | Abbreviated month name ("Jul") |
| {MM} | Month of the year ("07") |
| {DD} | Day of the month ("17") |
| {WWWW} | Full weekday name ("Tuesday") |
| {WWW} | Abbreviated weekday name ("Tue") |
| {H} | Hour of the day, 24-hour clock, no leading zero ("9") |
| {HH} | Hour of the day, 24-hour clock, with leading zero ("09") |
| {h} | Hour of the day, 12-hour clock, no leading zero ("9") |
| {hh} | Hour of the day, 12-hour clock, with leading zero ("09") |
| {M} | Minute of the hour ("54") |
| {S} | Second of the minute ("45") |
| {t} | Meridian indicator ("AM" or "PM") |
| {time} | Equivalent to "{HH}:{M}" ("09:54") |
| {date} | Equivalent to "{YYYY}-{MM}-{DD}" ("2012-07-17") |

## Link Tag

{:column:link_tag} will replace with following content:

    {if :column:link_url}<a href="{:column:link_url}" alt="{:column:link_title}">{/if}

{:column:link_tag} will replace with following content:

    {if :column:link_url}</a>{/if}

:column: - column identifier, e.g. {column1:link_tag}

Sample for using with Image Block:

    {link_tag}
      {image(300x)}
    {/link_tag}

Sample for using with OneColumn Block:

    {column1:link_tag}
      {column1:image(300x)}
    {/column1:link_tag}

## Images

Image tags and image URL's can be output in the following ways:

    {image} #outputs a full image tag at default 400px wide
    {image_url} #outputs the path to the URL of the original uploaded image.
    {image(400x)} #resizes the image.  See below for options
    
When an image tag is rendered the heigh and width are calculated automatically, and style attributes such as border:none are added.

### Resizing

Images can be dynamically resized or cropped by passing a geometry parameter

    {image(400x400^)} #crops image to a 400px x 400px square

We follow's ImageMagick's geometry strings.  Here is a sample:

| Geometry | Description |
| :----- | :----- |
| 400x300 | resize, maintain aspect ratio |
| 400x300! | force resize, don't maintain aspect ratio |
| 400x | resize width, maintain aspect ratio |
| x300 | resize height, maintain aspect ratio |
| 400x300> | resize only if the image is larger than this |
| 400x300< | resize only if the image is smaller than this |
| 50x50% | resize width and height to 50% |
| 400x300^ | resize width, height to minimum 400,300, maintain aspect ratio |
| 2000@ | resize so max area in pixels is 2000 |
| 400x300# | resize, crop if necessary to maintain aspect ratio (centre gravity) |
| 400x300#ne | as above, north-east gravity |
| 400x300se | crop, with south-east gravity |
| 400x300+50+100 | crop from the point 50,100 with width, height 400,300 |

## Custom Settings for Appearance

Custom settings allow users to customize elements of the design without needing to know HTML.  The theme author is free to make any elements variables, such as logo, font, colors, etc

There are 4 types of custom settings attributes available:

| Variable | Description |
| :----- | :----- |
| {color:name} | Edit colors with a color picker widget |
| {text:name} | Custom text settings |
| {image:name} | Image upload widget |
| {font:name} | Font picker widget |

### Initialization

Design custom settings are initialized through meta tags, in the head section of design body:

    <meta name="color:block background" content="#eee"/>
    <meta name="text:greeting" content="Hello"/>
    <meta name="font:font" content="Arial, sans-serif"/>
    <meta name="image:logo" content="http://www.google.com/images/logo.png"/>

First part of name attribute is a widget type. There are four types of settings: image, color, text and font. Last part of name is a unique name for widget. It is important that name attribute of meta tag was formed by the rules above.

Content attribute is an optional. Its value set default value for a widget. Image widgets accepts remote url to image file. And returns url for image file

### Usage

Just put variable same as in name attribute like
    {text:greeting}
NOTE: For images also can be set dimensions. For example
    {image:logo(100x100!)}
    {image:logo(30x40)}
In this case it will return same image but with different sizes

#### Example of real usage:

Template:

    <html>
      <head>
        <meta name="color:body_background" content="#fff"/>
        <meta name="color:Header background" content="#bbd9ee"/>
        <meta name="color:link" content="#0066b3"/>
        <meta name="text:greeting" content="Hello World!"/>
        <meta name="font:font" content="Arial, sans-serif"/>
        <meta name="image:logo" content="http://www.google.com/images/logo.png"/>
        <style>
            html,body{margin:0;padding:0}
            body { background: {color:body_background}; font-family: {font:font} }
            .header { width:100%;overflow:hidden; background: {color:header background}; }
            a { color: {color:link}; background: inherit;}
        </style>
      </head>
      <body>
        <div class="header">
          <p><img src="{image:logo}"/></p>
          <p>{text:greeting}</p>
        </div>
    </html>

Output:

    <html>
      <head>
        <style>
            html,body{margin:0;padding:0}
            body { background: #fff; font-family: Arial, sans-serif }
            .header { width:100%;overflow:hidden; background: #bbd9ee; }
            a { color: #0066b3; background: inherit;}
        </style>
      </head>
      <body>
        <div class="header">
          <p><img src="http://www.google.com/images/logo.png"/></p>
          <p>Hello World!</p>
        </div>
    </html>
