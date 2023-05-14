# c_project
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_TRANSLATIONS 100
// Structure to store translation pair
typedef struct {
char source[100];
char target[100];
} Translation;
// Global array to store translations
Translation translations[MAX_TRANSLATIONS];
int num_translations = 0;
// Function Prototypes
void addTranslation();
char* translateText(const char* text);
int main() {
int choice;
char text[100];
do {
printf("\nLanguage Translator\n");
printf("1. Add Translation\n");
printf("2. Translate Text\n");
printf("0. Exit\n");
printf("Enter your choice: ");
scanf("%d", &choice);
switch (choice) {
case 1:
addTranslation();
break;
case 2:
printf("Enter text to translate: ");
scanf(" %[^\n]s", text);
printf("Translated Text: %s\n", translateText(text));
break;
case 0:
printf("Exiting program. Goodbye!\n");
break;
default:
printf("Invalid choice. Please try again.\n");
break;
}
} while (choice != 0);
return 0;
}
// Function to add a translation pair to the translator
void addTranslation() {
if (num_translations == MAX_TRANSLATIONS) {
printf("Cannot add more translations. Limit reached.\n");
return;
}
printf("Enter source language: ");
scanf(" %[^\n]s", translations[num_translations].source);
printf("Enter target language: ");
scanf(" %[^\n]s", translations[num_translations].target);
printf("Translation added successfully.\n");
num_translations++;
}
// Function to translate text based on available translations
char* translateText(const char* text) {
char* translated_text = (char*)malloc(1000 * sizeof(char));
translated_text[0] = '\0';
for (int i = 0; i < num_translations; i++) {
if (strcmp(translations[i].source, text) == 0) {
strcpy(translated_text, translations[i].target);
break;
}
}
if (translated_text[0] == '\0') {
strcpy(translated_text, "Translation not found.");
}
return translated_text;
}
