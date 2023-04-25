# Review for the First Midterm
## Files
In order to access files, you need to use the `<fstream>` library which
contains the `ifstream` and `ofstream` member functions.

`ifstream` - This reads the data from a file.

Example:
```cpp
#include <iostream>
#include <ifstream>
#include <string>

int main()
{
    // Creating an object
    ifstream input_file;
    // Opening our userInfo.csv file
    // ex: John,Smith
    input_file.open("userInfo.csv");
    // Declaring variables to hold the data read from the file
    string first_name, last_name;
    // Reading in our data with the >> operator.
    input_file >> first_name >> second_name;
    // Now first_name = John last_name = Smith
    cout << first_name << " " << last_name << endl;
    // Close our file after getting the data we need.
    input_file.close();
    return 0;
}

```

`ofstream` - This writes data to a file.

Example:
```cpp
#include <iostream>
#include <ifstream>
#include <string>

int main()
{
    // Creating an object
    ofstream output_file;
    // This will either open a file with this name, but if it
    // doesn't exist, it will create this file.
    output_file.open("userInfo.csv");
    // Declaring variables to hold the data we will write to the file
    string first_name, last_name;
    // Asking user for info
    cout << "What is your first name?" << endl;
    cin >> first_name;
    cout << "What is your last name?" << endl;
    cin >> last_name;
    // Writing out our data with the << operator.
    output_file >> first_name >> second_name;
    // Close our file after writing our data.
    output_file.close();
    return 0;
}
```

### Checking for failures
```cpp
// ---- other code
    // Check that the input file was read successfully
    if(in_stream.fail())
    {
        // Display error message
        cout << "Input file has failed to open.\n";
        // End the program
        exit(1);
    }
    // Check that the output file was read successfully
    if(out_stream.fail())
    {
        // Display error message
        cout << "Output file has failed to open.\n";
        // End the program
        exit(1);
    }
// ---
```

### Appending Data to a File

```cpp
// Appends data to the end of a file called data.txt
#include <fstream>
#include <iostream>

using namespace std;

int main()
{
    cout << "Opening data.txt to append data...";
    ofstream file_out;
    file_out.open("data.txt", ios::app);
    // ios::app puts your position at the end of the file every time the stream is flushed.
    // ios::ate puts your position to the end of the file it is opened.
                                         
    if(file_out.fail())
    {
        cout << "Failed to open input file.";
        exit(1);
    }
    file_out << "5 6 pick up sticks.\n"
             <<  "7 8 ain't C++ great!\n";
    file_out.close();
    cout << "Date appended to data.txt successfully.";
    
    return 0;
}
```

### Using User Input for File Names.
```cpp

#include <fstream>
#include <iostream>

using namespace std;

int main()
{
    char file_path_in[16], file_path_out[16];
    cout << "What file would you like to parse? (max 15 characters): ";
    cin >> file_path_in;
    
    cout << "What file would you like to save this data to? (max 15 characters): ";   
    cin >> file_path_out;
    
    ifstream in_stream;
    ofstream out_stream;
    in_stream.open(file_path_in);
    out_stream.open(file_path_out)
    
    if(in_stream.fail())
    {
        cout << "Failed to open " << file_path_in;
        exit(1);
    }
    if(out_stream.fail())
    {
        cout << "Failed to open " << file_path_out;
        exit(0);
    }
    int first_number, second_number, third_number;
    in_stream >> first_number >> second_number >> third_number;
    out_stream  << "The sum of the numbers in  "
                << file_path_in << ": "
                << first_number << ', ' 
                << second_number << ', ' 
                << "and " << third_number 
                << " is " << ( first_number + second_number + third_number ) 
                << "\n"
                << "Writing to " 
                << file_path_out
                << " was successful."
                << endl;
    in_stream.close();
    out_stream.close();
    cout << "Ending program...";
   
    return 0;
}
```

## Structs

Structures (also called structs) are a way to group several related variables into one place.
Each variable in the structure is known as a member of the structure.

Unlike an array, a structure can contain different data types (int, string, bool, etc.)

[w3schools](https://www.w3schools.com/cpp/cpp_structs.asp)

### Creating a Structure
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

### Using our Structure
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

### Using Structures in Functions

### Structures as Arguments
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

### Structures as Return Types
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

### Array of Structures

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