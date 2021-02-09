# Top.gg-python-webhook-tutorial-
A Unofficial tutorial on how to make a working webhook on top.gg or any other bot listing services.


# Begining

Webhooks is how programs communicate and share data, and this tutorial might be difficult if you don't know how to deal with it!



# Requirements

An Accepted discord bot in Top.gg

discord.py bot

# How to make a webhook in (vps):

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
            self.token = 'dbl_token'  # set this to your DBL token
            self.dblpy = dbl.DBLClient(self.bot, self.token, webhook_path='/dblwebhook', webhook_auth='password', webhook_port=5000)

        @commands.Cog.listener()
        async def on_dbl_vote(self, data):
            """An event that is called whenever someone votes for the bot on top.gg."""
            print("Received an upvote:", "\n", data, sep="")

        @commands.Cog.listener()
        async def on_dbl_test(self, data):
            """An event that is called whenever someone tests the webhook system for your bot on top.gg."""
            print("Received a test upvote:", "\n", data, sep="")


    def setup(bot):
        bot.add_cog(TopGG(bot))

