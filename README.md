# CMPM121 Code Smells

Duplicated Code: Seamus

Mysterious Name: Evan

A **Code Smell** is a surface indication that usually corresponds to coding malpractices and to the trained eye, can be detected instantly.

## Mysterious Name

### Introduction

One of the most important parts of coding clearly is coming up with good names that communicate what they do to us and others. As we code independently, it can be easy to come up with names for variables and functions that only make sense to us. Its important to think about others when you code, Fowler suggests that keeping code "mundane and clear" is vital to clearly communicating what your code does and how to use it properly.

### Code Example (From Clicker D1 Project!):

Here, its not clear what button1 really does, changing it to "mainbutton" might be more clear to suggest its purpose of incrementing "counter" to users.

Before: 
```typescript
const button1 = document.createElement("button");
button1.className = "button";
button1.id = "Increment";
button1.textContent = "Spin Me!";
Object.assign(button1.style, {
  width: "80px",
  height: "80px",
  borderRadius: "50%",
  border: "none",
  cursor: "pointer",
});
```

After: 
```typescript
const mainbutton = document.createElement("button");
mainbutton.className = "button";
mainbutton.id = "Increment";
mainbutton.textContent = "Spin Me!";
Object.assign(mainbutton.style, {
  width: "80px",
  height: "80px",
  borderRadius: "50%",
  border: "none",
  cursor: "pointer",
});
```
The **Mysterious Name** smell looks the same across all coding languages. Look for "let" or "const" in js/ts before variables to spot potential Mysterious Names. In C, look for data types being assigned to variables to spot this smell. Once you spot a Mysterious Name, change it to a mundane and clear name.

## Duplicated Code

### Introduction

Often times when coding you will find sections of code that resemble eachother or are identical. Fowler states that when you find such cases, your code will always be better if you can find a way to unify them. When unifying, you must find all examples of the repeated code and figure out any differences that might be between them in order to unify. Once done, your code could be much shorter and easier to read.

### Prevention and Refactoring

The simplest case of finding and fixing a duplicated code smell is if you have the same expression in two methods of the same class. In that case, one can use the Extract Function method that Fowler describes in chapter 6. However, if you have statements that are similar but not identical Fowler suggests using the Slide Statement method to rearrange the code into its identical sections and then extract those.

### Code Example

