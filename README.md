# Sifreleme-ve-Sifre-Cozme-Programi

// Kullanıcı tarafından girilen bir mesajı şifreleyen ya da şifresini çözen C programı.

#include<stdio.h>

void menu();
void encrypt_open_msg();
void decrypt_secret_msg();
int find_size_of_line(char line[]);
void reverse_line(char line[], int line_lenght);
 
int main()
{
    menu();
}

void menu()
{
    int choice;
    do{
        printf("1. Encrypt\n2. Decrypt\n0. Exit\nChoice: ");
        scanf("%d", &choice);
        switch(choice){
            case 1:
                encrypt_open_msg();
                break;
            case 2:
                decrypt_secret_msg();
                break;
            case 0:
                break;
            default:
                menu();
                break;
        }
    printf("\n________________________\n\n");
    }while(choice != 0);
}

void encrypt_open_msg()
{   
    int key, a, i;
    char line[1024];
    char *status;
    FILE *inp, *outp;
    inp = fopen("open_msg.txt", "r");
    outp = fopen("secret_msg.txt", "w");
    do{
        printf("Key value between 0-26: ");
        scanf("%d", &key);
    }while(key < 0 || key > 26);
    for(status = fgets(line, 1024, inp); status != 0; status = fgets(line, 1024, inp)){
        for(i = 0; line[i] != '\0'; i++);
        for(i=(i-1); i >= 0; i--){
            a = (line[i]-key);
            if(a < 'a')
                a = (a + 26);
            if(a > 'z')
                a = (a-26);
            if(line[i] != ' ' && line[i] != '.' && line[i] != '\n' && a != '"'){
                printf("%c", a);
                fprintf(outp, "%c", a);
            }
            if(line[i] == ' '){
                printf("_");
                fprintf(outp, "_");
            }
            if(line[i] == '.'){
                printf("*");
                fprintf(outp, "*");
            }
        }
        fprintf(outp, "\n");
        printf("\n");
    }
    fclose(inp);
    fclose(outp);
}

void decrypt_secret_msg()
{
    int key, a, i;
    char line[1024];
    char *status;
    FILE *inp, *outp;
    inp = fopen("secret_msg.txt", "r");
    outp = fopen("open_msg.txt", "w");
    do{
        printf("Key value between 0-26: ");
        scanf("%d", &key);
    }while(key < 0 || key > 26);
    for(status = fgets(line, 1024, inp); status != 0; status = fgets(line, 1024, inp)){
        for(i = 0; line[i] != '\0'; i++);
        for(i=(i-1); i >= 0; i--){
            a = (line[i]+key);
            if(a < 'a')
                a = (a + 26);
            if(a > 'z')
                a = (a - 26);
            if(line[i] >= 'a' || line[i] >='z'){
                printf("%c", a);
                fprintf(outp, "%c", a);
            }
            if(line[i] == '_'){
                printf(" ");
                fprintf(outp, " ");
            }
            if(line[i] == '*'){
                printf(".");
                fprintf(outp, ".");
            }
        }
        printf("\n");
        fprintf(outp, "\n");
    }
    fclose(inp);
    fclose(outp);
}

int find_size_of_line(char line[])
{
    int i;
    for(i = 0; line[i] != '\0'; i++);
    return i;
}

void reverse_line(char line[], int line_lenght)
{
    for(line_lenght-=1; line_lenght >= 0; line_lenght--){
        printf("%c", line[line_lenght]);
    }
}
