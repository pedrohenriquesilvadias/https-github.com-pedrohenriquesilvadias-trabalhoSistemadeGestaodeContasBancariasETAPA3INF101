Trabalho Sistema Bancário Etapa 3
Pedro Henrique Silva Dias-28780
Disciplina: INF-101 Programação de Computadores I
[trabalho-etapa-3-sistema-bancario.zip](https://github.com/user-attachments/files/35413663/trabalho-etapa-3-sistema-bancario.zip)

- Neste trabalho, descobri que deve se declarar as variáveis com arrays MAX_CONTAS E MAX_MOVIMENTAÇÕES da etapa 2 e as variáveis da etapa 3 o void salvar
contas e movimentações na qual foi usado o "ifstream" no carregar e "ofstream" no salvar através do <fstream> antes de declarar o "int main();".
O salvarContas(); e o salvarMovimentações teve de ser declarados antes do break. O arquivo.close(); serve pra gravar os arquivos depois de escolher
a opção 8 sair. Foi usado no void carregarContas; o while (getline(arquivo, temp, ';')), getline(arquivo, nomeCliente[quantidadeContas], ';');
getline(arquivo, cpf[quantidadeContas], ';'); getline(arquivo, temp, ';'); tipoConta[quantidadeContas] = stoi(temp); getline(arquivo, temp, ';');
saldo[quantidadeContas] = stod(temp);
Na Etapa 2, anderson a missão necessária era, cadastrar contas, listar contas cadastradas, consultar contas, realizar depósitos e saques,
