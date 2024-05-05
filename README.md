#include <iostream>
#include <fstream>
#include <vector>
#include <algorithm>

int main() {
    std::ifstream dictFile("/usr/share/dict/words");
    if (!dictFile) {
        std::cerr << "Error opening dictionary file." << std::endl;
        return 1;
    }

    std::vector<std::string> words;
    std::string word;
    while (dictFile >> word) {
        words.push_back(word);
    }
    dictFile.close();

    std::string filename;
    std::cout << "Enter the filename to check: ";
    std::cin >> filename;

    std::ifstream file(filename);
    if (!file) {
        std::cerr << "Error opening file." << std::endl;
        return 1;
    }

    std::cout << "Words not found in the dictionary:" << std::endl;
    while (file >> word) {
        if (std::find(words.begin(), words.end(), word) == words.end()) {
            std::cout << word << std::endl;
        }
    }

    file.close();
    return 0;
}
