# Testing HTML

You should have already tested your triggers by following the [Testing triggers](https://github.com/duckduckgo/duckduckgo#testing-triggers) section. Now that you're confident your triggers are functioning properly, follow these steps to see how it looks on a live server!

1. Go to the root of your forked repository.

  For example:

    ```shell
    cd zeroclickinfo-spice/
    ```

2. Start the server.

    ```shell
    duckpan server
    ```

    This command will start up a small Web server running on port 5000.

3. Visit the server in your browser.

    If you are running the duckpan server on your local computer, you can navigate to:

    [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

    Replace 127.0.0.1 with your server's IP address or Fully Qualified Domain Name if you have started the duckpan server remotely.

    You should now be able to browse your duckpan server and see live results. The server runs code from our site which should make it look very much like the real DuckDuckGo.

4. Search.

    Having already tested your triggers, you should be able to construct a query to hit that trigger and see your newly defined result. Information about the processing of your requests is printed to the terminal where you started the server. Any external API calls will be highlighted if supported by your terminal.

5. Debug.

    If your search doesn't hit an instant answer, there will be an error message displayed on the page: "Sorry, no hit for your instant answer."

  If the trigger is hit but you do not see something displayed on the screen, a number of things could be wrong:

    - You have a JavaScript error of some kind. Internally, we like to use the JavaScript console in [Firebug](http://getfirebug.com/) to get more details.

    - An external API was not called correctly. You should examine the Web server output to make sure the correct API is being called. If it's not you will need to revise your [Spice handle function](#spice-handle-functions).

    - An external API did not return anything. Firebug is a great help here, as well. You should be able to see the external call in your browser and examine the response.

6. Tweak the display.

    Once all of the processing is working properly, you will probably want to adjust your callback function to get the display just right. The [Guidelines](https://github.com/duckduckgo/duckduckgo#guidelines) have some pointers to help you along.

7. Document.

    Please document your code as appropriate using in-line comments.
