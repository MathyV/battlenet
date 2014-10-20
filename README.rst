battlenet
=====================

Python Library for Blizzard's Community Platform API

Major features
----------------------

* Pythonic
* Unicode normalization
* Lazyloading and eagerloading
* Support locales (en, fr, de, ...)
* Support api/public/private keys

Making a connection
----------------------

Global connection settings can be setup so that objects can make connections implicitly.

::

    from battlenet import Connection

    Connection.setup(
        api_key='your api key',
        public_key='your public key',
        private_key='your private key',
        locale='fr')

You can also create connections explicitly.

::

    from battlenet import Connection

    connection = Connection(
        api_key='your api key',
        public_key='your public key',
        private_key='your private key',
        locale='fr')

Using the api/public/private keys
----------------------------------

You can define your keys via environment variables. For example using a bash shell:

::

    $ export BNET_API_KEY=put-your-api-key-here

More details on the keys on the official battle.net dev website https://dev.battle.net/.

Fetching a specific realm
-------------------------

::

    from battlenet import Realm

    # If a global connection was setup
    realm = Realm(battlenet.UNITED_STATES, 'Nazjatar')

    # Using a specific connection
    realm = connection.get_realm(battlenet.UNITED_STATES, 'Nazjatar')

    print realm.name
    # => Nazjatar

    print realm.is_online()
    # => true

    print realm.type
    # => PVP


Fetching all realms
-------------------------

::

    for realm in connection.get_all_realms(battlenet.UNITED_STATES):
        print realm

Fetching a character
----------------------

::

    from battlenet import Character

    # If a global connection was setup
    character = Character(battlenet.UNITED_STATES, 'Nazjatar', 'Vishnevskiy', fields=[Character.GUILD])

    # Using a specific connection
    character = connection.get_character(battlenet.UNITED_STATES, 'Nazjatar', 'Vishnevskiy', fields=[Character.GUILD])

    print character.name
    # => Vishnevskiy

    print character.guild.name
    # => Excellence


Fetching a guild
----------------------

::

    from battlenet import Guild

    # If a global connection was setup
    guild = Guild(battlenet.UNITED_STATES, 'Nazjatar', 'Excellence')

    # Using a specific connection
    guild = connection.get_guild(battlenet.UNITED_STATES, 'Nazjatar', 'Excellence')

    print guild.name
    # => Excellence

    leader = guild.get_leader()
    print leader.name
    # => Clí

More Examples
----------------------

Read the unit tests inside the tests directory.
