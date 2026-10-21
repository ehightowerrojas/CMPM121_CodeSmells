# CMPM121 Code Smells

Duplicated Code: Seamus

Mysterious Name: Evan

A **Code Smell** is a surface indication that usually corresponds to coding malpractices and to the trained eye, can be detected instantly.

## Mysterious Name

One of the most important parts of coding clearly is coming up with good names that communicate what they do to us and others. As we code independently, it can be easy to come up with names for variables and functions that only make sense to us. Its important to think about others when you code, Fowler suggests that keeping code "mundane and clear" is vital to clearly communicating what your code does and how to use it properly.

Code Example (From Clicker D1 Project!):

Here, its not clear what button1 really does, changing it to "mainbutton" might be more clear to suggest its purpose of incrementing "counter" to users.

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

The **Mysterious Name** smell looks the same across all coding languages. Look for "let" or "const" in js/ts before variables to spot potential Mysterious Names. In C, look for data types being assigned to variables to spot this smell. Once you spot a Mysterious Name, change it to a mundane and clear name.

## Duplicated Code

### Introduction

Often times when coding you will find sections of code that resemble eachother or are identical. Fowler states that when you find such cases, your code will always be better if you can find a way to unify them. When unifying, you must find all examples of the repeated code and figure out any differences that might be between them in order to unify. Once done, your code could be much shorter and easier to read.

### Prevention and Refactoring

The simplest case of finding and fixing a duplicated code smell is if you have the same expression in two methods of the same class. In that case, one can use the Extract Function method that Fowler describes in chapter 6. However, if you have statements that are similar but not identical Fowler suggests using the Slide Statement method to rearrange the code into its identical sections and then extract those.

## Loops
* Loops are very commonly used because they are one of the first operations taught to programmers, but can be unclear in their function or purpose.
* Usage of loops can be replaced/replicated via pipeline functions like filters and maps, which more clearly display what the operation is doing and do what type of data.

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


