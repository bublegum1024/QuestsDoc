# Доработка Quest API

{% hint style="info" %}
**Предупреждение:** Эта информация пригодится разработчикам. Требуется знание Java!
{% endhint %}

### Добавьте в свой проект

Если вы используете Maven или другой инструмент управления проектами, добавьте последнюю версию Quests через сервис CodeMC.

```xml
<repository>
  <id>codemc-repo</id>
  <url>https://repo.codemc.io/repository/maven-public/</url>
</repository>
```

Если вы не разрабатываете кросс-платформенный проект, вам потребуется задать основной артефакт.

```xml
<dependency>
  <groupId>me.pikamug.quests</groupId>
  <artifactId>quests-core</artifactId>
  <version>VERSION</version>
</dependency>
```

### Изучите интерфейс

Quests предоставляет простой API для создания индивидуальных требований, наград и целей. Для начала убедитесь, что вы компилируете версию 4.0.0 или выше. Закончив следовать этому руководству, используйте папку /Quests/modules в качестве места назначения для готового и скомпилированного jar-файла. При распространении вашего модуля обязательно сообщите конечному пользователю правильное расположение папки.

В следующих примерах предполагается, что вы создаете проект для программного обеспечения на базе Bukkit.

#### Requirements API (API Требований)

Создать требования к квестам очень просто. Для начала создайте класс Java, расширяющий класс CustomRequirement. После этого ознакомьтесь с этим примером специального требования, в котором у игрока должно быть определенное имя, чтобы выполнить квест:

```java
package xyz.janedoe;

import java.util.Map;
import org.bukkit.entity.Player;
import me.pikamug.quests.module.BukkitCustomRequirement;

public class NameRequirement extends BukkitCustomRequirement {
    // Construct the requirement
    public NameRequirement() {
        setName("Name Requirement");
        setAuthor("Jane Doe");
        setItem("NAME_TAG", (short)0);
        addStringPrompt("Name", "Enter value that player's name must contain in order to take the Quest", null);
        addStringPrompt("Case-Sensitive", "Should the check be case-sensitive or not? (Enter \'true\' or \'false\'", null);
	setDisplay("Sorry, you are not on the list.");
    }
    
    // Test whether a player has met the requirement
    @Override
    public boolean testRequirement(Player player, Map<String, Object> data) {
	      String caseSensitive = (String) data.get("Case-Sensitive");
		
	      // Check whether the name must be case-sensitive
	      if (caseSensitive.equalsIgnoreCase("true")) {
	          // Mark the requirement as satisfied if name matches
	          return player.getName().contains((String)data.get("Name"));
	      } else {
	          // Mark the requirement as satisfied if name matches, ignoring case
	          return player.getName().toLowerCase().contains(((String)data.get("Name")).toLowerCase());
	      }
    }
}
```

В конструкторе вашего класса вы можете использовать любой из следующих методов:

| Метод           | Описание                                                                                                                                                                                                          |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| setName         | Устанавливает имя пользовательского требования.                                                                                                                                                                   |
| setAuthor       | Устанавливает автора пользовательского требования (вас!).                                                                                                                                                         |
| setItem         | Устанавливает элемент, который будет отображаться в интерфейсных плагинах, таких как QuestsGUI.                                                                                                                   |
| setDisplay      | Устанавливает способ отображения требования в случае, если проверка неудачна.                                                                                                                                     |
| addStringPrompt | Добавляет новое приглашение с указанным заголовком, описанием и значением по умолчанию для вашего пользовательского требования. Создатели квестов смогут ввести строку, которую вы затем можете проанализировать. |

Внутри #testRequirement вы выполняете свою логику, чтобы определить, соответствует ли игрок требованию, и возвращаете true, если он соответствует, или false, если нет.

Карта данных содержит данные, которые ей передал тот, кто создал квест. В этом примере карта данных содержит два значения: 'Name' и 'Case-Sensitive'. Также обратите внимание, что хотя значения имеют тип Object, внутри они были приведены к типу String. Вам необходимо выполнить преобразование типов вручную, если вы хотите получить целые числа, логические значения и т. д.

#### Rewards API (API Наград)

