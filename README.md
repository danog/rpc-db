# RPC database

This database contains info about telegram MTProto RPC errors and localized descriptions for said errors.

See [here](https://github.com/danog/telerpc) for the error reporting API.  

[Database JSON available at https://rpc.madelineproto.xyz/core.json &raquo;](https://rpc.madelineproto.xyz/core.json).

Structure:

* `errors` - All error messages and codes for each method (object).
  * Keys: Error codes as strings (numeric strings)
  * Values: All error messages for each method (object)
    * Keys: Error messages (string)
    * Values: An array of methods which may emit this error (array of strings, may be empty for errors that can be emitted by any method)
* `descriptions` - Descriptions for every error mentioned in `errors` (and a few other errors not related to a specific method)
  * Keys: Error messages
  * Values: Error descriptions
* `user_only` - A list of methods that can only be used by users, **not** bots.
* `bot_only` - A list of methods that can only be used by bots, **not** users.
* `business_supported` - A list of methods that can be used by bots over a [business connection with invokeWithBusinessConnection](https://core.telegram.org/api/business).

Error messages and error descriptions may contain `printf` placeholders in key positions, for now only `%d` is used to map durations contained in error messages to error descriptions.

Example:

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