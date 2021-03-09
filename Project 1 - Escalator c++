/*

  File:         proj1.cpp
  Author:       Ara Carmel Quinones
  Date:         9/24/2020
  Section:      CMSC 202 Section 10
  Description:  Projet 1 - Escalators
  
  Develop the code to evaluate if a three-word list can be made from previous words when removing exactly one letter.

*/

#include <iostream>
#include <string>
#include <ctime>
#include <fstream>
#include <iomanip>
#include <cmath>

using namespace std;

const int sizeArray = 3;        //the maximum number of words in a file
const int maxFirst = 6;         //maximum length of the first word
const int maxSecond = 5;        //maximum length of the second word
const int maxThird = 4;         //maximum length of the third word
const int numAlphabet = 26;     //numbers of the alphabet
const int maxNoMatch = 2;       //the maximum number of word that has wrong frequencies
const int numChar = 80;         //numbers of characters that can be stored

// Name: loadFile
// PreCondition:  empty wordsArray to store words into, fileName is the file user wants to open
// PostCondition: return true if file is found and fills in wordsArray with words, and false if file does not exist
int loadFile(char wordsArray[][numChar], string fileName);

// Name: checkAnswer
// PreCondition:  wordsArray contains words to iterate through to count the letters, empty wordsLength to store length of words
// PostCondition: Returns true or false whether all the words meets length requirement
int checkAnswer(char wordsArray[][numChar], int wordsLength[]);

// Name: countLetters
// PreCondition:  wordsArray stores the list of words, frequency array will be used to store how many letters is in a word
// PostCondition: Returns true or false whether the list of words meets required frequency
int countLetters(char wordsArray[][numChar], int frequency[][numAlphabet]);

// Name: printWords
// PreCondition:  wordsArray stores the list of words, wordsLength is stores the length of each word in the list
// PostCondition: nothing is return, just a print function
void printWords(char wordsArray[][numChar], int wordLength[]);

// Name: clearList
// PreCondition:  wordsArray stores the list of words, frequency stores how many letters is in a word,
// wordsLength is an array that stores the length of each word in the list
// PostCondition:nothing is return, it resets all the Arrays to use for another round of the program
void clearList(char wordsArray[][numChar], int frequency[][numAlphabet], int wordLength[]);

int main() {
    string fileName;
    char wordsArray[sizeArray][numChar];
    int trueOrFalseLoadFile;
    int trueOrFalseCheckAnswer;
    int trueOrFalseCountLetters;
    int frequency[sizeArray][numAlphabet] = { { 0 } };
    int wordLength[] = {0,0,0};
    string yesOrNo;
    string smallYes = "y";
    string bigYes = "Y";
    string smallNo = "n";
    string bigNo = "N";

    cout << "Welcome to Escalators" << endl;
    //do while loop ends when user does not enter 'y' or 'Y'
    do {
        cout << "What is the file name of the list of words?" << endl;
        cin >> fileName;

        //loadFile function call: checks if file exist
        trueOrFalseLoadFile = loadFile(wordsArray, fileName);

        //check if file exist: returns 1 if file exist
        if (trueOrFalseLoadFile == 1) {

            //checkAnswer function call: checks if words meets length requirement
            trueOrFalseCheckAnswer = checkAnswer(wordsArray, wordLength);

            //if trueOrFalseCheckAnswer is 1,words are correct length
            if (trueOrFalseCheckAnswer == 1) {

                //checks if list of words meets frequency requirement
                trueOrFalseCountLetters = countLetters(wordsArray, frequency);

                //list is a valid escalator, calls printWord to print the words and length
                if (trueOrFalseCountLetters == 1) {
                    printWords(wordsArray, wordLength);
                    cout << "This list is valid!" << endl;
                }

                    //list is not valid escalator, does not meet frequency requirement, prints words and length
                else {
                    printWords(wordsArray, wordLength);
                    cout << "Words do not share appropriate letter frequency." << endl;
                    cout << "This list is not valid!" << endl;
                }
                //if trueOrFalseCheckAnswer is 0, words are not correct length
            }
            else {
                printWords(wordsArray, wordLength);
                cout << "Words are not correct length." << endl;
                cout << "This list is not valid!" << endl;
            }
            //returns 0 if file does not exist
        }
        else {
            cout << "No file found." << endl;
        }
        cout << "Check another list? (y/n)" << endl;
        cin >> yesOrNo;

        //calls the function to clear the arrays
        clearList(wordsArray, frequency, wordLength);

        //if user enter 'y' or 'Y', the loop restarts again
    } while ((yesOrNo == smallYes) || (yesOrNo == bigYes));
    cout << "Thank you for using Escalators!" << endl;

    return 0;

}

