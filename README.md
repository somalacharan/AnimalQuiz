#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <stdlib.h>

int check_guess(char guess[], const char *answer, int score) {
    int attempt = 0;
    int still_guessing = 1;

    
    char answer_lower[50];
    strncpy(answer_lower, answer, sizeof(answer_lower) - 1);
    answer_lower[sizeof(answer_lower) - 1] = '\0'; 
    for (int i = 0; answer_lower[i]; i++) {
        answer_lower[i] = tolower(answer_lower[i]);
    }

    while (still_guessing && attempt < 3) {
        for (int i = 0; guess[i]; i++) {
            guess[i] = tolower(guess[i]);
        }

        if (strcmp(guess, answer_lower) == 0) {
            printf("Correct answer!\n");
            score += 1;
            still_guessing = 0;
        } else {
            if (attempt < 2) {
                printf("Sorry, incorrect answer. Try again: ");
                fgets(guess, 50, stdin);  
        
                guess[strcspn(guess, "\n")] = '\0';
            }
            attempt += 1;
        }
    }

    if (attempt == 3) {
        printf("The correct answer is: %s\n", answer);
    }

    return score;
}

int main() {
    int score = 0;
    char guess1[50], guess2[50], guess3[50], guess4[50];

    printf("Welcome to the Animal Quiz!\n");

    
    printf("Which bear lives at the North pole: ");
    fgets(guess1, 50, stdin);  
    guess1[strcspn(guess1, "\n")] = '\0'; 
    score = check_guess(guess1, "polar bear", score);


    printf("Which is the largest animal: ");
    fgets(guess2, 50, stdin);  
    guess2[strcspn(guess2, "\n")] = '\0';  
    score = check_guess(guess2, "blue whale", score);

    
    printf("Which is the fastest land animal: ");
    fgets(guess3, 50, stdin);  
    guess3[strcspn(guess3, "\n")] = '\0';  
    score = check_guess(guess3, "cheetah", score);

    
    printf("Which animal is known for its trunk: ");
    fgets(guess4, 50, stdin);  
    guess4[strcspn(guess4, "\n")] = '\0';  
    score = check_guess(guess4, "elephant", score);

    
    printf("Your final score is: %d/4\n", score);

    return 0;
}
