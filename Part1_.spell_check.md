#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

int main()
{
    // Open dictionary file ifstream: inputs the files to be read, dict_file is myvariable to store the dictionary file
    ifstream dict_file("C:/Users/alexc/OneDrive/Documents/National University/Intro to programming/Group_4_Final_Project/words");             //pulls dictionary from saved dictionary file may need to be updated for individual file locations
                                                                                                                                               // often programs pull info from C drive and windows x86 in order to be consistant amongst different users. 
    if (!dict_file)                                                      //checks if the file fails to open
    {
        cout << "Error: Could not open dictionary file." << endl;
        return 1;
    }

    // Vector to store all dictionary words 
    vector<string> words;                                               // creates vector to hold words from dictionary

    // Read every word in the dictionary
    string w;                                                           //declares new stirng varibale where words will be stored temporarily
    while (dict_file >> w)
    {
        words.push_back(w);                                             // reads wors from dict file and adds tothe end of the vector
    }                                                                   // loop repeats until all words are read

    dict_file.close();                                                  // closes the file since it is no longer neaded

    sort(words.begin(), words.end());                                   // sorts words vector in alphabetical order

    // Ask user for full path to the file we will spell check 
    cout << "Enter FULL path of the file to spell check:" << endl;
    cout << "(Example: C:/Users/Name/Documents/test.txt)" << endl;
    cout << "Ensure backslashs are correct / = is correct. " << endl;
    cout << ".docx or any word documents do not work. Convert to txt file before inputing" << endl;

    string filename;                                                    // declares new string for new txt file
    getline(cin >> ws, filename);                                       // reads full line (ws)including spaces

    //  Check file can be opened from user input 
    ifstream check_file(filename);

    if (!check_file)
    {
        cout << "Error: Could not open input file at:" << endl;
        cout << "  " << filename << endl;
        return 1;
    }

    // Read each word from the input file and check dictionary  
    string test_word;                                                   // temp variable to store each word from users file
    while (check_file >> test_word)                                     // reads words one at a time
    {
        if (!binary_search(words.begin(), words.end(), test_word))      //checks if the word is not found in dictionary
        {
            cout << "Not found: " << test_word << endl;                 // prints word. possible spelling error
        }
    }

    check_file.close();

    cout << "\nSpell checking completed." << endl;

    return 0;
}
