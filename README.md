


Future at Work – Assistente de Requalificação

O Future at Work é um assistente interativo em Python desenvolvido para auxiliar pessoas em processo de requalificação profissional. O sistema identifica lacunas de competências, compara as habilidades do usuário com ocupações em ascensão e gera um plano de desenvolvimento personalizado, além de um relatório em arquivo .txt.

Este projeto foi desenvolvido como parte de uma entrega acadêmica, utilizando conceitos essenciais de lógica de programação, estruturas de decisão, listas, funções, manipulação de arquivos e interação com o usuário.

Objetivo

O assistente tem como propósito orientar usuários que desejam migrar de carreira ou aprimorar suas habilidades, oferecendo:

Visualização de carreiras do futuro e suas skills essenciais

Comparação entre skills do usuário e skills requeridas

Identificação de competências faltantes

Geração automática de um plano básico de estudo

Emissão de relatório em arquivo de texto

Funcionalidades
1. Cadastro de Competências

O usuário pode adicionar ou remover competências que já possui, formando seu perfil inicial.

2. Consulta de Carreiras do Futuro

O sistema apresenta uma lista de ocupações relevantes, com descrição e habilidades principais associadas.

3. Análise de Gap de Skills

Com base no objetivo escolhido, o assistente compara as habilidades do usuário com as habilidades exigidas pela carreira desejada.

4. Geração de Plano de Ação

O sistema cria um plano simples e direto para orientar o desenvolvimento das habilidades faltantes.

5. Exportação de Relatório

Após a análise, um arquivo relatorio_future_at_work_simples.txt é gerado contendo:

Nome do usuário

Carreira alvo

Competências informadas

Skills já compatíveis

Skills faltantes

Plano de estudo sugerido

Estrutura do Código

O projeto utiliza:

Variáveis globais para armazenar dados do usuário

Funções modulares para cada etapa do processo

Laço while e estruturas condicionais para o menu

try/except para tratamento de erros

Manipulação de arquivos para geração do relatório

Como Executar

Certifique-se de ter Python instalado.

Salve o código em um arquivo .py (por exemplo, future_at_work.py).

Execute o programa no terminal:

python future_at_work.py


Siga as instruções exibidas no menu interativo.

Requisitos

Python 3.x

Nenhuma biblioteca externa é necessária

Observação

O código inclui uma validação para execução direta utilizando:

if _name_ == "_main_":
    rodar_menu()

# FUTURE AT WORK – ASSISTENTE DE REQUALIFICAÇÃO
#
# Joan Ferreira - RM: 562913
# Gabriel Salles - RM: 563584


# VARIÁVEIS GLOBAIS
OCUPACOES_DATA = [
    ("Analista de Dados", ["Python", "SQL", "Estatística"], "Profissional que analisa dados e gera insights."),
    ("Especialista em IA", ["Python", "Machine Learning", "Prompt Engineering"], "Profissional que cria soluções com inteligência artificial."),
    ("Desenvolvedor Low-Code", ["Automação", "Lógica", "APIs"], "Profissional que cria sistemas usando plataformas visuais.")
]

NOME_USUARIO = ""
SKILLS_USUARIO = []


# FUNÇÕES PRINCIPAIS

def mostrar_carreiras():
    """Exibe as carreiras disponíveis (Nome e Descrição)."""
    print("\nCarreiras disponíveis (Carreira, Skills Requeridas, Descrição):\n")
    for nome, skills, descricao in OCUPACOES_DATA: 
        print(f" - {nome}: {descricao}")
        print(f"    Skills Chave: {', '.join(skills)}") 

def buscar_skills_requeridas(objetivo):
    """Retorna a lista de skills necessárias para uma ocupação."""
    for nome, skills, _ in OCUPACOES_DATA:
        if nome.lower() == objetivo.lower():
            return skills
    return []

def avaliar_competencias(skills_do_usuario, objetivo):
    """Compara as skills do usuário com as skills requeridas para o objetivo."""
    requeridas = buscar_skills_requeridas(objetivo)
    ja_possui = []
    a_aprender = []

    skills_usuario_norm = [s.lower() for s in skills_do_usuario]

    for skill_req in requeridas:
        if skill_req.lower() in skills_usuario_norm:
            ja_possui.append(skill_req)
        else:
            a_aprender.append(skill_req)

    return ja_possui, a_aprender