Создать награду за квесты очень просто. Для начала создайте класс Java, расширяющий класс CustomReward. После этого посмотрите на этот пример пользовательской награды, где игрок получает открытый инвентарь, содержащий железо, золото и алмазы:

```java
package xyz.janedoe;

import java.util.Map;

import org.bukkit.Bukkit;
import org.bukkit.Material;
import org.bukkit.entity.Player;
import org.bukkit.inventory.Inventory;
import org.bukkit.inventory.ItemStack;

import me.pikamug.quests.module.BukkitCustomReward;

import java.util.UUID;

public class LootReward extends BukkitCustomReward {
    // Construct the reward
    public LootReward() {
        setName("Loot Reward");
        setAuthor("Jane Doe");
        setItem("CHEST", (short)0);
        setDisplay("Loot Chest: %Title%");
        addStringPrompt("Title", "Title of the loot inventory interface.", null);
        addStringPrompt("NumIron", "Enter the number of iron ingots to give in the loot chest.", null);
        addStringPrompt("NumGold", "Enter the number of gold ingots to give in the loot chest.", null);
        addStringPrompt("NumDiamond", "Enter the number of diamonds to give in the loot chest.", null);
    }
    
    // Give loot reward to a player
    @Override
    public void giveReward(UUID uuid, Map<String, Object> data) {
        final Player player = Bukkit.getPlayer(uuid);
        if (player == null) {
            Bukkit.getLogger().severe("Player was null for UUID " + uuid);
            return;
        }
        String title = (String) data.get("Title");
        int numIron = 0;
        int numGold = 0;
        int numDiamond = 0;
        
        // Attempt to load user input as integers
        try {
            numIron = Integer.parseInt((String) data.get("NumIron"));
        } catch (NumberFormatException nfe) {
        	Bukkit.getLogger().severe("Loot Reward has invalid Iron number: " + numIron);
        }
        try {
            numGold = Integer.parseInt((String) data.get("NumGold"));
        } catch (NumberFormatException nfe) {
        	Bukkit.getLogger().severe("Loot Reward has invalid Gold number: " + numGold);
        }
        try {
            numDiamond = Integer.parseInt((String) data.get("NumDiamond"));
        } catch (NumberFormatException nfe) {
        	Bukkit.getLogger().severe("Loot Reward has invalid Diamond number: " + numDiamond);
        }
        
        // Create a temporary inventory to add items to
        Inventory inv = Bukkit.getServer().createInventory(player, 3, title);
        int slot = 0;

        // Check if amount is greater than default value
        if (numIron > 0) {
            // Add item to current slot in temporary inventory, then get next slot ready
            inv.setItem(slot, new ItemStack(Material.IRON_INGOT, numIron > 64 ? 64 : numIron));
            slot++;
        }
        if (numGold > 0) {
            inv.setItem(slot, new ItemStack(Material.GOLD_INGOT, numGold > 64 ? 64 : numGold));
            slot++;
        }
        if (numDiamond > 0) {
            inv.setItem(slot, new ItemStack(Material.DIAMOND, numDiamond > 64 ? 64 : numDiamond));
        }
        
        // Open temporary inventory for player to accept items
        player.openInventory(inv);
    }
}
```

В конструкторе вашего класса вы можете использовать любой из следующих методов:

| Метод           | Описание                                                                                                                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| setName         | Устанавливает имя пользовательской награды.                                                                                                                                                                  |
| setAuthor       | Устанавливает автора пользовательской награды (вас!).                                                                                                                                                        |
| setItem         | Устанавливает элемент, который будет отображаться в интерфейсных плагинах, таких как QuestsGUI.                                                                                                              |
| setDisplay      | Устанавливает имя награды (текст, который появится, когда игрок завершит квест) для пользовательской награды.                                                                                                |
| addStringPrompt | Добавляет новое приглашение с указанным заголовком, описанием и значением по умолчанию для вашей пользовательской награды. Создатели квестов смогут ввести строку, которую вы затем можете проанализировать. |


