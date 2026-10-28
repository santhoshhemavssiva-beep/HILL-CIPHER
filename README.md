NAME:SANTHOSH SIVAKUMAR

REG NO:212225040382

# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = {{1,2,1},{2,3,2},{2,2,1}};
int invkeymat[3][3] = {{-1,0,1},{2,-1,0},{-2,2,-1}};
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

void encode(char a, char b, char c, char ret[]) {
    int p[3] = {a-'A', b-'A', c-'A'}, i, j, x;
    for (i = 0; i < 3; i++) {
        x = 0;
        for (j = 0; j < 3; j++)
            x += p[j] * keymat[j][i];
        ret[i] = key[x % 26];
    }
    ret[3] = '\0';
}

void decode(char a, char b, char c, char ret[]) {
    int p[3] = {a-'A', b-'A', c-'A'}, i, j, x;
    for (i = 0; i < 3; i++) {
        x = 0;
        for (j = 0; j < 3; j++)
            x += p[j] * invkeymat[j][i];
        ret[i] = key[(x % 26 + 26) % 26];
    }
    ret[3] = '\0';
}

int main() {
    char msg[1000], enc[1000] = "", dec[1000] = "", temp[4];
    int i, j, n;

    printf("Enter plaintext: ");
    fgets(msg, sizeof(msg), stdin);
    msg[strcspn(msg, "\n")] = '\0';

    for (i = 0, j = 0; msg[i]; i++)
        if (isalpha((unsigned char)msg[i]))
            msg[j++] = toupper((unsigned char)msg[i]);
    msg[j] = '\0';

    printf("Input message : %s\n", msg);

    n = strlen(msg) % 3;
    for (i = 0; i < (n ? 3 - n : 0); i++)
        strcat(msg, "X");

    printf("Padded message : %s\n", msg);

    for (i = 0; i < strlen(msg); i += 3) {
        encode(msg[i], msg[i+1], msg[i+2], temp);
        strcat(enc, temp);
    }
    printf("Encoded message : %s\n", enc);

    for (i = 0; i < strlen(enc); i += 3) {
        decode(enc[i], enc[i+1], enc[i+2], temp);
        strcat(dec, temp);
    }
    printf("Decoded message : %s\n", dec);

    return 0;
}
```

## OUTPUT

<img width="1670" height="797" alt="image" src="https://github.com/user-attachments/assets/5b07ae47-d46e-4472-8b3a-08be61656e55" />


## RESULT

Succesfully implemented the HILL CIPHER


