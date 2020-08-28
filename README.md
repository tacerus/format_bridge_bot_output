# Fork of format_bridge_bot_output

This is a fork of the `format_bridge_out_bot_output` weechat script

## Original README
Intercepts messages before WeeChat displays them and if found to have been sent by a bridge bot proceeds to alter the message so that when displayed it has the appearance of being sent by a native IRC user.

I wrote a blog post to accompany this script when I first released it in November 2018: [WeeChat IRC Client - Formatting Bridge Bot Output](https://www.thecliguy.co.uk/2018/11/18/weechat-format-bridge-bot-output-script)

## Using this for the #ocaml discord bot

Downlaod the script:

```
wget -O ~/.weechat/python/format_bridge_bot_output.py \
  https://raw.githubusercontent.com/Gbury/format_bridge_bot_output/master/format_bridge_bot_output/format_bridge_bot_output.py
```

(Optional) Link it for auto-loading:
```
cd ~/.weechat/python/autoload && ln -s ../format_bridge_bot_output.py
```

Load the script in weechat:
```
/script load format_bridge_bot_output.py
```

In weechat, setup the script for your desired channel:
```
/format_bridge_bot_output_add-server-channel-botnicks-nicklength <group_name> <server_name> <channel_name> <bot_name> <max_nick_length>
```

Note that `<group_name>` is an arbitrary name you can choose to refer to the configuration of the script for the particular combination of server, channel, and bot name.

For instance, on my setup, the command looked like:
```
/format_bridge_bot_output_add-server-channel-botnicks-nicklength ocamldiscord freenode #ocaml d_bot 15
```

Finally, setup the regexp for the bot:
```
/format_bridge_bot_output_add-regex <group_name> (?P<action>(?:^[\x01]ACTION |^))<(?P<nick>.+?)> (?P<text>.*)
```

## Note

Fomr what I can tell, this script may not interact as well as desired with other scripts, but the main limitation I saw up to now is that nicks in rewritten messages are not colorized, which is sad, but in my opinion still better than not rewriting the messages.
