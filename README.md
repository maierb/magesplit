MageSplit
=========

**Overview**

MageSplit is an extremely simple tool for running split tests in Magento.  
The reason that I put it together was that I was just beginning to run
some very simple tests, and wasn't really interested in paying for a
service.

Also, the types of tests that I was doing didn't really require a nice
visual editor, which is usually one of the main features of the A/B
testing services that are out there.

**Installation**

Install using modman:

    modman clone git@github.com:kalenjordan/magesplit.git
    
Then, to create a test, just pop into one of your `phtml` files, and:

    <script type="text/javascript">
        if (typeof(MageSplit) != 'undefined') {
            new MageSplit().run('red_addtocart_button', function() {
                jQuery('button#addtocart').css('color', 'red');
            });
         }
    </script>

**How does it work?**

All that it does is generates a random number per each visitor, storing
it on a cookie.  If it's greater than 0.5, then it enables the experiment.

When the experiment is enabled, the code that you've defined will be run,
and also a custom event will be sent up to Google Analytics, with a category
name of MageSplit, and an event name of "$experimentName: Enabled"
or "$experimentName: Disabled".

So, you get the idea - crazy simple and probably not very useful if you're
doing anything fancy.  But if you're just getting started, may save you
a minute or two fussing around with javascript cookies.