def plano_de_estudo(faltas):
    """Gera um plano básico de estudo."""
    if not faltas:
        return ["Você já possui todas as habilidades essenciais! Parabéns!"]

    plano = []
    for skill in faltas:
        plano.append(f"-> Focar em {skill}: Dedicar 2 semanas à compreensão de seus fundamentos.")

    return plano


def salvar_analise(objetivo, skills_user, possui, faltas, plano):
    """Gera um relatório .txt com a análise completa (Manipulação de Arquivos)."""
    try:
        with open("relatorio_future_at_work_simples.txt", "w", encoding="utf-8") as f:
            f.write("RELATÓRIO DE ANÁLISE DE REQUALIFICAÇÃO\n")
            f.write(f"Nome do Participante: {NOME_USUARIO}\n")
            f.write(f"Meta Profissional: {objetivo}\n\n")

            f.write("Habilidades Informadas:\n")
            for s in skills_user:
                f.write(f" - {s}\n")

            f.write("\nSkills Compatíveis (Já possui):\n")
            for s in possui:
                f.write(f" - {s}\n")

            f.write("\nSkills a Desenvolver (Faltantes):\n")
            for s in faltas:
                f.write(f" - {s}\n")

            f.write("\nPlano de Ação Sugerido:\n")
            for r in plano:
                f.write(f" {r}\n")

        print("\n[SUCESSO] Relatório de Análise salvo em: relatorio_future_at_work_simples.txt")

    except Exception as e:
        print(f"[ERRO] Falha ao salvar o relatório: {e}")


# PROGRAMA PRINCIPAL

def rodar_menu():
    """Função principal que gerencia a interação do usuário (while, if/elif/else, try/except)."""
    global NOME_USUARIO, SKILLS_USUARIO 

    print("FUTURE AT WORK – ASSISTENTE DE REQUALIFICAÇÃO")

    NOME_USUARIO = input("Por favor, digite seu nome: ").strip()

    while True:
        print("\nMenu de Opções:")
        print("1 - Adicionar Competência")
        print("2 - Remover Competência")
        print("3 - Visualizar Carreiras do Futuro")
        print("4 - INICIAR ANÁLISE e gerar plano")
        print("5 - Sair do Assistente")

        try:
            opcao = int(input("Escolha o número da opção desejada: "))
        except ValueError:
            print("[ALERTA] Entrada inválida. Digite apenas o número da opção.")
            continue

        if opcao == 1:
            skill = input("Digite a nova competência: ").strip()
            if skill:
                SKILLS_USUARIO.append(skill)
                print(f"Competência '{skill}' adicionada.")

        elif opcao == 2:
            if not SKILLS_USUARIO:
                print("Sua lista de competências está vazia.")
                continue

            print("\nSuas Competências Atuais:")
            for i, s in enumerate(SKILLS_USUARIO, 1):
                print(f" {i}. {s}")

            remove_str = input("Qual competência deseja remover? (Digite o nome exato): ").strip()
            
            try:
                SKILLS_USUARIO.remove(remove_str)
                print(f"Competência '{remove_str}' removida.")
            except ValueError:
                print("[ALERTA] Competência não encontrada. Verifique a escrita.")

        elif opcao == 3:
            mostrar_carreiras()

        elif opcao == 4:
            mostrar_carreiras()
            objetivo = input("\nDigite exatamente o nome da carreira alvo: ").strip()

            requeridas = buscar_skills_requeridas(objetivo)
            if not requeridas:
                print("[ERRO] Carreira não reconhecida. Tente novamente.")
                continue

            possui, faltas = avaliar_competencias(SKILLS_USUARIO, objetivo)
            plano = plano_de_estudo(faltas)

            print("\nRELATÓRIO RÁPIDO")
            print(f"Total de skills requeridas: {len(requeridas)}")
            print(f"Skills que VOCÊ POSSUI: {len(possui)}")
            
            print("\n- Skills que você já tem (Compatíveis):")
            for s in possui:
                print(f"    -> {s}")

            print("\n- Skills que faltam (A desenvolver):")
            for s in faltas:
                print(f"    -> {s}")

            print("\nPLANO DE AÇÃO")
            for r in plano:
                print(f" {r}")
            
            salvar_analise(objetivo, SKILLS_USUARIO, possui, faltas, plano)

        elif opcao == 5:
            print("Saindo do assistente. Sucesso em sua requalificação!")
            break

        else:
            print("[ALERTA] Opção fora do intervalo (1-5). Tente novamente.")
if _name_ == "_main_":
    rodar_menu() esse aqui
