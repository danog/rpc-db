# RPC database

This database contains info about telegram MTProto RPC errors and localized descriptions for said errors.

See [here](https://github.com/danog/telerpc) for the error reporting API.  

[Database JSON available at https://rpc.madelineproto.xyz/core.json &raquo;](https://rpc.madelineproto.xyz/core.json).

Structure:

```json
{
    "errors": {
        "420": {
            "2FA_CONFIRM_WAIT_%d": [
                "account.deleteAccount"
            ],
            "SLOWMODE_WAIT_%d": [
                "messages.forwardMessages",
                "messages.sendInlineBotResult",
                "messages.sendMedia",
                "messages.sendMessage",
                "messages.sendMultiMedia"
            ]
        }
    },
    "descriptions": {
        "2FA_CONFIRM_WAIT_%d": "Since this account is active and protected by a 2FA password, we will delete it in 1 week for security purposes. You can cancel this process at any time, you'll be able to reset your account in %d seconds.",
        "SLOWMODE_WAIT_%d": "Slowmode is enabled in this chat: wait %d seconds before sending another message to this chat.",
        "FLOOD_WAIT_%d": "Please wait %d seconds before repeating the action."
    },
    "user_only": [
        "account.deleteAccount"
    ],
    "bot_only": [
        "messages.setInlineBotResults"
    ],
    "business_supported": [
        "messages.sendMessage"
    ]
}
```