# LotoManager
Manages loto in your code, for MySQL databases, it's made for discord, but you can use it in any code.

## Important informations
This manager can handle loto, but end is manual.

This handler can handle **loto with numbers only**, it means that the reward **must** be an integer, because it's splited between all winners.

## Database
To use the manager, you first have to create the database table.

1. Take the command in [loto.sql](./loto.sql)
2. Put it in your SQL command prompt
3. Table is created !

## Create manager
```js
const Discord = require('discord.js');
const mysql = require('mysql');
const token = "your token";

const lotoManager = require('LotoManager.js');

const client = new Discord.Client({ 
    intents: [  ]
});

// here connect your database
const db = new mysql.createConnection({ 
    database: 'db',
    user: 'user',
    password: "password",
    host: 'host'
});
client.login(token)

db.connect(async err => {
    if (err) throw err;

    const manager = new lotoManager(db);
    manager.init();

    // Manager is ready !
});
```

## Methods
Here are listed all methods that you can use

#### Start
Start a loto
```js
manager.start({
    numbers: 'number of numbers that you want in the loto',
    complementaries: 'number of complementaries that you want in the loto',
    guildId: 'id of the guild',
    reward: 10000,
    time: 120000
});
```

It returns nothing, but make your bot crash if there is an error with the db

#### Participate
Participate to the current loto

```js
manager.addParticipation({
    guildId: 'id of the guild',
    userId: 'user id',
    numbers: [84, 51, 65, 98, 11], // The amount of numbers must be the same than declared in the .start() method
    complementaries: [72, 44], // The amount of complementary numbers must be the same than declared in the .start() method
})
```

###### Returns
The potentials returns of this method are listed here :
* invalid loto
* invalid numbers
* invalid arrays
* invalid compared
* user already exists
* added

#### End
End the current loto

```js
manager.end('guild id');
```

###### Returns
The potentials returns of this method are listed here :
* invalid loto
* an array with all the winner's data

## Good usage
You can now use the Greensky's loto manager, it's free to use.

## Contact
If you get any error, contact me on [this discord server](https://discord.gg/fHyN5w84g6)
