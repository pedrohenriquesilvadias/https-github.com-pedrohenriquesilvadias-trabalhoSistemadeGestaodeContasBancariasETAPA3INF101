Conteúdo: Trabalho Sistema de Gestão de Contas Bancárias ETAPA 3

Nome: Pedro Henrique Silva Dias

Matrícula: 28780

Disciplina: INF-101 Programação de Computadores I

Neste trabalho, descobri que deve se declarar as variáveis com arrays MAX_CONTAS E MAX_MOVIMENTAÇÕES da etapa 2 e as variáveis da etapa 3 o void salvar/
carregar contas/movimentações na qual foi usado o "ofstream" no salvar e "ifstream" no carregar através do <fstream> antes de declarar o "int main();".

O salvarContas(); e o salvarMovimentações teve de ser declarados antes do break (nos códigos declarados na etapa 2). 

O arquivo.close(); obrigatoriamente declarado depois de quantidadeContas (=0, ++) serve para encerrar o arquivo depois de ler ou escrever os dados nele.

Foi usado o void carregarContas; o while (getline(arquivo, temp, ';')), getline(arquivo, nomeCliente[quantidadeContas], ';'); getline(arquivo, cpf[quantidadeContas], ';'); getline(arquivo, temp, ';'); tipoConta[quantidadeContas] = stoi(temp); contaAtiva[quantidadeContas] = true;
getline(arquivo, temp, ';'); saldo[quantidadeContas] = stod(temp);

Na Etapa 2, a objetivo era, cadastrar contas, listar contas cadastradas, consultar contas, realizar depósitos, saques transferências, e exibir
o extrato usando string, bool, do-while, switch opcao, for e cases, declarar novas variáveis a cada case e a variável double valor foram declarados como 
value, valeur e elValor pois variáveis não podem se repetir.

Primeiro digita o número da conta nome, cpf, tipo da conta e saldo para cadastrar, listar, consultar, fazer depósitos, saques, transferências, emitir
extratos e por fim sair.

Na etapa 3, depois de todos de fazer todo esse processo acima e escolhido a opção 8 sair (na etapa 2), abre duas novas abas do online GDB:, a contas.txt com o número da conta, nome, conta poupança ou corrente e saldo declarados e a movimentacoes.txt com o número da conta, tipo depósito ou saque e o saldo depositado/sacado.

Depois do int main, declara carregarContas e carregarMovimentacoes antes de copiar os códigos declarados na etapa 2.

*Foi necessário a remoção das setinhas (< >) no iostream, fstream e string pois eles não apareciam na aba visualizar, apareciam apenas o include.