Внутри #giveReward вы выполняете свою логику, чтобы дать игроку все, что дает ваша специальная награда. Карта данных содержит данные, которые ей передал тот, кто создал квест. В этом примере карта данных содержит четыре значения: одно для заголовка графического интерфейса и три для количества железа/золота/алмазов. Также обратите внимание, что хотя значения имеют тип Object, внутри они были приведены к типу String. Вам необходимо выполнить преобразование типов вручную, если вы хотите получить целые числа, логические значения и т. д.

#### Objectives API (API Целей)

Building a Quests Objective is a bit more complicated than Requirements or Rewards. To get started, create a Java class that extends the CustomObjective class. If you want to catch one of Bukkit's Events, you'll need to implement the Listener class (Quests will take care of registering it for you). After that, check out these examples of a Custom Objective:

{% tabs %}
{% tab title="Example 1" %}
```java
// Player must gain a certain amount of experience to advance

package xyz.janedoe;

import me.pikamug.quests.module.BukkitCustomObjective;
import me.pikamug.quests.Quest;
import me.pikamug.quests.Quests;

import org.bukkit.Bukkit;
import org.bukkit.event.EventHandler;
import org.bukkit.event.player.PlayerExpChangeEvent;

public class ExperienceObjective extends BukkitCustomObjective {
    // Get the Quests plugin
    Quests qp = (Quests) Bukkit.getServer().getPluginManager().getPlugin("Quests");
	
    // Construct the objective
    public ExperienceObjective() {
        setName("Experience Objective");
        setAuthor("Jane Doe");
        setItem("BOOK", (short)0);
        setShowCount(true);
        setCountPrompt("Enter the experience points that the player must acquire:");
        setDisplay("Acquire experience points: %count%");
    }

    // Catch the Bukkit event for a player gaining/losing exp
    @EventHandler
    public void onPlayerExpChange(PlayerExpChangeEvent evt) {
        // Make sure to evaluate for all of the player's current quests
        for (Quest quest : qp.getQuester(evt.getPlayer().getUniqueId()).getCurrentQuests().keySet()) {
            // Check if the player gained exp, rather than lost
            if (evt.getAmount() > 0) {
                // Add to the objective's progress, completing it if requirements were met
                incrementObjective(evt.getPlayer(), this, evt.getAmount(), quest);
            }
        }
    }
}
```
{% endtab %}

{% tab title="Example 2" %}
```java
// Require the player to drop a certain number of a certain type of item.

package xyz.janedoe;

import me.pikamug.quests.module.BukkitCustomObjective;
import me.pikamug.quests.Quest;
import me.pikamug.quests.Quests;

import org.bukkit.Bukkit;
import org.bukkit.entity.EntityType;
import org.bukkit.event.EventHandler;
import org.bukkit.event.player.PlayerDropItemEvent;
import org.bukkit.inventory.ItemStack;

public class DropItemObjective extends BukkitCustomObjective {
    // Get the Quests plugin
    Quests qp = (Quests) Bukkit.getServer().getPluginManager().getPlugin("Quests");

    // Construct the objective
    public DropItemObjective() {
        setName("Drop Item Objective");
        setAuthor("Jane Doe");
        setItem("ANVIL", (short)0);
        setShowCount(true);
        setCountPrompt("Enter the amount that the player must drop:");
        setDisplay("Drop %Item Name%: %count%");
        addStringPrompt("Item Name", "Enter the name of the item that the player must drop", "DIRT");
    }

    // Catch the Bukkit event for a player dropping an item
    @EventHandler
    public void onPlayerDropItem(PlayerDropItemEvent evt){
    	// Make sure to evaluate for all of the player's current quests
    	for (Quest quest : qp.getQuester(evt.getPlayer().getUniqueId()).getCurrentQuests().keySet()) {
    	    Map<String, Object> map = getDataForPlayer(evt.getPlayer(), this, quest);
	    if (map == null) {
	        continue;
            }
            ItemStack stack = evt.getItemDrop().getItemStack();
            String userInput = (String) map.get("Item Name");
            EntityType type = EntityType.fromName(userInput);
            // Display error if user-specified item name is invalid
            if (type == null) {
            	Bukkit.getLogger().severe("Drop Item Objective has invalid item name: " + userInput);
            	continue;
            }
            // Check if the item the player dropped is the one user specified
            if (evt.getItemDrop().getItemStack().getType().equals(type)) {
    		// Add to the objective's progress, completing it if requirements were met
            	incrementObjective(evt.getPlayer(), this, stack.getAmount(), quest);
            }
    	}
    }
}
```
{% endtab %}

