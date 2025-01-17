# Action Editor

{% hint style="info" %}
**Notice:** This information is intended for intermediate users. Read carefully!
{% endhint %}

Similar to how all quest stages have objectives, they can also perform actions. An action is something that happens during a stage, but is typically cosmetic and doesn't inherently progress the quest. For example, causing a player to lose hunger or get struck by lightning are considered actions.

To make an action, run **/quests actions** in-game (or from the console, with limited features). You will be greeted with the following:

![](../.gitbook/assets/action\_editor.png)

Enter '1' in chat so the plugin may prompt you to enter a name for your action. This can be any alphanumeric sequence, which means letters and numbers are OK, but no special characters or symbols! Don't worry, you can change it later if you're unsure.

After you've chosen a valid name, this screen will appear:

![](../.gitbook/assets/action\_main.png)

<details>

<summary>Expand to see the breakdown.</summary>

1. Change the name of your action
2. Send message, clear inventory, give items, apply potion effects, set hunger level, set saturation level, teleport to location, or execute commands
3. Set time to fail quest and whether to cancel the quest timer
4. Set effects or set explosion locations
5. Set storm or thunder in a particular world, or set lightning strike locations
6. Action to spawn mobs
7. Run a [Denizen](https://pikamug.gitbook.io/quests/beginner/dependencies#denizen) script
8. Action to fail the quest
9. Finish working on your action
10. Discard all work on your action

</details>

For now, enter '5' for the Weather menu, then '2' to set up an action which will force thunder across a world for a while.

![](../.gitbook/assets/action\_thunder.png)

Input '1' to select one of your Minecraft server's worlds by name. They will be listed for your convenience, but you can only select one! You may create a second action later if you wish to deal out thunder across multiple worlds.

Once that's done, enter '2' to set a duration of time in seconds. This is how long your thunder action will last for. As an example, type in 180 for the event to last 3 minutes. Now, enter all the appropriate prompt numbers for 'Done' until you've saved your action.

Nice job! Unlike the [Quest Editor](../setup/quests-editor.md), there is no need to reload the plugin. Exit the Action Editor and then create or edit a quest in the Quests Editor. Go to the 'Edit Stages' menu and, after setting at least one objective, select option 9 to run the action before, during, or after the stage:

![](../.gitbook/assets/action\_quest.png)

<details>

<summary>Expand to see the breakdown.</summary>

1. Activate on start of stage
2. Activate at end of stage
3. Activate if player fails quest
4. Activate if player dies during stage
5. Activate if player disconnects during stage
6. Activate if chat message sent during stage
7. Activate if command run during stage
8. Save and return to previous menu

</details>

Chat and command actions are run during the stage when the player enters a specific keyword or command in-game, respectively.
