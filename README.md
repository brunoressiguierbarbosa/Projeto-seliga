#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CLIENTES 100

typedef struct {
    char nome[50];
    int numeroConta;
    float saldo;
} Conta;

Conta clientes[MAX_CLIENTES];
int totalClientes = 0;

void criarConta() {
    if (totalClientes >= MAX_CLIENTES) {
        printf("Limite de clientes atingido!\n");
        return;
    }
    
    Conta novaConta;
    
    printf("\n--- CRIAR NOVA CONTA ---\n");
    printf("Nome do cliente: ");
    scanf(" %[^\n]", novaConta.nome);
    printf("Numero da conta: ");
    scanf("%d", &novaConta.numeroConta);
    
    // Verificar se o número da conta já existe
    for (int i = 0; i < totalClientes; i++) {
        if (clientes[i].numeroConta == novaConta.numeroConta) {
            printf("Erro: Numero de conta ja existe!\n");
            return;
        }
    }
    
    novaConta.saldo = 0.0;
    clientes[totalClientes] = novaConta;
    totalClientes++;
    
    printf("Conta criada com sucesso!\n");
}

void depositar() {
    int numeroConta;
    float valor;
    
    printf("\n--- DEPOSITAR ---\n");
    printf("Numero da conta: ");
    scanf("%d", &numeroConta);
    
    for (int i = 0; i < totalClientes; i++) {
        if (clientes[i].numeroConta == numeroConta) {
            printf("Valor a depositar: ");
            scanf("%f", &valor);
            
            if (valor <= 0) {
                printf("Erro: Valor invalido!\n");
                return;
            }
            
            clientes[i].saldo += valor;
            printf("Deposito realizado com sucesso!\n");
            printf("Novo saldo: R$ %.2f\n", clientes[i].saldo);
            return;
        }
    }
    
    printf("Conta nao encontrada!\n");
}

void sacar() {
    int numeroConta;
    float valor;
    
    printf("\n--- SACAR ---\n");
    printf("Numero da conta: ");
    scanf("%d", &numeroConta);
    
    for (int i = 0; i < totalClientes; i++) {
        if (clientes[i].numeroConta == numeroConta) {
            printf("Saldo atual: R$ %.2f\n", clientes[i].saldo);
            printf("Valor a sacar: ");
            scanf("%f", &valor);
            
            if (valor <= 0) {
                printf("Erro: Valor invalido!\n");
                return;
            }
            
            if (valor > clientes[i].saldo) {
                printf("Erro: Saldo insuficiente!\n");
                return;
            }
            
            clientes[i].saldo -= valor;
            printf("Saque realizado com sucesso!\n");
            printf("Novo saldo: R$ %.2f\n", clientes[i].saldo);
            return;
        }
    }
    
    printf("Conta nao encontrada!\n");
}

void consultarSaldo() {
    int numeroConta;
    
    printf("\n--- CONSULTAR SALDO ---\n");
    printf("Numero da conta: ");
    scanf("%d", &numeroConta);
    
    for (int i = 0; i < totalClientes; i++) {
        if (clientes[i].numeroConta == numeroConta) {
            printf("Cliente: %s\n", clientes[i].nome);
            printf("Numero da conta: %d\n", clientes[i].numeroConta);
            printf("Saldo: R$ %.2f\n", clientes[i].saldo);
            return;
        }
    }
    
    printf("Conta nao encontrada!\n");
}

void listarClientes() {
    printf("\n--- LISTA DE CLIENTES ---\n");
    
    if (totalClientes == 0) {
        printf("Nenhum cliente cadastrado.\n");
        return;
    }
    
    for (int i = 0; i < totalClientes; i++) {
        printf("\nCliente %d:\n", i + 1);
        printf("Nome: %s\n", clientes[i].nome);
        printf("Conta: %d\n", clientes[i].numeroConta);
        printf("Saldo: R$ %.2f\n", clientes[i].saldo);
    }
}

void menu() {
    int opcao;
    
    do {
        printf("\n=== BANCO SIMPLES ===\n");
        printf("1. Criar conta\n");
        printf("2. Depositar\n");
        printf("3. Sacar\n");
        printf("4. Consultar saldo\n");
        printf("5. Listar clientes\n");
        printf("6. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);
        
        switch(opcao) {
            case 1:
                criarConta();
                break;
            case 2:
                depositar();
                break;
            case 3:
                sacar();
                break;
            case 4:
                consultarSaldo();
                break;
            case 5:
                listarClientes();
                break;
            case 6:
                printf("Obrigado por usar nosso banco!\n");
                break;
            default:
                printf("Opcao invalida!\n");
        }
        
    } while(opcao != 6);
}

int main() {
    menu();
    return 0;
}