{% tab title="Example 3" %}
```java
// Allow player to break ANY block rather than a specific one

package xyz.janedoe;

import me.pikamug.quests.module.BukkitCustomObjective;
import me.pikamug.quests.Quest;
import me.pikamug.quests.Quests;

import org.bukkit.Bukkit;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.EventPriority;
import org.bukkit.event.block.BlockBreakEvent;

public class AnyBreakBlockObjective extends BukkitCustomObjective {
    // Get the Quests plugin
    private static Quests quests = (Quests) Bukkit.getServer().getPluginManager().getPlugin("Quests");
    
    public AnyBreakBlockObjective() {
        setName("Break Blocks Objective");
        setAuthor("Jane Doe");
        setItem("DIRT", (short)0);
        setShowCount(true);
        addStringPrompt("Obj Name", "Set a name for the objective", "Break ANY block");
        setCountPrompt("Set the amount of blocks to break");
        setDisplay("%Obj Name%: %count%");
    }
    
    @EventHandler(priority = EventPriority.LOW)
    public void onBlockBreak(BlockBreakEvent event) {
        Player player = event.getPlayer();
        for (Quest q : quests.getQuester(player.getUniqueId()).getCurrentQuests().keySet()) {
            incrementObjective(player, this, q, 1);
            return;
        }
    }
}
```
{% endtab %}
{% endtabs %}

In the constructor of your class, you may use any of the following methods:

| Метод           | Описание                                                                                                                                                                                                                                                                                                              |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| setName         | Устанавливает имя пользовательской цели.                                                                                                                                                                                                                                                                              |
| setAuthor       | Устанавливает автора пользовательской цели (вас!).                                                                                                                                                                                                                                                                    |
| setItem         | Устанавливает элемент, который будет отображаться в интерфейсных плагинах, таких как QuestsGUI.                                                                                                                                                                                                                       |
| setShowCount    | Устанавливает, может ли создатель квеста устанавливать счетчик (количество раз, которое игрок может повторить задание). По умолчанию установлено «истина». _Это будет применяться ко всем запросам, добавленным с помощью #addStringPrompt, кроме отключенных._                                                       |
| setCountPrompt  | Задает описание подсказки, позволяющей пользователю ввести счетчик для цели. По умолчанию "Введите число".                                                                                                                                                                                                            |
| setDisplay      | Устанавливает способ отображения цели в списке /quests и журнале квестов. Для заполнителей используйте `%count%`, чтобы получить значение #setShowCount, и заголовки #addStringPrompt для пользовательского ввода (например, `%Item Name%` во втором примере). По умолчанию установлено значение "Прогресс: %count%". |
| addStringPrompt |Добавляет новое приглашение с указанным заголовком, описанием и значением по умолчанию для вашей пользовательской цели. Создатели квестов смогут ввести строку, которую вы затем можете проанализировать.                                                                                                              |

Внутри обработчиков событий (если применимо) определите, выполнил ли игрок часть или всю цель, а затем используйте #incrementObjective для продвижения игрока. Первым и вторым аргументом #incrementObjective всегда должны быть игрок и 'this' соответственно. Третий аргумент — насколько увеличить цель, а последний — квест, к которому можно применить приращение. Даже если ваша цель не имеет счетчика, вы все равно должны использовать #incrementObjective — используйте приращение 1, чтобы сигнализировать о том, что цель достигнута.

Карта `Map<String, Object>` содержит данные, предоставленные редактором квестов. В этом примере ключи данных — это имена элементов, тогда как значения — это вводимые пользователем данные для вашего приглашения (которые _могут_ быть null). Также обратите внимание, что хотя значения имеют тип Object, внутри они были приведены к типу String. Вам необходимо выполнить преобразование типов вручную, если вы хотите получить целые числа, логические значения и т. д.
