# Modules

{% hint style="info" %}
**Notice:** This information is intended for intermediate users. Read carefully!
{% endhint %}

Plugins which integrate with Quests to provide Custom Objectives, Rewards and Requirements, use what are known as _modules_. A module is a jar file created by developers using the [Quests API](https://github.com/PikaMug/Quests/wiki/Master-%E2%80%90-Custom-Quest-API), which acts as a middleman between Quests and the integrating plugin. This is in contrast to a [dependency](https://github.com/PikaMug/Quests/wiki/Beginner-%E2%80%90-Dependencies), which you typically do not need a module for.

Module jars must be placed in the _Quests/modules_ folder, while the target plugin goes in the _/plugins_ folder as usual. Note that all modules are entirely optional and you may add or remove them as seen fit. Below is an incomplete list of popular plugins for which a module is known to exist, along with a description of how it links.

| Labels: |  |
| :--- | :--- |
| 🌟 = Recommended for optimal user experience | 💲 = May require purchase of premium resource |

### Boss 💲

![](https://camo.githubusercontent.com/53192d923a6add754608ffd62dae992b9963ebbc72635ac313027ea8dd0632e9/68747470733a2f2f692e696d6775722e636f6d2f68793653754b392e706e67)

Adds a "Kill Boss" objective. Requires Boss 3.1.0 or greater.

* Quests 3.6.0 and above: [Click here](https://www.spigotmc.org/resources/boss-quests-module.66973/)

### CustomMobs

![](https://camo.githubusercontent.com/6029eb00543fc07c423a8818389bb53d679c4be330064631bc7d8aa2d0d1a86a/68747470733a2f2f692e696d6775722e636f6d2f79446e32704c632e706e67)

Adds a "Kill CustomMobs" objective.

* Quests 3.6.0 and above: [Click here](https://www.spigotmc.org/resources/custommobs-quests-module.56686/)
* Quests 3.2.7 to 3.5.9: [Click here](https://www.spigotmc.org/resources/custommobs-quests-module.56686/download?version=232903)
* Quests 3.2.6 and below: [Click here](https://www.spigotmc.org/resources/custommobs-quests.25679/)

### DungeonsXL

![](https://camo.githubusercontent.com/70fecf6dfd0399b3a64f8a16d94dd3d7cf928178d92c9f180a7f3345117fdc78/687474703a2f2f65726574686f6e2e64652f7265736f75726365732f6c6f676f732f44756e67656f6e73584c2e706e67)

Adds "Finish dungeon", "Get reward item", "Get reward level", "Get reward money", and "Kill dungeon mob" objectives.

* Quests 3.6.0 and above: [Click here](https://www.spigotmc.org/resources/dungeonsxl-quests-module.66703/)

### Magic

![](https://camo.githubusercontent.com/d9ef4d8eb088489debd7f72e65cbf67f6a682f9c3d36e41a4b3a3747b635ab92/68747470733a2f2f692e696d6775722e636f6d2f453155344361522e706e67)

Link with various Magic spells and tasks.

* Quests 3.6.0 and above: [Click here](http://jenkins.elmakers.com/job/MagicQuests/)
* Quests 3.2.7 to 3.5.9: [Click here](http://jenkins.elmakers.com/job/MagicQuests/90/)
* Quests 3.2.6 and below: [Click here](http://jenkins.elmakers.com/job/MagicQuests/88/)

### mcMMO Overhaul 💲

![](https://camo.githubusercontent.com/8f19026fc09827670ad5f270b6865286c135f18de8400bd3de55402fd49a165f/68747470733a2f2f692e696d6775722e636f6d2f655575427247522e706e67)

Adds "Skill" reward and requirement. For the older mcMMO Classic, use [this dependency](https://github.com/PikaMug/Quests/wiki/Beginner-%E2%80%90-Dependencies#mcmmo-classic) instead.

* Quests 2.1.0 and above: [Click here](https://www.spigotmc.org/resources/mcmmo-overhaul-quests-module.69548/)

### MobArena

![](https://camo.githubusercontent.com/c0d2e237c6293ada28cce473aa0578a0246f045ec75ed26a38054d8b6564f034/68747470733a2f2f692e696d6775722e636f6d2f733874715944702e706e67)

Adds "Kill mobs", "Finish wave", and "Complete arena" objectives.

* Quests 3.6.0 and above: [Click here](https://www.spigotmc.org/resources/mobarena-quests-module.72355/)

### MythicMobs 🌟

![](https://camo.githubusercontent.com/aebb3e692cec287e8baddc103a16e47bfb986dd861678a461e799e7cf240ebfc/68747470733a2f2f692e696d6775722e636f6d2f7a6c776f31304c2e706e67)

Adds "Kill MythicMobs" and "MythicItem NPC Deliver" objectives, a "MythicItem" reward, and a "MythicItem" requirement.

* Quests 3.6.0 and above: [Click here](https://mc.hackerzlair.org/jenkins/job/MythicMobsQuests/)
* Quests 3.2.7 to 3.5.9: [Click here](https://github.com/BerndiVader/MythicMobsQuestsModule/blob/a346d24545e874587c0895b30b369492978f6f81/MythicMobsQuests.jar)
* Quests 3.2.6 and below: [Click here](https://github.com/BerndiVader/MythicMobsQuestsModule/blob/edd5df5968628c06e5670c0e2a1c19ca41a86467/MythicMobsQuests285.jar)

### NPCDestinations

![](https://camo.githubusercontent.com/5703b4f519542e8fe21a9296a5a0c291744b13b0be8547b450baa729c1f6669a/68747470733a2f2f692e696d6775722e636f6d2f59504942596b462e706e67)

{% hint style="info" %}
**Warning:** Module is auto-installed and cannot be disabled without removing NPCDestinations!
{% endhint %}

Adds NPC location requirement and reward.

* Quests 3.9.5 and above: [Click here](https://www.spigotmc.org/resources/npcdestinations-create-living-npcs.13863/)

### Want support for other plugins or features?

If you can't find a module for a particular purpose here or via Internet search, consider hiring a developer at one of these sites:

* [Quests Community](https://discordapp.com/invite/QdJAv2G7qg)
* [SpigotMC](https://www.spigotmc.org/forums/hiring-developers.55/)
* [Lectern](https://lectern.namelesshosting.com/forum/view/14-requesting/)

Quests is not sponsored by any of the sites above. Neither Quests nor its contributors hold any responsibility for the quality and/or functionality of third-party modules, implied or otherwise, regardless of origin.
