# HackBot

Meet HackBot - a version of GitHub's Hubot. It's fun for the whole family!

This version is designed to be deployed on [Heroku][heroku] for IRC.

[heroku]: http://www.heroku.com

## HackBot Commands

Robots are good and all but it's no fun if they idle all day. Just remember, with great power comes great responsibility. Consider yourself warned. Here's how to converse with HackBot:

<table>
  <tr>
    <th>What?</th>
    <th>Base Command</th>
    <th>Example</th>
    <th>HackBot Response</th>
  </tr>
  <tr>
    <td>Gives you a nice list of available HackBot commands</td>
    <td>hackbot help</td>
    <td>hackbot help</td>
    <td>Displays a list of available commands</td>
  </tr>
  <tr>
    <td>Queries Google maps for direction</td>
    <td>hackbot map me * to *</td>
    <td>hackbot map me Etsy to Fat Cats</td>
    <td>http://maps.google.com/maps?q=etsy%20to%20fat%20cats&hl=en&sll=37.0625,-95.677068&sspn=73.579623,100.371094&vpsrc=0&hnear=etsy%20to%20fat%20cats&t=m&z=11</td>
  </tr>
  <tr>
    <td>Calculates the given expression</td>
    <td> hackbot math me *</td>
    <td> hackbot math me 1^1 * 2^2 * 3^3 </td>
    <td>108</td>
  </tr>
  <tr>
    <td>Translate a given word or phrase</td>
    <td>hackbot translate me *</td>
    <td>hackbot translate me salut</td>
    <td>"salut" is French for "hello"</td>
  </tr>
  <tr>
    <td> Returns a random animated gif based on your query </td>
    <td>hackbot animate me *</td>
    <td>hackbot animate me cat</td>
    <td> <img src="http://i.imgur.com/ZqddU.gif"> </td>
  </tr>
  <tr>
    <td> Queries Google Images for a random image </td>
    <td> hackbot image me *</td>
    <td> hackbot image me kitten</td>
    <td> <img src="http://static.ddmcdn.com/gif/how-to-solve-cat-behavior-problems-2.jpg"> </td>
  </tr>
  <tr>
    <td>Returns a pug image</td>
    <td> hackbot pug me</td>
    <td> hackbot pug me</td>
    <td><img src="http://30.media.tumblr.com/tumblr_lqexmferHa1qg02ino1_500.jpg"></td>
  </tr>
  <tr>
    <td>Returns a motivational squirrel image</td>
    <td> ship it</td>
    <td> ship it</td>
    <td><img src="http://images.cheezburger.com/completestore/2011/11/2/46e81db3-bead-4e2e-a157-8edd0339192f.jpg"></td>
  </tr>
  <tr>
    <td>Returns a lovely image of Ron Swanson</td>
    <td> hackbot swanson me </td>
    <td> hackbot swanson me  </td>
    <td><img src="http://i.imgur.com/DxpKu.jpg"></td>
  </tr>
  <tr>
    <td>Returns a "Courage Wolf" with associated text</td>
    <td> hackbot * courage *</td>
    <td> Why fear the unknown courage when it can fear you</td>
    <td><img src="http://memecaptain.com/9ddb9b.jpg"></td>
  </tr>
  <tr>
    <td>Returns a "All the things" poster with associated text</td>
    <td> hackbot * all the things</td>
    <td> hackbot refactor all the things</td>
    <td><img src="http://memecaptain.com/e13db6.jpg"></td>
  </tr>
  <tr>
    <td>Returns a "One does not simple" poster with associated text</td>
    <td> hackbot one does not simply *</td>
    <td> hackbot one does not simply compile julia from source</td>
    <td><img src="http://memecaptain.com/35fb5f.jpg"></td>
  </tr>
  <tr>
    <td>Returns a "Yo Dawg" poster with associated text</td>
    <td> hackbot You dawg * so * </td>
    <td> hackbot Yo dawg I heard you like package managers so I put a package manager in your package manager</td>
    <td><img src="http://memecaptain.com/d0c6a5.jpg"></td>
  </tr>
</table>

## Playing with Hubot

You'll need to install the necessary dependencies for hubot. All of
those dependencies are provided by [npm][npmjs].

[npmjs]: http://npmjs.org

## HTTP Listener

Hubot has a HTTP listener which listens on the port specified by the `PORT`
environment variable.

You can specify routes to listen on in your scripts by using the `router`
property on `robot`.

```coffeescript
module.exports = (robot) ->
  robot.router.get "/hubot/version", (req, res) ->
    res.end robot.version
```

There are functions for GET, POST, PUT and DELETE, which all take a route and
callback function that accepts a request and a response.

#
### Testing Hubot Locally

You can test your hubot by running the following.

    % bin/hubot

You'll see some start up output about where your scripts come from and a
prompt.

    [Sun, 04 Dec 2011 18:41:11 GMT] INFO Loading adapter shell
    [Sun, 04 Dec 2011 18:41:11 GMT] INFO Loading scripts from /home/tomb/Development/hubot/scripts
    [Sun, 04 Dec 2011 18:41:11 GMT] INFO Loading scripts from /home/tomb/Development/hubot/src/scripts
    Hubot>

Then you can interact with hubot by typing `hubot help`.

    Hubot> hubot help

    Hubot> animate me <query> - The same thing as `image me`, except adds a few
    convert me <expression> to <units> - Convert expression to given units.
    help - Displays all of the help commands that Hubot knows about.
    ...

Take a look at the scripts in the `./scripts` folder for examples.
Delete any scripts you think are silly.  Add whatever functionality you
want hubot to have.


## hubot-scripts

There will inevitably be functionality that everyone will want. Instead
of adding it to hubot itself, you can submit pull requests to
[hubot-scripts][hubot-scripts].

To enable scripts from the hubot-scripts package, add the script name with
extension as a double quoted string to the hubot-scripts.json file in this
repo.

[hubot-scripts]: https://github.com/github/hubot-scripts

## Deployment

    % heroku create --stack cedar
    % git push heroku master
    % heroku ps:scale app=1

If your Heroku account has been verified you can run the following to enable
and add the Redis to Go addon to your app.

    % heroku addons:add redistogo:nano

If you run into any problems, checkout Heroku's [docs][heroku-node-docs].

You'll need to edit the `Procfile` to set the name of your hubot.

More detailed documentation can be found on the
[deploying hubot onto Heroku][deploy-heroku] wiki page.


## Restart the bot

You may want to get comfortable with `heroku logs` and `heroku restart`
if you're having issues.