# Hubot: hubot-auth

#### This is a fork that simply contains a merged PR missing from the main repo that makes hubot-auth save roles into the brain and actually persist across reboots instead of clearing them.

(https://github.com/hubot-scripts/hubot-auth/pull/40) 

#### Props to the original authors Alex Williams (http://github.com/aw), alexwilliamsca and tombell and especially the author of the PR/Fix Dario Berzano (https://github.com/dberzano)

#### On NPM at: https://www.npmjs.com/package/hubot-auth-persistent

Assign roles to users and restrict command access in other scripts.


## Installation

Add **hubot-auth-persistent** to your `package.json` file:

```
npm install --save hubot-auth-persistent
```

Add **hubot-auth-persistent** to your `external-scripts.json`:

```json
["hubot-auth-persistent"]
```

Run `npm install`

## Sample Interaction

```
user1>> hubot user2 has jester role
hubot>> OK, user2 has the jester role.
```

## Sample Usage
### Restricting commands
```coffee
module.exports = (robot) ->
  # Command listener
  robot.respond /some command/i, (msg) ->
    role = 'some-role'
    user = robot.brain.userForName(msg.message.user.name)
    return msg.reply "#{name} does not exist" unless user?
    unless robot.auth.hasRole(user, role)
      msg.reply "Access Denied. You need role #{role} to perform this action."
      return
    # Some commandy stuff
    msg.reply 'Command done!'
```
### Example Interaction
```
user2>> hubot some command
hubot>> Access Denied. You need role some-role to perform this action.
user1>> hubot user2 has some-role role
hubot>> OK, user2 has the some-role role.
user2>> hubot some command
hubot>> Command done!
```
