#include <stdio.h>
#include <stdlib.h>  

int main() {
    int decimal;

    printf("-----------------------------------------------------------------------------------------------\n");
    printf("THIS IS A CONVERER WHICH CONVERTS DECIMAL NUMBER TO BINARY,OCTAL AND HEXADECIMAL\n");
    printf("-----------------------------------------------------------------------------------------------\n");
    do {
        printf("Enter A Non-Negative Integer: ");
        scanf("%d", &decimal);

        if (decimal < 0)
            printf("Enter a posivite integer\n");
    } while (decimal < 0);

    // ---------- DECIMAL TO BINARY ----------
    char *binary = NULL;
    int num = decimal;
    int binLength = 0;

    do {
        binary = realloc(binary, binLength + 2); 
        binary[binLength++] = (num % 2) ? '1' : '0';
        num /= 2;
    } while (num != 0);

    binary[binLength] = '\0';

    for (int i = 0; i < binLength / 2; i++) {
        char temp = binary[i];
        binary[i] = binary[binLength - i - 1];
        binary[binLength - i - 1] = temp;
    }

    // ---------- DECIMAL TO OCTAL ----------
    char *octal = NULL;
    num = decimal;
    int octLength = 0;

    do {
        octal = realloc(octal, octLength + 2);
        octal[octLength++] = (num % 8) + '0';
        num /= 8;
    } while (num != 0);

    octal[octLength] = '\0';

    for (int i = 0; i < octLength / 2; i++) {
        char temp = octal[i];
        octal[i] = octal[octLength - i - 1];
        octal[octLength - i - 1] = temp;
    }

    // ---------- DECIMAL TO HEXADECIMAL ----------
    char *hex = NULL;
    char hexChars[] = "0123456789ABCDEF";
    num = decimal;
    int hexLength = 0;

    do {
        hex = realloc(hex, hexLength + 2);
        hex[hexLength++] = hexChars[num % 16];
        num /= 16;
    } while (num != 0);

    hex[hexLength] = '\0';

    for (int i = 0; i < hexLength / 2; i++) {
        char temp = hex[i];
        hex[i] = hex[hexLength - i - 1];
        hex[hexLength - i - 1] = temp;
    }

    printf("\nNumber Conversions for %d:\n", decimal);
    printf("Binary      : %s\n", binary);
    printf("Octal       : %s\n", octal);
    printf("Hexadecimal : %s\n", hex);

    // Free allocated memory
    free(binary);
    free(octal);
    free(hex);

    return 0;
}
