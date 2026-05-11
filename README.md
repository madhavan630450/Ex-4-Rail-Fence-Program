# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:
To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.

STEP-2: Arrange the plain text in row columnar matrix format.

STEP-3: Now read the keyword depending on the number of columns of the plain text.

STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.

STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM:
```
#include <stdio.h>
#include <string.h>

// Encryption
void encrypt(char text[], int key) {
    int len = strlen(text);
    char rail[key][len];

    // Fill matrix with '\n'
    for(int i = 0; i < key; i++)
        for(int j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;

    // Place characters in zig-zag
    for(int i = 0; i < len; i++) {
        rail[row][i] = text[i];

        if(row == 0)
            dir = 1;
        else if(row == key - 1)
            dir = -1;

        row += dir;
    }

    // Read row-wise
    int k = 0;
    for(int i = 0; i < key; i++) {
        for(int j = 0; j < len; j++) {
            if(rail[i][j] != '\n')
                text[k++] = rail[i][j];
        }
    }
    text[k] = '\0';
}

// Decryption
void decrypt(char text[], int key) {
    int len = strlen(text);
    char rail[key][len];

    // Fill with '\n'
    for(int i = 0; i < key; i++)
        for(int j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;

    // Mark zig-zag positions
    for(int i = 0; i < len; i++) {
        rail[row][i] = '*';

        if(row == 0)
            dir = 1;
        else if(row == key - 1)
            dir = -1;

        row += dir;
    }

    // Fill characters row-wise
    int k = 0;
    for(int i = 0; i < key; i++) {
        for(int j = 0; j < len; j++) {
            if(rail[i][j] == '*' && k < len)
                rail[i][j] = text[k++];
        }
    }

    // Read zig-zag to reconstruct
    row = 0; dir = 1;
    k = 0;

    for(int i = 0; i < len; i++) {
        text[k++] = rail[row][i];

        if(row == 0)
            dir = 1;
        else if(row == key - 1)
            dir = -1;

        row += dir;
    }
    text[k] = '\0';
}

int main() {
    char text[100];
    int key;

    // Input
    printf("Enter plaintext: ");
    fgets(text, sizeof(text), stdin);

    printf("Enter key (number of rails): ");
    scanf("%d", &key);

    // Remove newline from fgets
    text[strcspn(text, "\n")] = '\0';

    // Encrypt
    encrypt(text, key);
    printf("Encrypted text: %s\n", text);

    // Decrypt
    decrypt(text, key);
    printf("Decrypted text: %s\n", text);

    return 0;
}
```
# OUTPUT:
<img width="1707" height="931" alt="image" src="https://github.com/user-attachments/assets/b99ea4da-8242-4858-8acc-a61ce4ffcf05" />


# RESULT:
Thus, the C program for Rail Fence is executed successfully.
