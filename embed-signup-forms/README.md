# Embed & Signup forms

Signup forms make it easy for people to subscribe to your Sendicate mailing list.  Options can be opening your subscriber list in Sendicate then by clicking “Embed Subscribe Form” in the right sidebar.  Outside of the API there are 2 main ways to collect subscribers:

* [Link to signup page](#link-to-signup-page)
* [Signup form embed code](#signup-form-embed-code)

For customization options refer to:

* [Customize subscribe page design](#customize-subscribe-page-design)
* [Styling the embed code](#styling-the-embed-code)

## Link to Signup Page

The simplest approach is directing users to the list signup page.  This can be found at the bottom of the embed code page mentioned above.  The link is in the following format where “xxxxxx” is the list ID that can be seen in the URL.

    https://www.sendicate.net/subscribe/xxxxxx

##  Signup Form Embed Code   

Each list has its own embed code.  To access the list embed code in Sendicate click Manage, Subscribers, your list, then "embed subscribe form" on the sidebar.  Using the embed code offers the best integration as the subscriber enters their details into a form hosted on your site that is submitted to Sendicate directly.  Email is a required field, name is optional.   The code is a simple unstyled form.  All the inputs and ID’s need to match exactly for the form to submit properly.  The “xxxxxx” needs to be updated with the appropriate list ID found in the URL of your list.

    <form accept-charset="UTF-8" action="https://www.sendicate.net/subscribe/xxxxxx" method="post"> 
        <label for="subscriber_name">Name</label> 
        <input id="subscriber_name" name="subscriber[name]" type="text" /> <br /> 
        <label for="subscriber_email">Email</label> 
        <input id="subscriber_email" name="subscriber[email]" type="text" /> <br /> 
        <input name="commit" type="submit" value="Subscribe" /> 
    </form> 

## Customize Subscribe Page Design

Each list in Sendicate can have its own look and feel.  To customize Sendicate’s subscribe forms click Manage, Subscribers, your list, then "embed subscribe form" on the sidebar.   The following can be customized:

| Item | Description |
| :----- | :----- |
| Header Image  | Upload an image for the header.  If no image is chosen the “logo” image will be used from the Account section |
| Title | The heading title|
| Description text | Descpription paragraph|
| Background color | Hex value/color picker of the page background color|
| Background image | Upload an image for the page background.  Images will be tiled. |
| Success redirect| Upon successfully adding a subscriber Sendicate can redirect the user to a page on your website.  Enter a full URL |

## Styling the Embed Code

Inline CSS can be added to style colors, width, height, etc.  Javascript has also been added to show "Email Address" in the form as default text.  An example is below:

    <form accept-charset="UTF-8" action="https://www.sendicate.net/subscribe/xxxxxx" method="post">
        <input id="subscriber_email" name="subscriber[email]" type="text" value="Email Address" style="width: 130px !important; color: #CCCCCC; padding: 5px 2px 5px 2px; background-color: #F8EDE8; border: none !important;" onclick="if ( this.value == 'Email Address' ) { this.value = ''; }" onblur="if ( this.value == '' ) { this.value = 'Email Address'; }"/> 
        <input name="commit" type="submit" value="Subscribe" style="background-color: #F8EDE8; color: #CCCCCC; padding: 5px; border: none !important;" />
    </form>
