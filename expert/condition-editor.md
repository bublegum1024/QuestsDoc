# Condition Editor

{% hint style="info" %}
**Warning:** This information is intended for advanced users. Proceed with caution!
{% endhint %}

When a player is carrying out a stage of a quest, it may be desirable to force them to meet a certain criteria. For example, holding a specific item while completing objectives. To do this, a condition must be created and applied.

To make a condition, run **/quests conditions** in-game (or from the console, with limited features). You will be greeted with the following:

![](https://camo.githubusercontent.com/7c7cf8db7760543f731b49ec61ef1651886830e96b79c7ce4afb6741f53bb7dc/68747470733a2f2f692e696d6775722e636f6d2f6c7148626f4b492e706e67)

Enter '1' in chat so the plugin may prompt you to enter a name for your condition. This can be any alphanumeric sequence, which means letters and numbers are OK, but no special characters or symbols! Don't worry, you can change it later if you're unsure.

After you've chosen a valid name, this screen will appear:

![](https://camo.githubusercontent.com/23267d859c71ffcb3cd6f4123060c813a2d75817eb8c8a1f535f17c7f4fc2338/68747470733a2f2f692e696d6775722e636f6d2f455379363872492e706e67)

<details>

<summary>Expand to see the breakdown.</summary>

1. Change the name of your condition
2. Ride an entity or [Citizens](https://pikamug.gitbook.io/quests/beginner/dependencies#citizens) NPC
3. Own permission, hold item in main hand, or wear items as armor
4. Stay within world, stay within ticks, stay within biome, or stay within [WorldGuard](https://pikamug.gitbook.io/quests/beginner/dependencies#worldguard) region
5. Whether placeholder value is true
6. Whether to fail quest if condition not met
7. Finish working on your condition
8. Discard all work on your condition

</details>

Select a condition type and decide whether the player should fail the quest if said condition is not met. Now, enter all the appropriate prompt numbers for 'Done' until you've saved your condition.

Nice job! Unlike the Quests Editor, there is no need to reload the plugin. Exit the Condition Editor and then create or edit a quest in the Quests Editor. Go to the 'Edit Stages' menu and, after setting at least one objective, select option 11 to apply the condition.
