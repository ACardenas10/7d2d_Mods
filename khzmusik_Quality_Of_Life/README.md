# Quality Of Life

A collection of small modifications that should make your in-game life more convenient.

These are intended to be modifications that are uncontroversial,
and do not require any custom assets.

* :heavy_check_mark: Server side only (clients do not need to install the mod)
* :heavy_check_mark: EAC safe (clients and servers do not need to disable Easy Anti-Cheat)

## Features

* The "already read book" icon is now a semi-translucent green check mark.
    Inspired by this post on the forums:
    [Mod that lets you know you've already read a book?](https://community.7daystodie.com/topic/24306-mod-that-lets-you-know-youve-already-read-a-book/)
* The time it takes to scrap or smelt brass is reduced by half.
* If you have the required knowledge to craft ammo bundles,
    you can craft them from loose ammo (not just from raw materials).
* Dropped loot bags stick around for 60 (real-time) minutes before despawning.
* Anvils can be scrapped for iron, or smelted in the forge.
* The wood resource no longer makes the wood "grab" or "place" sounds when dragged and dropped.
    No other UI sounds are affected.
    _(New for v1.0.1.0)_
* The "Lock" icon colors have a bit more contrast,
    and the lock/unlock sounds are different.
    _(New for v1.0.1.1)_
* Location name fix for the "White River Citizen" quest to find a trader.
    _(New for v1.0.1.1)_
* Large bushes and hedges give slightly more wood than small, dead bushes.
    _(New for v1.0.1.1)_
* Slight increase in the amount of small rocks spawned on the ground.
    _(New for v1.0.1.1)_

## Technical Details

This modlet uses XPath to modify XML files, and does not require SDX or DMT.
It should be compatible with EAC.
It does _not_ contain any new assets (such as images or models).
Servers should automatically push the XML modifications to their clients, so separate client
installation should _not_ be necessary.

Starting a new game should not be necessary, but is always recommended just in case.

### Ammo Bundles

There are new recipes for all ammo bundles,
where the ammo itself is the required ingredients,
not the raw materials.

These should take exactly as much ammo to craft as they give back.
If players want the raw material bonuses, they have to use the raw materials.

However, the bundles made from ammo also take 2/3 the time to craft.
This seem more "realistic,"
and takes into consideration the time the player may have spent crafting the loose ammo.

### Modifying the _icons_ for read/unread books

It is possible to also change the icons for both unread and already-read books.
If you want to change them, uncomment the relevant XML code in this modlet's `items.xml` file.

The current XML in that file changes the icon for already-read books to a green check mark.
There is also commented-out code to change the icon for unread books to a plus sign.
But you can add any icon(s) you like.

Open `controls.xml`, and look at the "sprite" attribute for this entry in the `item_stack` node:
```xml
<sprite depth="8" name="itemtypeicon" width="24" height="24" sprite="ui_game_symbol_{itemtypeicon}" pos="2,-2" foregroundlayer="true" visible="{hasitemtypeicon}" color="{itemtypeicontint}" />
```

Now, match up the variables (in `{}`) with these properties in the "schematicMaster" item in `items.xml`:
```xml
<property name="ItemTypeIcon" value="book"/>
<property name="AltItemTypeIcon" value="book_read"/>
```

Putting it all together, I found the `ui_game_symbol_check.tga` filename,
stripped out the "ui_game_symbol_" prefix,
and used it as the value of the "AltItemTypeIcon" property.

I did the same for the "ItemTypeIcon" property,
except that I chose the `ui_game_symbol_add.tga` file.
(This is in the code that is commented out.)

There's a list of `ui_game_symbol_{x}` TGA files in the `XML.txt` file.

There is also a table of available icons here:
http://smuggerstech.com/7DTD/Assets/Sprites/

That website is not associated with 7D2D or The Fun Pimps,
so the link might be stale in the future.
