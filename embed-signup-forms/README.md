# Embed & Signup forms

Signup forms make it easy for people to subscribe to your Sendicate mailing list.  Options can be opening your subscriber list in Sendicate then by clicking “Embed Subscribe Form” in the right sidebar.  There are 2 main ways to collect subscribers:

* [Link to Signup Page](#link-to-signup-page)
* [Signup form embed code](#signup-form-embed-code)

## Link to Signup Page

The simplest approach is directing users to the list signup page.  This can be found at the bottom of the embed code page mentioned above.  The link is in the following format where “xxxxxx” is the list ID that can be seen in the URL.

    https://www.sendicate.net/subscribe/xxxxxx

##  Signup Form Embed Code   

Each list has its own embed code.  To access the list embed code in Sendicate click Manage, Subscribers, your list, then "embed subscribe form" on the sidebar.  Using the embed code offers the best integration as the subscriber enters their details into a form hosted on your site that is submitted to Sendicate directly.  Email is a required field.   The code is a simple unstyled form.  All the inputs and ID’s need to match exactly for the form to submit properly.  The “xxxxxx” needs to be updated with the appropriate list ID found in the URL of your list.

    <form accept-charset="UTF-8" action="https://www.sendicate.net/subscribe/xxxxxx" method="post"> 
        <label for="subscriber_name">Name</label> 
        <input id="subscriber_name" name="subscriber[name]" type="text" /> <br /> 
        <label for="subscriber_email">Email</label> 
        <input id="subscriber_email" name="subscriber[email]" type="text" /> <br /> 
        <input name="commit" type="submit" value="Subscribe" /> 
    </form> 
