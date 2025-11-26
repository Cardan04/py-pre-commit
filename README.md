# py-pre-commit

# 🛡️ Guia de Qualidade de Código (Pre-Commit)

Este projeto utiliza o framework **`pre-commit`** como a nossa primeira linha de defesa para garantir a qualidade, consistência e conformidade com os padrões de estilo do código Python.

É **obrigatório** que todos os desenvolvedores instalem e usem o `pre-commit` para evitar que erros de formatação, linting ou padrões indesejados (como a função `print()`) cheguem ao nosso repositório principal.

## 1. 🔍 Importância da Dupla Camada de Defesa

Nós utilizamos uma abordagem de **duas camadas** para a qualidade do código:

| Camada | Ferramenta | Onde Roda | Propósito |
| :--- | :--- | :--- | :--- |
| **1ª Linha** (Local) | `pre-commit` (via `.pre-commit-config.yaml`) | Na sua máquina (`git commit`) | **Velocidade:** Feedback instantâneo e correção automática. |
| **2ª Linha** (Remota) | GitHub Actions (via `.github/workflows/`) | No servidor do GitHub (`git push` / PR) | **Garantia:** Bloqueia o merge se alguém ignorar o hook local. |

## 2. 📝 Arquivos de Configuração

Os arquivos essenciais para o nosso sistema de qualidade são:

### A. `.pre-commit-config.yaml` (Raiz do Projeto)

Este arquivo define quais **hooks** (verificações) serão executados.

* **Função:** É o manifesto que lista todas as ferramentas de qualidade que devem ser rodadas no *commit*.
* **Exemplo de Hook em Uso:**
    * Possui um hook local configurado com `grep` que **bloqueia** qualquer chamada à função `print()` em arquivos `.py` para garantir o uso de bibliotecas de *logging* adequadas.
    * (Se você tiver) Outras ferramentas como `black` (formatador) e `flake8` (linter) também estariam listadas aqui.

### B. `.github/workflows/` (Pastas)

Esta pasta contém os fluxos de trabalho do GitHub Actions (Ex: `bloqueia_print.yml`).

* **Função:** É o nosso sistema de Integração Contínua (CI). Ele executa **após** o código ser enviado ao GitHub, atuando como a rede de segurança.
* **Importância:** Mesmo que um desenvolvedor use `git commit --no-verify`, o Action **falhará** no servidor, e o Pull Request será **bloqueado** devido às Regras de Proteção de Branch.

---

## 3. 🛠️ Como Instalar e Usar o Pre-Commit

Siga estes passos **em seu repositório local** para ativar os hooks definidos no `.pre-commit-config.yaml`.

### Passo 1: Instalar o Framework

Certifique-se de que você tem o Python e o `pip` instalados e, em seguida, instale o framework `pre-commit`:

```bash
pip install pre-commit
