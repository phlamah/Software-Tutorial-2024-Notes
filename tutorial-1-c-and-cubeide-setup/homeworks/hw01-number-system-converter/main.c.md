#include <stdio.h>
#include <string.h>
#include <stdint.h>
#include <stdbool.h>

const char* const error_msg_decimal = "Error! That set of number is not a decimal number.\n";
const char* const error_msg_trinary = "Error! That set of number is not a trinary number.\n";
const char* const error_msg_duodecimal = "Error! That set of number is not a duodecimal number.\n";
const char* const error_msg_unsupported_system = "Error! The number system is not supported.\n";

const char* const msg_prompt_number = "Please enter a set of number:\n";
const char* const msg_prompt_current_number_system = "Please enter the current number system:\n";
const char* const msg_prompt_number_system_to_convert = "Please enter the number system you want the set of number be converted to:\n";
const char* const msg_output = "Output=";

unsigned long long int power(unsigned long long int x, int y){
    if (y == 0){
        return 1;
    }
    unsigned long long int tmp = x;
    for (int i = 0;i < y-1;i++){
        x *= tmp;
    }
    return x;
}
unsigned long long int string_to_interger(char *x){
    unsigned long long int sum = 0; int length = strlen(x);
    for (int i = 0;i < length ; i++) {
        sum = sum + power(10,length - i - 1) * (x[i] - '0');
    }
    return sum;
}
void decimal_to_duodecimal(unsigned long long int x){
    char tempoary[42] = ""; char t;
    int z = 0; int remainer; int length; unsigned long long int temp = x;
        while (temp > 0){
                remainer = temp % 12;
                 if (remainer == 10){
                    tempoary[z] = 'A';
                }
                else if (remainer == 11){
                    tempoary[z] = 'B';
                }
                else{
                    tempoary[z] = remainer + '0';
                }
                temp = temp / 12;
                z++;
            }
        
        length = z;
        printf("%s", msg_output);
        for (int i = 0;i < length;i++){
            printf("%c", tempoary[length-i-1]);

        }
}
void decimal_to_trinary(unsigned long long int x){
    char tempoary[42] = ""; char t;
    int z = 0; int remainer; int length; unsigned long long int temp = x;
        while (temp > 0){
                remainer = temp % 3;
                tempoary[z] = remainer + '0';
                temp = temp / 3;
                z++;
            }
        
        length = z;
        printf("%s",msg_output);
        for (int i = 0;i < length;i++){
            printf("%c", tempoary[length-i-1]);

        }
}


unsigned long long int duodecimal_to_decimal(char *x){
    int length = strlen(x);
    unsigned long long int value = 0; int z;
        for (int u = 0; u < length; u++){
            if (x[u] == 'A'){
                z = 10;                
            }
            else if (x[u] == 'B'){
                z = 11;
            }
            else{
                z = x[u] - '0';          
            }
            value += z * power(12,length - u -1);
        }
    return value;
    }

unsigned long long int trinary_to_decimal(char *x){
    int length = strlen(x);
    unsigned long long int value = 0; int z;
        for (int u = 0; u < length; u++){
                z = x[u] - '0'; 
                value += z * power(12,length - u -1);         
            }
            return value;
        }

    


bool is_trinary(char* x){
    for (int i = 0; i < strlen(x);i++){
        if (x[i] < '0'||x[i] > '2'){
            return false;
        }
    }
    return true;
}
bool is_decimal(char* x){
    int length = strlen(x);
    for (int i = 0; i < length;i++){
        if (x[i] < '0'||x[i] > '9'){
            return false;
        }
    }
    return true;
}
bool is_duodecimal(char* x){
    for (int i = 0; i < strlen(x);i++){
        if ((x[i] >= '0'&&x[i] <= '9')||x[i] == 'A'||x[i] == 'B'){
            continue;
        }
        else {
            return false;
        }
    }
    return true;
}

int main(){
    char input[42] = ""; int from; int to;
    printf("%s", msg_prompt_number);
    scanf("%s", input);
    int length = strlen(input);
    while (true){
        if (input[0] == '0'){
            for (int j = 0;j < length;j++){
                input[j] = input[j+1];
                }
        }
        else{
            break;
        }

    }
    printf("%s", input);
        
  
    /**
     * @brief 
     * Get user input for number to be convert
     */

    // TODO:
    

    printf("%s", msg_prompt_current_number_system);
    scanf("%d", &from);
    if (from != 3 && from != 10 && from != 12){
        printf("%s", error_msg_unsupported_system);
        return 0;
    }
    if (from == 3){
        if (!is_trinary(input)){
            printf("%s", error_msg_trinary);
            return 0;
        }
    }
    if (from == 10){
        if (!is_decimal(input)){
            printf("%s", error_msg_decimal);
            return 0;
        }
    }
    if (from == 12){
        if (!is_duodecimal(input)){
            printf("%s", error_msg_duodecimal);
            return 0;
        }
    }

    /**
     * @brief 
     * Get user input for current number system
     */

    // TODO:
    printf("%s", msg_prompt_number_system_to_convert);
    scanf("%d", &to);
    if (to != 3 && to != 10 && to != 12){
        printf("%s", error_msg_unsupported_system);
        return 0;
    }
    if (from == 12 && to == 10){
        printf("%s%d", msg_output, duodecimal_to_decimal(input));
    }
    if (from == 3 && to == 10){
        printf("%s%d", msg_output, trinary_to_decimal(input));
    }
    if (from == 3 && to == 12){
        decimal_to_duodecimal(trinary_to_decimal(input));
    }
    if (from == 12 && to == 3){
        decimal_to_trinary(duodecimal_to_decimal(input));
    }
    if (from == 10 && to == 3){
        decimal_to_trinary(string_to_interger(input));
    }
    if (from == 10 && to == 12){
        decimal_to_duodecimal(string_to_interger(input));
    }
 

    /**
     * @brief 
     * Get user input for the number system for conversion.
     * Print converted number in format of "Output=12", e.g Output=ABCDEF
     * No space should be inserted in the asnwer "Output=XXX".
     * In case of wrong number system for conversion, please use the above error msgs.
     */

    // TODO:


    return 0;
}
// C programmers never die. They are just cast into void.