//Load File – Populates a list of words by reading in a file.
//Validates that a file was found and opened
int loadFile(char wordsArray[][numChar], string fileName) {
    ifstream inputStream;

    inputStream.open(fileName);
    //if a file exist and it's open, store its content to wordsArray
    if (inputStream.is_open()) {

        inputStream >> wordsArray[0];
        inputStream >> wordsArray[1];
        inputStream >> wordsArray[2];

        inputStream.close();
        //return 1 if file exist
        return 1;

        //return 0 if file does not exists
    }
    else {
        return 0;
    }
}

//Should print the words from the list
void printWords(char wordsArray[][numChar], int wordLength[]) {

    //iterates through the wordsArray to print the words in it
    for (int i = 0; i < sizeArray; i++) {
        cout << i + 1 << "." << wordsArray[i] << "(" << wordLength[i] << " letters)" << endl;
    }
}

//Clears the array between runs
void clearList(char wordsArray[][numChar], int frequency[][numAlphabet], int wordLength[]) {
    int maxLength = maxFirst;

    //clears the wordsArray by storing null character in it
    for (int i = 0; i < sizeArray; i++) {
        for (int j = 0; j < maxLength; j++) {
            wordsArray[i][j] = '\0';
            --maxLength;
        }
    }
    //clears the frequency array by storing 0 in all the elements
    for (int i = 0; i < sizeArray; i++) {
        for (int j = 0; j < numAlphabet; j++) {
	  frequency[i][j] = {{0}};
        }
    }
    //clears the wordsLength by storing null character in it
    for (int i = 0; i < sizeArray; i++)
        wordLength[i] = '\0';
}


//Iterates through each word and calls countLetters
//count how many letters in a word
int checkAnswer(char wordsArray[][numChar], int wordLength[]) {
    int countFirst = 0;
    int countSecond = 0;
    int countThird = 0;
    int count = 0;
    int allWordsMeetsMax = 3;


    //finds the length of the first word
    for (countFirst; wordsArray[0][countFirst] != '\0'; countFirst++) {
    }

    //finds the length of the second word
    for (countSecond; wordsArray[1][countSecond] != '\0'; countSecond++) {
    }

    //finds the length of the third word
    for (countThird; wordsArray[2][countThird] != '\0'; countThird++) {
    }

    //checks if each words meets required length
    if (countFirst == maxFirst) {
        count++;
    }
    if (countSecond == maxSecond) {
        count++;
    }
    if (countThird == maxThird) {
        count++;
    }

    // stores each length into array
    wordLength[0] = countFirst;
    wordLength[1] = countSecond;
    wordLength[2] = countThird;

    //check if words meets length requirement
    if (count == allWordsMeetsMax)
        return 1;

    //return false(0) if words doesn't meet length requirement
    else
        return 0;
}
//Counts how many of each letter exist in each word
int countLetters(char wordsArray[][numChar], int frequency[][numAlphabet]) {
    int noMatchCounter = 0;
    char alphabet[] = "abcdefghijklmnopqrstuvwxyz";

    //finds how many letters is in a word
    for (int i = 0; i < sizeArray; i++) {
        for (int j = 0; j < numAlphabet; j++) {
            //check if a letter is in the word I am looking at
            if (wordsArray[i][i] == alphabet[j]) {
                //increment by 1 if letter exist
                frequency[i][j]++;
            }
        }
    }
    
    //looks if there's 1 or 2 letters that does not match, this indicates if the list is valid or not
    //check if letters exist in the other word
    for (int i = 0; i < sizeArray - 1; i++) {
      for (int j = 0; j < numAlphabet; j++) {
	if (frequency[i + 1][j] != frequency[i][j])
	  //if there's a letter that does not match, increment by 1
	  noMatchCounter++;
      }
    }

    //is there are 2 existing mismatch letters between the words, the list meets frequency requirement
    if (noMatchCounter == maxNoMatch) {
        return 1;
    }
        //if no 2 letters are mismatch, the list does not meet frequency requirement
    else {
        return 0;
    }
}
