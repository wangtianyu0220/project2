#include <iostream>
#include <map>
#include <vector>
#include <string>
#include<fstream>
#include <algorithm>
#include <stdlib.h> 

int main()
{
	std::ifstream input("common_passwords.txt");
	std::map<int, std::vector<std::string>> password_map;
	std::string password, password_give;
	std::vector<int> get_minidiff;
	std::vector<std::string> result;
	int len_of_password_give;
	std::cout << "Give me a password: ";
	std::cin >> password_give;
	std::cout << "You provided a password of " << password_give << std::endl;
	len_of_password_give = password_give.length();
	while (input >> password) {
		int diff = 0;
		int len_of_password = password.length();
		if (len_of_password < len_of_password_give) {
			for (int i = 0; i < len_of_password; i++) {
				if (password[i] != password_give[i]) {
					++diff;
				}
			}
			diff += len_of_password_give - len_of_password;
		}
		else {
			for (int i = 0; i < len_of_password_give; i++) {
				if (password[i] != password_give[i]) {
					++diff;
				}
			}
			diff += len_of_password - len_of_password_give;
		}
		password_map[diff].push_back(password);
		get_minidiff.push_back(diff);
	}
	std::sort(get_minidiff.begin(), get_minidiff.end());
	result = password_map[get_minidiff[0]];
	std::sort(result.begin(), result.end());
	std::cout << "The most similar passwords to " << password_give << " are:" << std::endl;
	for (auto x : result) {
		std::cout << x << ", ";
	}
	std::cout << std::endl;
	std::cout << "All of which are " << get_minidiff[0] << " character(s) different." << std::endl;
}
