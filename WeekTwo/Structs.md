# Introduction to Structures ( Structs )

Structures (also called structs) are a way to group several related variables into one place. 
Each variable in the structure is known as a member of the structure.

Unlike an array, a structure can contain different data types (int, string, bool, etc.)

[w3schools](https://www.w3schools.com/cpp/cpp_structs.asp)

## Creating a Structure
In order to create a structure, we need to use the `struct` keyword and assign the member variables inside that code block.

__Example__
```cpp
struct PlayerCharacter
{
    int charisma;
    int strength;
    int dexterity;
    string name;
};
```
In the above example, we declare the structure with the `struct` keyword, followed by the tag ( label / type ) `PlayerCharacter` with four _member variables_ of `int charisma`, `int strength`, `int dexterity` and `string name`.

Additionally, the member variables within our `PlayerCharacter` structure could be a structure type aswell. For example:

```cpp
struct Weapon
{
    string name;
    int strength;
    double value;
}

struct PlayerCharacter
{
  // ... everything else
  Weapon playerWeapon;
}
```

When defining a structure, it is generally placed outside of any function definition. This makes the structure type you've created available to all code following its definition.

## Using our Structure
Now that we have our structure called `PlayerCharacter` we can assign that as a type to variables.

__Example__
```cpp
PlayerCharacter gandalfTheGrey, frodoBaggins;
```
This would create two variables called `gandalfTheGrey` and `frodoBaggins` that are of the type `PlayerCharacter`. We can then assign values to those member variables we created earlier.
```cpp
gandalfTheGrey.name = "Gandalf The Grey";
frodoBaggins.name = "Frodo Baggins";
cout << gandalfTheGrey.name << endl
        << frodoBaggins.name << endl;
```
Output
```
Gandalf The Grey
Frodo Baggins
```


*Important note*

By creating this `PlayerCharacter` `struct`, these two variables are distinct from one another. This means that updating or changing one will not effect other variables with the same `struct`.

# Using Structures in Functions

## Structures as Arguments
Just like the primitive data types we have used before such as `int`, `bool`, and `float`, you can use your structure-typed variables as arguments in function calls. These arguements can either be passed-by-value or passed-by-reference the same way as if you were to pass in a reference to an `int`.

__Example__
```cpp
struct Car 
{
    string make, model;
    double mpg, mileage;
    int year;
}

void getCarMilage(Car& car)
{
     cout << car.mileage;
}

int main()
{
  Car nissanUltima;
  nissanUltima.year = 2005;
  nissanUltima.make = "Nissan";
  nissanUltima.model = "Ultima";
  nissanUltima.mileage = 180000;
  nissanUltima.mpg = 35;

  getCarMileage(nissanUltima);

  return 0;
}
```
__Output__
```
35
```

## Structures as Return Types
In addition to being used to type arguments passed into functions, structures allow you to type your function returns.

```cpp
Car createNewCar(string make, string model, int year, double mpg, double mileage)
{
  Car newCar;
  newCar.make = make;
  newCar.model = model;
  newCar.year = year;
  newCar.mpg = mpg;
  newCar.mileage = mileage;
  return newCar; 
};
```

The above function takes in five arguements, which are all going to be assigned to the member variables of the new Car instance `newCar`. Once the values are assigned, the function returns the new object.

```cpp
Car jacksCar;
jacksCar = createNewCar("Voltswagon", "Bus", 1960, 5, 209000);
cout << "Jack drives a "
        << jacksCar.make 
        << " " 
        << jacksCar.model
        << endl;
```
__Output__
```
Jack drives a Voltswagon Bus
```

# Array of Structures

```cpp
struct StarfleetOfficer
{
    string name;
    string rank;
}

StarfleetOfficer captain;
StarfleetOfficer numberOne;
StarfleetOfficer scienceOfficer;

captain.name = "Jean Luc Picard";
captain.rank = "Captain";
numberOne.name = "William T. Riker";
numberOne.rank = "Commander";
scienceOfficer.name = "Beverly Crusher";
scienceOfficer.rank = "Dr.";

StarfleetOfficer[3] bridgeCrew = { captain, numberOne, scienceOfficer };

cout << "Aboard the Starship Enterprise there is:" << endl;

for(int crewMember = 0; crewMember < 3; ++crewMember)
{
    cout << bridgeCrew[crewMember].rank << " "
            << bridgeCrew[crewMember].name << endl;
}

```

__Output__
```
Aboard the Starship Enterprise there is:
Captain Jean Luc Picard
Commander William T. Riker
Dr. Beverly Crusher
```

This can also be written as a _hierarchical_ structure to increase readability.

```cpp
struct StarfleetOfficer
{
  // ...
};

struct StarfleetShip
{
    string name;
    string callsign;
    StarfleetOfficer crew[3];
};

StarfleetShip starshipEnterprise;
starshipEnterprise.name = "Enterprise";
starshipEnterprise.callsign = "NCC1701D";
starshipEnterprise.crew = { captain, numberOne, scienceOfficer };

cout << "Aboard the Starship " << starshipEnterprise.name  << " there is:" << endl;

for(int crewMember = 0; crewMember < 3; ++crewMember)
{
    cout << starshipEnterprise.crew[crewMember].rank << " "
            << starshipEnterprise.crew[crewMember].name << endl;
}

```

__Output__
```
Aboard the Starship Enterprise there is:
Captain Jean Luc Picard
Commander William T. Riker
Dr. Beverly Crusher
```