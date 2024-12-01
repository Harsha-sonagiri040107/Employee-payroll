
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct employee {
    int id;
    char name[30];
    double salary;
    double ta, da, hra, gross, it, netsal;
};

int main() {
    struct employee emp[100];
    int i, j, keepcount;
    i = j = keepcount = 0;
    while (j != 4) {
        printf("1. Add employee information\n");
        printf("2. Display employee information\n");
        printf("3. Number of employees\n");
        printf("4. Exit\n");
        printf("Enter one of the above: ");
        scanf("%d", &j);
        switch (j) {
            case 1:
                printf("===========================\n");
                printf("Enter employee id: ");
                scanf("%d", &emp[i].id);
                printf("Enter employee name: ");
                scanf(" %[^\n]", emp[i].name);
                printf("Enter employee salary: ");
                scanf("%lf", &emp[i].salary);
                // Calculate allowances and deductions
                if (emp[i].salary < 10000) {
                    emp[i].ta = emp[i].salary * 0.05;
                    emp[i].da = emp[i].salary * 0.06;
                    emp[i].hra = emp[i].salary * 0.07;
                    emp[i].it = 0;
                } else if (emp[i].salary >= 10000 && emp[i].salary < 25000) {
                    emp[i].ta = emp[i].salary * 0.06;
                    emp[i].da = emp[i].salary * 0.07;
                    emp[i].hra = emp[i].salary * 0.08;
                    emp[i].it = emp[i].salary * 0.02;
                } else if (emp[i].salary >= 25000 && emp[i].salary < 50000) {
                    emp[i].ta = emp[i].salary * 0.07;
                    emp[i].da = emp[i].salary * 0.08;
                    emp[i].hra = emp[i].salary * 0.09;
                    emp[i].it = emp[i].salary * 0.03;
                } else {
                    emp[i].ta = emp[i].salary * 0.08;
                    emp[i].da = emp[i].salary * 0.09;
                    emp[i].hra = emp[i].salary * 0.10;
                    emp[i].it = emp[i].salary * 0.05;
                }
                emp[i].gross = emp[i].salary + emp[i].ta + emp[i].da + emp[i].hra;
                emp[i].netsal = emp[i].gross - emp[i].it;
                keepcount++;
                i++;
                printf("===========================\n");
                break;
            case 2:
                printf("You have entered the following employee information:\n");
                for (i = 0; i < keepcount; i++) {
                    printf("==========================\n");
                    printf("Employee id            : %d\n", emp[i].id);
                    printf("Employee name          : %s\n", emp[i].name);
                    printf("Employee salary        : %.2lf\n", emp[i].salary);
                    printf("Travelling allowance   : %.2lf\n", emp[i].ta);
                    printf("Draught allowance      : %.2lf\n", emp[i].da);
                    printf("House renting allowance: %.2lf\n", emp[i].hra);
                    printf("Gross salary           : %.2lf\n", emp[i].gross);
                    printf("Income tax             : %.2lf\n", emp[i].it);
                    printf("Net salary             : %.2lf\n", emp[i].netsal);
                    printf("==========================\n");
                }
                break;
            case 3:
                printf("===========================\n");
                printf("Number of employees: %d\n", keepcount);
                printf("===========================\n");
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }
    return 0;
}