Before:
```javascript
waveOne() {
        let my = this.my

        if (my.shieldenemyRed1) {
            my.shieldenemyRed1.destroy();
            my.shieldenemyRed1 = null;
        }
        if (my.shieldenemyRed2) {
            my.shieldenemyRed2.destroy();
            my.shieldenemyRed2 = null;
        }
        if (my.bowenemyYellow1) {
            my.bowenemyYellow1.destroy();
            my.bowenemyYellow1 = null;
        }
        if (my.bowenemyYellow2) {
            my.bowenemyYellow2.destroy();
            my.bowenemyYellow2 = null;
        }

        this.enemiesRemaining = 4;

        //Shield Enemy 1
        this.my.sprite.SquareRed1 = this.add.sprite(0, 0, "shieldEnemyRed");
        this.my.shieldenemyRed1 = this.add.container(this.enemyX, this.enemyY, [this.my.sprite.SquareRed1])
        let Helmet1 = this.add.sprite(0,-25, "Helmet");
        this.my.sprite.Helmet1 = Helmet1;
        let Shield1 = this.add.sprite(+15,+10, "Shield").setScale(.5);
        this.my.shieldenemyRed1.add([Helmet1, Shield1]);
        this.my.shieldenemyRed1.visible = true;

        this.shield1PathProgress = 0;

        // this.shieldEnemies.add(this.my.shieldenemyRed1);

        this.timesShieldHit1 = 0;
        this.shieldJustHit1 = false;

        //Shield Enemy 2
        this.my.sprite.SquareRed2 = this.add.sprite(0, 0, "shieldEnemyRed");
        my.shieldenemyRed2 = this.add.container(this.enemyX, this.enemyY, [this.my.sprite.SquareRed2])
        let Helmet2 = this.add.sprite(0,-25, "Helmet");
        this.my.sprite.Helmet2 = Helmet2;
        let Shield2 = this.add.sprite(+15,+10, "Shield").setScale(.5);
        this.my.shieldenemyRed2.add([Helmet2, Shield2]);
        my.shieldenemyRed2.visible = true;

        this.shield2PathProgress = 0;

        // this.shieldEnemies.add(this.my.shieldenemyRed2);

        this.timesShieldHit2 = 0;
        this.shieldJustHit2 = false;

        //Bow Enemy 1
        let Bow1 = this.add.sprite(+15,+10, "Bow").setOrigin(.1,.5);
        let YellowHand1 = this.add.sprite(+15,+10, "YellowHand").setOrigin(.1,.5);
        this.my.sprite.Bow1 = Bow1;
        this.my.sprite.YellowHand1 = YellowHand1;
 
        this.my.sprite.OvalYellow1 = this.add.sprite(0, 0, "OvalYellow");
        my.bowenemyYellow1 = this.add.container(this.shieldX, this.shieldY, [this.my.sprite.OvalYellow1])
        this.my.bowenemyYellow1.add([Bow1, YellowHand1]);

        this.bow1PathProgress = 0;

        // this.bowEnemies.add(this.my.bowenemyYellow1);

        this.timesBowHit1 = 0;
        this.justBowHit1 = false;


        //Bow Enemy 2
        let Bow2 = this.add.sprite(+15,+10, "Bow").setOrigin(.1,.5);
        let YellowHand2 = this.add.sprite(+15,+10, "YellowHand").setOrigin(.1,.5);
        this.my.sprite.Bow2 = Bow2;
        this.my.sprite.YellowHand2 = YellowHand2;
 
        this.my.sprite.OvalYellow2 = this.add.sprite(0, 0, "OvalYellow");
        my.bowenemyYellow2 = this.add.container(this.shieldX, this.shieldY, [this.my.sprite.OvalYellow2])
        this.my.bowenemyYellow2.add([Bow2, YellowHand2]);

        this.bow2PathProgress = 0;

        // this.bowEnemies.add(this.my.bowenemyYellow2);

        this.timesBowHit2 = 0;
        this.justBowHit2 = false;
    }


    waveTwo() {
        let my = this.my

        if (my.shieldenemyRed1) {
            my.shieldenemyRed1.destroy();
            my.shieldenemyRed1 = null;
        }
        if (my.shieldenemyRed2) {
            my.shieldenemyRed2.destroy();
            my.shieldenemyRed2 = null;
        }
        if (my.shieldenemyRed3) {
            my.shieldenemyRed3.destroy();
            my.shieldenemyRed3 = null;
        }
        if (my.bowenemyYellow1) {
            my.bowenemyYellow1.destroy();
            my.bowenemyYellow1 = null;
        }
        if (my.bowenemyYellow2) {
            my.bowenemyYellow2.destroy();
            my.bowenemyYellow2 = null;
        }
        if (my.bowenemyYellow3) {
            my.bowenemyYellow3.destroy();
            my.bowenemyYellow3 = null;
        }

        this.enemiesRemaining = 6;

        //Shield Enemy 1
        this.my.sprite.SquareRed1 = this.add.sprite(0, 0, "shieldEnemyRed");
        this.my.shieldenemyRed1 = this.add.container(this.enemyX, this.enemyY, [this.my.sprite.SquareRed1])
        let Helmet1 = this.add.sprite(0,-25, "Helmet");
        this.my.sprite.Helmet1 = Helmet1;
        let Shield1 = this.add.sprite(+15,+10, "Shield").setScale(.5);
        this.my.shieldenemyRed1.add([Helmet1, Shield1]);
        this.my.shieldenemyRed1.visible = true;

        this.shield1PathProgress = 0;

        // this.shieldEnemies.add(this.my.shieldenemyRed1);

        this.timesShieldHit1 = 0;
        this.shieldJustHit1 = false;

        //Shield Enemy 2
        this.my.sprite.SquareRed2 = this.add.sprite(0, 0, "shieldEnemyRed");
        my.shieldenemyRed2 = this.add.container(this.enemyX, this.enemyY, [this.my.sprite.SquareRed2])
        let Helmet2 = this.add.sprite(0,-25, "Helmet");
        this.my.sprite.Helmet2 = Helmet2;
        let Shield2 = this.add.sprite(+15,+10, "Shield").setScale(.5);
        this.my.shieldenemyRed2.add([Helmet2, Shield2]);
        my.shieldenemyRed2.visible = true;

        this.shield2PathProgress = 0;

        // this.shieldEnemies.add(this.my.shieldenemyRed2);

        this.timesShieldHit2 = 0;
        this.shieldJustHit2 = false;

        //Shield Enemy 3
        this.my.sprite.SquareRed3 = this.add.sprite(0, 0, "shieldEnemyRed");
        my.shieldenemyRed3 = this.add.container(this.enemyX, this.enemyY, [this.my.sprite.SquareRed3])
        let Helmet3 = this.add.sprite(0,-25, "Helmet");
        this.my.sprite.Helmet3 = Helmet3;
        let Shield3 = this.add.sprite(+15,+10, "Shield").setScale(.5);
        this.my.shieldenemyRed3.add([Helmet3, Shield3]);
        my.shieldenemyRed3.visible = true;

        this.shield3PathProgress = .5;

        // this.shieldEnemies.add(this.my.shieldenemyRed2);

        this.timesShieldHit3 = 0;
        this.shieldJustHit3 = false;

        //Bow Enemy 1
        let Bow1 = this.add.sprite(+15,+10, "Bow").setOrigin(.1,.5);
        let YellowHand1 = this.add.sprite(+15,+10, "YellowHand").setOrigin(.1,.5);
        this.my.sprite.Bow1 = Bow1;
        this.my.sprite.YellowHand1 = YellowHand1;
 
        this.my.sprite.OvalYellow1 = this.add.sprite(0, 0, "OvalYellow");
        my.bowenemyYellow1 = this.add.container(this.shieldX, this.shieldY, [this.my.sprite.OvalYellow1])
        this.my.bowenemyYellow1.add([Bow1, YellowHand1]);

        this.bow1PathProgress = 0;

        // this.bowEnemies.add(this.my.bowenemyYellow1);

        this.timesBowHit1 = 0;
        this.justBowHit1 = false;


        //Bow Enemy 2
        let Bow2 = this.add.sprite(+15,+10, "Bow").setOrigin(.1,.5);
        let YellowHand2 = this.add.sprite(+15,+10, "YellowHand").setOrigin(.1,.5);
        this.my.sprite.Bow2 = Bow2;
        this.my.sprite.YellowHand2 = YellowHand2;
 
        this.my.sprite.OvalYellow2 = this.add.sprite(0, 0, "OvalYellow");
        my.bowenemyYellow2 = this.add.container(this.shieldX, this.shieldY, [this.my.sprite.OvalYellow2])
        this.my.bowenemyYellow2.add([Bow2, YellowHand2]);

        this.bow2PathProgress = 0;

        // this.bowEnemies.add(this.my.bowenemyYellow2);

        this.timesBowHit2 = 0;
        this.justBowHit2 = false;


        //Bow Enemy 3
        let Bow3 = this.add.sprite(+15,+10, "Bow").setOrigin(.1,.5);
        let YellowHand3 = this.add.sprite(+15,+10, "YellowHand").setOrigin(.1,.5);
        this.my.sprite.Bow3 = Bow3;
        this.my.sprite.YellowHand3 = YellowHand3;
 
        this.my.sprite.OvalYellow3 = this.add.sprite(0, 0, "OvalYellow");
        my.bowenemyYellow3 = this.add.container(this.shieldX, this.shieldY, [this.my.sprite.OvalYellow3])
        this.my.bowenemyYellow3.add([Bow3, YellowHand3]);

        this.bow3PathProgress = .5;

        // this.bowEnemies.add(this.my.bowenemyYellow2);

        this.timesBowHit3 = 0;
        this.justBowHit3 = false;
    }
```

