lista1=[]

from random import randint
def registro(nome,sobrenome,idade,email,renda1,pai,mae,enem,cpf,cpf2,matricula,escolaridade_v):
    lista2=[]
    renda2=renda(renda1)
    nota=idade_enem(idade, enem)
    escolaridade_verificada = verificar_escolaridade_v(idade, escolaridade_v)

    print()
    print(30*"=",'Registro Aluno',30*'=')
    print()
    registro = f'Nome Completo: {nome} {sobrenome}\n'\
            f'Matricula: {matricula}\n' \
            f'Idade: {idade} \n' \
            f'Esolariade: {escolaridade_verificada}\n' \
            f'Emai: {email} \n'  \
            f'Cpf Aluno: {cpf}\n' \
            f'Cpf Dos Pais: {cpf2}\n' \
            f'Renda Familiar: {renda1} \n' \
            f'Nome Pai: {pai} \n' \
            f'Nome Mãe: {mae} \n' \
            f'Bolsa: {renda2} \n' \
            f'Nota Enem: {nota}'
    print()

    lista2.append(registro)
    lista1.append(lista2)
    return registro




def cadastro():
    print()
    print(30*'=','Cadastro Aluno',30*'=')
    print()

    ale=randint(1000,4000)

    matricula=ale
    while True:
        nome = input('Digite Nome: ')
        if nome.isalpha():
            break
        else:
            print("Nome deve conter apenas letras. Tente novamente.")

    while True:
        sobrenome = input('Digite Sobrenome: ')
        if sobrenome.isalpha():
            break
        else:
            print("Sobrenome deve conter apenas letras. Tente novamente.")


    while True:
        idade_input = input("Digite idade: ")
        if idade_input.isdigit():  # Verifica se a entrada contém apenas dígitos
            idade = int(idade_input)
            break
        else:
            print("Por favor, digite apenas números para a idade.")

    if idade >=18:
        cpf2=0

        while True:
            cpf_input = input("Digite Cpf: ")
            if cpf_input.isdigit() and len(cpf_input) == 11:
                cpf = int(cpf_input)
                break
            else:
                print('Digite apenas números válidos para o CPF (11 dígitos).')


    elif idade < 18:
        cpf=f'Sem cpf'
        while True:
            cpf2_input = input("Digite Cpf Da filiação: ")
            if cpf2_input.isdigit() and len(cpf2_input) == 11:
                cpf2 = int(cpf2_input)
                break
            else:
                print('Digite apenas números válidos para o CPF (11 dígitos).')

    if idade < 16:
      enem=0
    elif idade >= 16:
      enem=float(input(f'Digite Nota Enem: '))

    email=input("Digite Email: ")
    while '@' and '.com' not in email:
        print("E-mail deve conter o caractere '@' e .com. Tente novamente.")
        email = input("Digite Email: ")
    renda1=float(input('Digite Renda Familiar: '))
    pai=input('Digite Nome Pai: ')
    mae=input('Digite Nome Mãe: ')
    priodo_escolar()
    escolaridade_v=input("Digite Escolaridade: ")
    registro(nome,sobrenome,idade,email,renda1,pai,mae,enem,cpf,cpf2,matricula,escolaridade_v)
    idade_enem(idade,enem)
    renda(renda1)
    for x in lista1:
        for vv in x:
            print(vv)
    print()

    menu()

def verificar_escolaridade_v(idade, escolaridade_v):
    faixas_etarias = {
        (0, 5): 'Pré-Maternal',
        (6, 7): '1º Ano',
        (7, 8): '2º Ano',
        (8, 9): '3º Ano',
        (9, 10): '4º Ano',
        (11, 12): '5º Ano',
        (12, 13): '6º Ano a 9º Ano',
        (13, 14): '1º Ano  Médio',
        (15, 16): '2º Ano  Médio',
        (17, 18): '3º Ano  Médio'
    }

    for faixa, escolaridade_correta in faixas_etarias.items():
        if faixa[0] <= idade <= faixa[1] and escolaridade_v == escolaridade_correta:
            return 'Escolaridade Certa'
        elif idade < faixa[0] and escolaridade_v == escolaridade_correta:
            return 'Escolaridade Adiantada'
        elif idade > faixa[1] and escolaridade_v == escolaridade_correta:
            return 'Escolaridade Atrasada'

    return 'Escolaridade Errada'




def renda(renda1):
    salario=float(1433)
    if renda1 <= salario:
        bolsa=f'100%'
        return bolsa
    elif renda1 < 2 * salario:
        bolsa=f'50%'
        return bolsa
    elif renda1 < 3 * salario:
        bolsa=f'30%'
        return bolsa
    elif renda1 > 3 * salario:
      bolsa=f'Sem Beneficio Da Bolsa'
      return bolsa



def idade_enem(idade,enem):
    nota=enem
    idade1=idade

    if idade < 16 and enem == 0:
      nota1='Sem Idade Para Ter Nota'
      return nota1
    elif idade1 >= 16 and nota >= 500:
        nota1=f'Passou Na media!'
        return nota1
    elif idade1 >= 16 and nota < 500:
        nota1=f'Média Baixa!'
        return nota1

def priodo_escolar():

  print('==========Digite A Escolaridade Correspondente==========')
  print()
  print('Pré-MArtenal\n1°-Ano\n2°-Ano\n3°Ano\n4°-Ano\n5°-Ano\n6º Ano a 9º Ano\n1°-Ano Médio\n2°-Ano Médio\n3°-Ano Médio')
  print()


def menu():
    print()
    print(30*'=','Menu De Opções',30*'=')
    print()
    print("1-Novo Casdastro\n2-Consultar Registros\n3-Sair")
    print()
    resp=input('Escolha Uma opção: ')
    match resp:
        case '1':
            cadastro()
        case '2':
            for x in lista1:
                for vv in x:
                    print(vv)
        case '3':
            exit()

        case _:
            print('Invalido!')
            menu()


menu()
