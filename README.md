# Portal de Capacitação Ampernet Telecom 🚀

Este repositório contém o código-fonte da plataforma interna de simulação e treinamento para técnicos da **Ampernet Telecom**. O sistema simula o fluxo exato de atendimento de bots via Telegram, validando o conhecimento prático dos colaboradores através de interações realistas, cenários dinâmicos e uma avaliação final com emissão de certificado.

## 📋 Sumário
* [Visão Geral](#-visão-geral)
* [Estrutura dos Módulos](#-estrutura-dos-módulos)
* [Diretrizes de Comunicação](#-diretrizes-de-comunicação)
* [Tecnologias Utilizadas](#-tecnologias-utilizadas)
* [Como Executar](#-como-executar)

---

## 🔍 Visão Geral
O projeto é uma aplicação de página única (*Single Page Application*) que atua como um ambiente controlado de testes. O técnico insere seu nome completo e passa por uma trilha contendo 6 módulos práticos e informativos, culminando em um exame de 5 questões sobre os fluxos operacionais da empresa.

## 🛠 Estrutura dos Módulos

O portal está dividido em etapas sequenciais obrigatórias:
1. **Módulo 1 (Agendamento):** Fluxo de atendimento direcionado a ordens de serviço e contato com clientes (Ex: Cliente ausente, Não localizando endereço).
2. **Módulo 2 (Suporte TAC):** Simulação de suporte técnico para liberação de equipamentos e configurações (Ex: Liberação de ONU, Alteração de PPPoE).
3. **Módulo 3 (Suporte Inmap):** Fluxo voltado para falhas e problemas no aplicativo interno.
4. **Módulo 4 (Comercial):** Atendimento voltado para verificação de planos, upgrades e contratos junto ao time de BackOffice.
5. **Módulo 5 (Bot de Pedidos):** Fluxo automatizado estruturado para requisição de materiais por regionais, contendo etapas de confirmação de dados.
6. **Módulo 6 (Fluxo Padrão):** Seção teórica detalhando as boas práticas e regras de conduta na comunicação interna.
7. **Avaliação Final:** Sistema de prova dinâmica. É necessário acertar no mínimo **4 de 5 questões** para aprovação e liberação do certificado assinado digitalmente com o nome do colaborador.

---

## 📖 Diretrizes de Comunicação

O sistema instrui e avalia os técnicos com base nas seguintes regras de negócio da Ampernet:

* **Agendamento:** Responsável por direcionar as ordens de serviço e contato com clientes.
* **TAC:** Acionado para suporte, liberação de equipamentos ou auxílio em configurações.
* **Inmap:** Responsável pelo atendimento de falhas e suporte relacionados ao aplicativo.
* **Comercial:** Verificação de informações de planos e contratos dos clientes.
* **NOC:** Suporte avançado e monitoramento complexo. *Regra crucial:* O acionamento inicial deve ser feito via TAC, que fará o direcionamento ao NOC apenas quando necessário.

> 🚨 **Nota Importante:** Todas as interações ficam registradas no banco de dados, não sendo possível excluir ou editar mensagens. É fundamental manter a comunicação clara, objetiva e profissional.

---

## 💻 Tecnologias Utilizadas

* **HTML5** & **CSS3** (Estrutura e estilização de janelas de chat)
* **Tailwind CSS** (Estilização responsiva e interface em Dark Mode)
* **JavaScript (ES6+)** (Motores de estado dos bots, renderização de caixas de diálogo e lógica da avaliação)
* **Font Awesome v6.4.0** (Iconografia da interface)

---

## 🚀 Como Executar

Por ser um sistema construído puramente em cliente (*Client-Side Rendering*), não há necessidade de instalar dependências complexas ou servidores robustos:

1. Faça o clone deste repositório:
   ```bash
   git clone [https://github.com/SulivanF/Treniamento-Telegram.git](https://github.com/SulivanF/Treniamento-Telegram.git)