After:
```javascript
class Enemy {
    constructor(scene, x, y, pathProgress = 0) {
        this.scene = scene;
        this.pathProgress = pathProgress;
        this.timesHit = 0;
        this.justHit = false;
        this.container = scene.add.container(x, y, [scene.add.sprite(0, 0, this.bodyKey)]);
        this.addParts();                 // subclass hook
    }
    addParts() {}
    destroy() {
        this.container.destroy();
    }
}


class ShieldEnemy extends Enemy {
    get bodyKey() { return "shieldEnemyRed"; }
    addParts() {
        const s = this.scene;
        this.helmet = s.add.sprite(0, -25, "Helmet");
        this.shield = s.add.sprite(15, 10, "Shield").setScale(0.5);
        this.container.add([this.helmet, this.shield]);
    }
}


class BowEnemy extends Enemy {
    get bodyKey() { return "OvalYellow"; }
    addParts() {
        const s = this.scene;
        this.bow = s.add.sprite(15, 10, "Bow").setOrigin(0.1, 0.5);
        this.hand = s.add.sprite(15, 10, "YellowHand").setOrigin(0.1, 0.5);
        this.container.add([this.bow, this.hand]);
    }
}


// ---------- Wave data ----------
// Each entry: [EnemyClass, count, spawn-point key, path offsets for each enemy]
const WAVES = [
    [ // wave 1
        { type: ShieldEnemy, spawn: "enemy", offsets: [0, 0] },
        { type: BowEnemy,    spawn: "shield", offsets: [0, 0] },
    ],
    [ // wave 2
        { type: ShieldEnemy, spawn: "enemy", offsets: [0, 0, 0.5] },
        { type: BowEnemy,    spawn: "shield", offsets: [0, 0, 0.5] },
    ],
];


// ---------- Scene methods ----------
clearEnemies() {
    (this.enemies ?? []).forEach(e => e.destroy());
    this.enemies = [];
}


startWave(index) {
    this.clearEnemies();
    const spawnPoints = {
        enemy:  { x: this.enemyX,  y: this.enemyY },
        shield: { x: this.shieldX, y: this.shieldY },  // original bow enemies spawned here
    };


    for (const group of WAVES[index]) {
        const { x, y } = spawnPoints[group.spawn];
        for (const offset of group.offsets) {
            this.enemies.push(new group.type(this, x, y, offset));
        }
    }
    this.enemiesRemaining = this.enemies.length;
}
```
### This JavaScript code block is used for loops to create floating text, when it could be using a map function instead. 
 ```    JAVASCRIPT 
 for (let i = 1; i <= 7; i++) {
        this[`ball${i}`] = this.add.follower(line1, -200, game.config.height-(game.config.height/1.75), 'rocket');
        this[`ball${i}`].startFollow({
          delay: (i - 1) * delayIncrement,
          duration: 800,
          yoyo: true,
          ease: 'Sine.easeInOut',
          repeat: -1,
        });
      }
      for (let i = 7; i <= 12; i++){
        this[`ball${i}`] = this.add.follower(line1, -200, game.config.height-(game.config.height/2), 'rocket');
        this[`ball${i}`].startFollow({
          delay: (i - 7) * delayIncrement,
          duration: 800,
          yoyo: true,
          ease: 'Sine.easeInOut',
          repeat: -1,
        });
      }
      for (let i = 13; i <= 40; i++){
        this[`ball${i}`] = this.add.follower(line1, -200, game.config.height-(game.config.height/6), 'rocket');
        this[`ball${i}`].startFollow({
          delay: (i - 13) * delayIncrement,
          duration: 800,
          yoyo: true,
          ease: 'Sine.easeInOut',
          repeat: -1,
        });
      } 
 ``` 
## Refactor for JS
``` JAVASCRIPT
const transformedText = this[`ball${i}`].map(this[`ball${i}`] => this.add.follower(line1, -200, game.config.height-(game.config.height/6), 'rocket');)
return transformedText;
 ``` 
### This Python code block is using a for loop to find prime numbers, when it could be using a filter function instead.
 ``` PYTHON
if inputn > 1:
   for i in range(2,inputn):
       if (inputn % i) == 0:
           break
   else:
       print(inputn,"is a prime number.")
       
else:
   print(inputn,"is not a prime number.")
 ```
## Refactor for Python
``` PYTHON
primeList = list(filter(lambda n : isprime(n), numberList)
 ``` 
