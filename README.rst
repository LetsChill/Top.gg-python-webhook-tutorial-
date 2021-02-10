**Top.gg-python-webhook-tutorial-**
--------
A Unofficial tutorial on how to make a working webhook on top.gg or any other bot listing services.


Begining
---------

Webhooks is how programs communicate and share data, and this tutorial might be difficult if you don't know how to deal with it!



Requirements
------------

- **An Accepted discord bot in Top.gg**

- **discord.py bot**

- **dbl Module installed**

How to install dbl module
----------------

Install via pip (recommended)

.. code:: bash

    pip install dblpy

**Cog is needed for this explanation, you should know what are cogs, check https://discordpy.readthedocs.io/en/latest/ext/commands/cogs.html**

How to make a webhook:
----------------

There is alot it of stuff you can use with the webhook, you will learn how to make a webhook for guild posting, and receiveing data from top.gg:

Copy and paste this code in a python file inside your cogs folder:

.. code:: py

    from discord.ext import commands

    import dbl


    class TopGG(commands.Cog):
        """
        This example uses dblpy's webhook system.
        In order to run the webhook, at least webhook_port must be specified (number between 1024 and 49151).
        """

        def __init__(self, bot):
            self.bot = bot
            self.token = 'TOKEN'  # set this to your DBL token
            self.dblpy = dbl.DBLClient(self.bot, self.token, webhook_path='/dblwebhook', webhook_auth='PASSWORD', webhook_port=8080)

        @commands.Cog.listener()
        async def on_dbl_vote(self, data):
            vote_data = data
            voter = await self.bot.fetch_user(vote_data['user'])
            channel = self.bot.get_channel(ID)
            """An event that is called whenever someone votes for the bot on top.gg."""
            print("Received an upvote:", "\n", data, sep="")
            await channel.send(f"Thank You {voter.mention} For voting!")
 
        @commands.Cog.listener()
        async def on_dbl_test(self, data):
            """An event that is called whenever someone tests the webhook system for your bot on top.gg."""
            test_data = data
            tester = await self.bot.fetch_user(test_data['user'])
            channel = self.bot.get_channel(ID)
            print("Received a test upvote:", "\n", data, sep="")
            await channel.send(f"Tested the webhook and working {tester.mention}")
            

    def setup(bot):
        bot.add_cog(TopGG(bot)

**Now Change some variables in the code**

- Change TOKEN to your top.gg api token, can be found in your bots edit>Webhook tab page in Top.gg

**The variables PASSWORD can be anything, this should stay as a secret, change it to what ever you want! be carefull.**

if your changed the PASSWORD to anything you want, go to your webhook tab on top.gg and put the password in the authorisation field, under the webhook url.

**Restart your bot so the cog can be loaded now**

now the part where you find your webhook url.

- **On Repl.it** 

the webhook url format is: https://YOUR_REPL_PROJECT_NAME.YOUR_REPL_USER_NAME.repl.co/dblwebhook


- **For VPS** 

Get your ip adress, and port, when you get both of them, **IF THE PORT IS NOT 8080, CHANGE THE PORT IN THE CODE TO YOUR PORT**, make sure the port in the code matches your vps port.

the format of the webhook url must be : **X.X.X.X:XXXX or XXXXX/dblwebhook**

if you complete all the steps above, test the webhook, worked?, Congrats!

*subjected to change*

-- **For selfhosting**

still investigating how to do so, stay tuned.




repl users: **IF YOU HAVE A FLASK SERVER, ITS OK, TOP.GG CAN ACT AS A WEBSITE, UPTIMEBOT WILL SAY ITS DOWN BUT WILL KEEP PINGING IT! DO NOT RUN A FLASK SERVER WHILE RUNNUNG A WEBHOOK**