*Link de acesso: [trabalho-etapa-3-sistema-bancario.zip](https://github.com/user-attachments/files/35413663/trabalho-etapa-3-sistema-bancario.zip).
Os códigos estão no "main", vai abrir no VS Code.

*O código abaixo caso vc não consiga acessar os códigos declarados no link acima.

#include iostream

#include fstream

#include string

using namespace std;

//Variáveis para controle das contas

const int MAX_CONTAS = 100; // é previsto um limite máximo de 100 contas

//2.1 Dados das contas

int numeroConta[MAX_CONTAS]; //<-Array

string nomeCliente[MAX_CONTAS];

string cpf[MAX_CONTAS];

int tipoConta[MAX_CONTAS];

double saldo[MAX_CONTAS];

bool contaAtiva[MAX_CONTAS];

int quantidadeContas = 0; //conta quantas contas estão cadastradas; vai ter que ser somada +1

//2.2 Histórico de movimentações

const int MAX_MOVIMENTACOES = 500;

int contaMovimentacao[MAX_MOVIMENTACOES];

char tipoMovimentacao[MAX_MOVIMENTACOES];

double valorMovimentacao[MAX_MOVIMENTACOES];

int quantidadeMovimentacoes = 0;

int opcao;

void carregarContas() {

    ifstream arquivo("contas.txt");
    
    if (!arquivo.is_open()) {
        
        return; // Se o arquivo não existe (1ª execução), apenas sai sem erro
    
    }

    quantidadeContas = 0;
    
    string temp;

    // Lê até o primeiro ';' (número da conta). Se conseguir ler, há uma linha válida
    
    while (getline(arquivo, temp, ';')) {
        
        if (temp == "") break; // Evita ler linha em branco no final do arquivo
        
        numeroConta[quantidadeContas] = stoi(temp);

        getline(arquivo, nomeCliente[quantidadeContas], ';');
        
        getline(arquivo, cpf[quantidadeContas], ';');

        getline(arquivo, temp, ';');
        
        tipoConta[quantidadeContas] = stoi(temp);

        getline(arquivo, temp, ';');
        
        saldo[quantidadeContas] = stod(temp);

        // O último campo da linha termina com quebra de linha ('\n'), não com ';'
        
        getline(arquivo, temp);
        
        contaAtiva[quantidadeContas] = stoi(temp);

        quantidadeContas++;
    }
    arquivo.close();
}

void salvarContas() {
    
    ofstream arquivo("contas.txt");
    
    if (arquivo.is_open()) {
        
        for (int i = 0; i < quantidadeContas; i++) {
            
            arquivo << numeroConta[i] << ";"
                    
                    << nomeCliente[i] << ";"
                    
                    << cpf[i] << ";"
                    
                    << tipoConta[i] << ";"
                    
                    << saldo[i] << ";"
                    
                    << contaAtiva[i] << endl;
        
        }
        
        arquivo.close();
    
    }

}

void carregarMovimentacoes() {
    
    ifstream arquivo("movimentacoes.txt");
    
    if (!arquivo.is_open()) {
        
        return;
    
    }

    quantidadeMovimentacoes = 0;
    string temp;

    while (getline(arquivo, temp, ';')) {
        if (temp == "") break;
        contaMovimentacao[quantidadeMovimentacoes] = stoi(temp);

        getline(arquivo, temp, ';');
        tipoMovimentacao[quantidadeMovimentacoes] = temp[0]; // Pega o caractere 'D' ou 'S'

        getline(arquivo, temp);
        valorMovimentacao[quantidadeMovimentacoes] = stod(temp);

        quantidadeMovimentacoes++;
    }
    arquivo.close();
}

void salvarMovimentacoes() {
    
    ofstream arquivo("movimentacoes.txt");
    if (arquivo.is_open()) {
        for (int i = 0; i < quantidadeMovimentacoes; i++) {
            arquivo << contaMovimentacao[i] << ";"
                    << tipoMovimentacao[i] << ";"
                    << valorMovimentacao[i] << endl;
        }
        arquivo.close();
    }
}
    
int main() {
    
    carregarContas();         
    carregarMovimentacoes();
    
    //MENU
    //2.3 Funcionalidades obrigatórias
    do {
        cout<< "=========================================" << endl;
        cout<< "  SISTEMA DE GESTÃO DE CONTAS BANCARIAS  " << endl;
        cout<< "=========================================" << endl;
        cout<< "Escolha uma opção: " << endl;
        cout<< "1- Cadastrar contas " << endl;
        cout<< "2- Listar contas cadastradas " << endl;
        cout<< "3- Consultar conta " << endl;
        cout<< "4- Realizar depósito " << endl;
        cout<< "5- Realizar saque " << endl;
        cout<< "6- Realizar transferência " << endl;
        cout<< "7- Exibir extrato " << endl;
        cout<< "8- Sair " << endl;
        cout<< "Escolha uma opção: ";
        cin>> opcao;
        
        
        switch (opcao) {
            case 1: { //1. Cadastrar contas
                if (quantidadeContas >= MAX_CONTAS) {
                    cout<< "Limite máximo atingido de contas!" << endl;
                    break;
                }
                
                int num;
                cout<< "=== CADASTRO DE NOVA CONTA ===" << endl;
                cout<< "NÚmero da conta: ";
                cin>> num;

                // Verificar se a conta já existe
                bool contaExiste = false;
                for (int i = 0; i < quantidadeContas; i++) {
                    if (numeroConta[i] == num) {
                        contaExiste = true;
                        break;
                    }
                }

                if (contaExiste) {
                    cout<< "[ERRO] Já existe uma conta cadastrada com este número!" << endl;
                } else {
                    numeroConta[quantidadeContas] = num;
                    cout<< "=== CADASTRO DE CONTA ===" << endl;
                    cout<< "Número da conta NOVAMENTE: ";
                    cin>> numeroConta[quantidadeContas];
                    cout<< "Nome do Cliente: ";
                    cin.ignore();
                    getline (cin, nomeCliente[quantidadeContas]);
                    cout<< "CPF: ";
                    getline (cin, cpf[quantidadeContas]);
                    cout<< "Tipo da conta (1- Corrente, 2- Poupança): ";
                    cin>> tipoConta[quantidadeContas];
                    cout<< "Saldo inicial: R$ ";
                    cin>> saldo[quantidadeContas];

                    contaAtiva[quantidadeContas] = true;
                    quantidadeContas++;//quantidadeContas = quantidadeContas + 1
                    
                    salvarContas();
                    
                    cout<< "Conta cadastrada com sucesso!" << endl;
                }
                break;
            }
            
            case 2: { // 2. Listar as contas cadastradas
                cout<< "=== LISTA DE CONTAS CADASTRADAS ===" << endl;
                if (quantidadeContas == 0) {
                    cout<< "Nenhuma conta cadastrada no sistema." << endl;
                } else {
                    for (int i = 0; i < quantidadeContas; i++) {
                        cout<< "----------------------------------" << endl;
                        cout<< " CONTA " << i << ":" << endl;
                        cout<< "Número da Conta: " << numeroConta[i] << endl;
                        cout<< "Cliente: " << nomeCliente[i] << endl;
                        cout<< "CPF: " << cpf[i] << endl;
                        cout<< "Tipo: " << (tipoConta[i] == 1 ? "Corrente" : "Poupança") << endl;
                        cout<< "Saldo: R$ " << saldo[i] << endl;
                        cout<< "Status: " << (contaAtiva[i] ? "Ativa" : "Inativa") << endl;
                    }
                    cout<< "--------------------------------------" << endl;
                }
                break;
            }
                
            case 3: { // 3. Consultar uma conta pelo número
                int numConsulta;
                cout<< "=== CONSULTAR CONTA ===" << endl;
                cout<< "Digite o número da conta: ";
                cin>> numConsulta;
                
                int indiceEncontrado = -1;
                for (int i = 0; i < quantidadeContas; i++) {
                    if (numeroConta[i] == numConsulta) {
                        indiceEncontrado = i;
                        break;
                    }
                }
                
                if (indiceEncontrado == -1) {
                    cout<< "[ERRO] Conta não encontrada!" << endl;
                } else {
                    cout<< "=== CONTA ENCONTRADA ===" << endl;
                    cout<< "Número: " << numeroConta[indiceEncontrado] << endl;
                    cout<< "Cliente: " << nomeCliente[indiceEncontrado] << endl;
                    cout<< "CPF: " << cpf[indiceEncontrado] << endl;
                    cout<< "Saldo: R$ " << saldo[indiceEncontrado] << endl;
                    cout<< "Status: " << (contaAtiva[indiceEncontrado] ? "Ativa" : "Inativa") << endl;
                }
                break;
            }

            case 4: { // 4. Realizar depósitos
                int numDeposito;
                double value;
                cout<< "=== REALIZAR DEPÓSITO ===" << endl;
                cout<< "Número da conta: ";
                cin>> numDeposito;

                int idxDeposito = -1;
                for (int i = 0; i < quantidadeContas; i++) {
                    if (numeroConta[i] == numDeposito) {
                        idxDeposito = i;
                        break;
                    }
                }

                if (idxDeposito == -1) {
                    cout<< "[ERRO] Conta não encontrada!" << endl;
                } else if (!contaAtiva[idxDeposito]) {
                    cout<< "[ERRO] Conta inativa! Não é possível depositar." << endl;
                } else {
                    cout<< "Valor do depósito: R$ ";
                    cin>> value;

                    if (value <= 0) {
                        cout<< "[ERRO] O valor do depósito deve ser positivo!" << endl;
                    } else if (quantidadeMovimentacoes >= MAX_CONTAS) {
                        cout<< "[ERRO] Limite de movimentações atingido!" << endl;
                    } else {
                        saldo[idxDeposito] = saldo[idxDeposito] + value;
                        contaMovimentacao[quantidadeMovimentacoes] = numeroConta[idxDeposito];
                        tipoMovimentacao[quantidadeMovimentacoes] = 'D';
                        valorMovimentacao[quantidadeMovimentacoes] = value;
                        quantidadeMovimentacoes++;

                        cout<< "Depósito realizado com sucesso!" << endl; 
                        cout<< "Novo saldo: R$ " << saldo[idxDeposito] << endl;
                    
                    salvarContas();
                    salvarMovimentacoes();   
                    }
                }
                break;
            }
            
            case 5: { // 5. Realizar saques, verificando saldo suficiente
                int numSaque;
                double valeur;
                
                cout<< "=== REALIZAR SAQUE ===" << endl;
                cout<< "Número da conta: ";
                cin>> numSaque;
                
                int idxSaque = -1;
                for (int i = 0; i < quantidadeContas; i++) {
                    if (numeroConta[i] == numSaque) {
                        idxSaque = i;
                        break;
                    }
                }

                if (idxSaque == -1) {
                    cout<< "[ERRO] Conta não encontrada!" << endl;
                } else if (!contaAtiva[idxSaque]) {
                    cout<< "[ERRO] Conta inativa! Não é possível sacar." << endl;
                } else {
                    cout<< "Valor do saque: R$ ";
                    cin>> valeur;

                    if (valeur <= 0) {
                        cout<< "[ERRO] O valor do saque deve ser positivo!" << endl;
                    } else if (saldo[idxSaque] < valeur) {
                        cout<< "[ERRO] Saldo insuficiente para realizar o saque!" << endl;
                    } else if (quantidadeMovimentacoes >= MAX_CONTAS) {
                        cout<< "[ERRO] Limite de movimentações atingido!" << endl;
                    } else {
                        // Atualiza saldo e registra movimentação
                        saldo[idxSaque] = saldo[idxSaque] - valeur;
                        contaMovimentacao[quantidadeMovimentacoes] = numeroConta[idxSaque];
                        tipoMovimentacao[quantidadeMovimentacoes] = 'S';
                        valorMovimentacao[quantidadeMovimentacoes] = valeur;
                        quantidadeMovimentacoes++;

                        cout<< "Saque realizado com sucesso!" << endl;
                        cout<< "Novo saldo: R$ " << saldo[idxSaque] << endl;
                    
                    salvarContas();
                    salvarMovimentacoes();
                    }
                }
                break;
            }
            
            case 6: { // 6. Realizar transferências entre duas contas
                int contaOrigem, contaDestino;
                double elValor;
                
                cout<< "=== REALIZAR TRANSFERENCIA ===" << endl;
                cout<< "Número da conta de ORIGEM: ";
                cin>> contaOrigem;
                cout<< "Número da conta de DESTINO: ";
                cin>> contaDestino;

                if (contaOrigem == contaDestino) {
                    cout<< "[ERRO] A conta de origem e destino não podem ser a mesma!" << endl;
                    break;
                }

                int idxOrigem = -1;
                int idxDestino = -1;

                for (int i = 0; i < quantidadeContas; i++) {
                    if (numeroConta[i] == contaOrigem) idxOrigem = i;
                    if (numeroConta[i] == contaDestino) idxDestino = i;
                }

                // Validações detalhadas exigidas no enunciado
                if (idxOrigem == -1) {
                    cout<< "[ERRO] Conta de origem não encontrada!" << endl;
                } else if (idxDestino == -1) {
                    cout<< "[ERRO] Conta de destino não encontrada!" << endl;
                } else if (!contaAtiva[idxOrigem] || !contaAtiva[idxDestino]) {
                    cout<< "[ERRO] Ambas as contas devem estar ativas!" << endl;
                } else {
                    cout<< "Valor da transferência: R$ ";
                    cin>> elValor;

                    if (elValor <= 0) {
                        cout<< "[ERRO] O valor da transferência deve ser positivo!" << endl;
                    } else if (saldo[idxOrigem] < elValor) {
                        cout<< "[ERRO] Saldo insuficiente na conta de origem!" << endl;
                    } else if (quantidadeMovimentacoes + 2 > MAX_CONTAS) {
                        cout<< "[ERRO] Espaço insuficiente no histórico para registrar a transferência!" << endl;
                    } else {
                    // Atualização dos saldos
                    saldo[idxOrigem] -= elValor;
                    saldo[idxDestino] += elValor;

                    // Registro saída na Origem ('S')
                    contaMovimentacao[quantidadeMovimentacoes] = numeroConta[idxOrigem];
                    tipoMovimentacao[quantidadeMovimentacoes] = 'S';
                    valorMovimentacao[quantidadeMovimentacoes] = elValor;
                    quantidadeMovimentacoes++;

                    // Registro entrada no Destino ('D')
                    contaMovimentacao[quantidadeMovimentacoes] = numeroConta[idxDestino];
                    tipoMovimentacao[quantidadeMovimentacoes] = 'D';
                    valorMovimentacao[quantidadeMovimentacoes] = elValor;
                    quantidadeMovimentacoes++;
                    
                    cout<< "[SUCESSO] Transferencia realizada com sucesso!" << endl;
                    cout<< "Novo saldo da conta " << numeroConta[idxOrigem] << ": R$ " << saldo[idxOrigem] << endl;
                    cout<< "Novo saldo da conta " << numeroConta[idxDestino] << ": R$ " << saldo[idxDestino] << endl;
                    
                    salvarContas();
                    salvarMovimentacoes();
                    }
                }
                break;
            }
            
            case 7: { // 7. Exibir o extrato de uma conta
                int numExtrato;
                cout<< "=== EXIBIR EXTRATO ===" << endl;
                cout<< "Número da conta: ";
                cin>> numExtrato;

                int idxExtrato = -1;
                for (int i = 0; i < quantidadeContas; i++) {
                    if (numeroConta[i] == numExtrato) {
                        idxExtrato = i;
                        break;
                    }
                }

                if (idxExtrato == -1) {
                    cout<< "[ERRO] Conta não encontrada!" << endl;
                } else {
                    cout<< "========================================" << endl;
                    cout<< "EXTRATO DA CONTA: " << numeroConta[idxExtrato] << " | Titular: " << nomeCliente[idxExtrato] << endl;
                    cout<< "========================================" << endl;
                    
                bool temMovimento = false;
                for (int i = 0; i < quantidadeMovimentacoes; i++) {
                    if (contaMovimentacao[i] == numeroConta[i]) {
                        int encontrouMov = true;
                        if (tipoMovimentacao[i] == 'D') {
                            cout<< "[Depósito]  + R$ " << valorMovimentacao[i] << endl;
                        } else if (tipoMovimentacao[i] == 'S') {
                            cout<< "[Saque/Sai] - R$ " << valorMovimentacao[i] << endl;
                        }
                    }
                }
                if (!temMovimento) {
                        cout<< "Nenhuma movimentação registrada para esta conta." << endl;
                    }
                    cout<< "----------------------------------------" << endl;
                    cout<< "Saldo atual: R$ " << saldo[idxExtrato] << endl;
                    cout<< "========================================" << endl;
                }
                
                break;
            }
            
            case 8:
                cout<< "Saindo..." << endl;
                break;
            
            default:
                cout<< "[INVALIDO]É obrigatório escolher essas opções. " << endl;
                break;
        }
        
    } while (opcao != 8);
    
    return 0;
}
