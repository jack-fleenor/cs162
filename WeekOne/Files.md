# Using Datafiles
## April 3rd, 2023

When it comes to handling data in files it is import to remember a few key details.
1. The name of the file you're attempting to access ( must be exact )
2. File Path 
3. File type
4. Delimiters such as space, tab, comma, or newline characters.

```cpp
// Example File Paths:
// Windows: C:\Users\Pam\Desktop\Program.cpp
// MacOs: TODO: // Add Example
```

## Reading and Writing a File
In order to open a file and read it's content, we need to include the header `<fstream>` library at the top of the
application. We'll be using the subsets `<ifstream>` ( reading the file ) and `<ofstream>` ( for writing to a file )
latΩer.

```cpp
#include <fstream>
int main(){
    return 0;
}
```

### Sample Algorithm - Finding a Value in a File
* Declare <ifstream> object.
* Open the data file to read using its path.
* Read the data into an array.
* Close the data file to prevent data-corruption or other bugs.
Go through the array, looking for a target value.
* * If found, process a successful execution.
* * If not found after the array is searched, process an unsuccessful execution.

We need to consider how many values we want to put in a line of text, and how we want to separate those values
by __tab__, __return__, __comma__, or __space__.
```csv
[//]: # Example of an CSV file, where values are *seperated* ( delimited ) by *commas*
1, 2, 3, 4, 5, 6, 7, 8, 9
```

![Screenshot 2023-04-03 at 22.20.29.png](assets%2FScreenshot%202023-04-03%20at%2022.20.29.png)

## Code Sample - Reading and Writing Files
```cpp
// This allows us to use the cout member function.
# include <iostream>
// This allows us to use the ifstream and ofstream member functions.
#include <fstream>
// This allows us to use the exit() member function.
#inlcude <cstdlib>
using namespace std;

int main()
{
    // create in_stream and out_stream to hold our data.
    ifstream in_stream;
    oofstream out_stream;
    
    // Opening a file called 'input_file.dat' and assigning the values to in_stream
    in_stream.open("input_file.dat");
    // Open an output file called 'output_file.dat' and assigning the values to out_stream
    out_stream.open("output_file.dat");
    // Declare our integers.
    int first_number,
        second_number,
        third_number;
    // Read the data from the file and assign the values to our integers.
    in_stream >> first_number >> second_number >> third_numebr;
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
    
    // Write to our output file.
    out_stream  << "The sum of the numbers in input_file.dat: " 
                << first_number << ', ' 
                << second_number << ', ' 
                << "and " << third_number 
                << " is " << ( first_number + second_number + third_number ) 
                << endl;
    // Close our files.
    in_stream.close();
    out_stream.close();
    return 0;
}
```

## Code Sample - Appending to a File
```cpp
// Appends data to the end of a file called data.txt
#include <fstream>
#inlcude <iostream>

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

## Code Sample - Getting File Names as Input
```cpp
#include <fstream>
#inlcude <iostream>

using namespace std;

int main()
{
    char file_path[16];
    cout << "What file would you like to parse? (max 15 characters): ";
    cin >> file_path;
    
    ifstream in_stream;
    in_stream.open(file_path, ios::app);
    
    if(in_stream.fail())
    {
        cout << "Failed to open " << file_path;
        exit(1);
    }
    
    // Do stuff .... //
    
    file_out.close();
    cout << "Date appended to data.txt successfully.";
    
    return 0;
}
```

## Code Sample - Getting File Names as Output
```cpp
#include <fstream>
#inlcude <iostream>

using namespace std;

int main()
{
    char file_path_in[16], file_path_out[16];
    cout << "What file would you like to parse? (max 15 characters): ";
    cin >> file_path_in;
    
    cout << "What file would you like to save this data to? (max 15 characters): ";   
    cin >> file_path_out;
    
    cout << "Computing the values from " << file_path_in 
         << " and writing the sum to " << file_path_out 
         << endl;
    
    ifstream in_stream;
    ofstream out_stream;
    in_stream.open(file_path, ios::app);
    out_stream.open()
    
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
    
    // Do stuff .... //
    
    file_out.close();
    cout << "Date appended to data.txt successfully.";
    
    return 0;
}
```