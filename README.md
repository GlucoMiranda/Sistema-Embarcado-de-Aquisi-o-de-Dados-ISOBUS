Sistema Embarcado de Aquisição de Dados ISOBUS / J1939
Repositório oficial contendo o código-fonte, os artefatos de validação e os conjuntos de dados (datasets) empíricos desenvolvidos para a dissertação de mestrado: "Sistema Embarcado para Captura e Interpretação de Dados com Hardware de Baixo Custo e Software Dedicado", apresentada ao Programa de Pós-Graduação em Tecnologias Computacionais para o Agronegócio (PPGTCA) da UTFPR.

1. Descrição Arquitetural
Este repositório provê a infraestrutura de software para a captura passiva (sniffing), decodificação semântica em tempo real e análise de barramentos diferenciais agrícolas regidos pelas normas SAE J1939 e ISO 11783.

O projeto divide-se em três macrocomponentes:

- Embedded Sniffer (src/embedded_sniffer): Parser em Python projetado para execução em ambiente Linux embarcado (Raspberry Pi).
- Trace-Driven Simulator (src/simulation): Ferramental em malha fechada (Hardware-in-the-Loop) composto por firmware Arduino e injetor Windows para a replicação de logs de maquinário real no barramento.
- Desktop Interpreter (src/desktop_interpreter): Aplicação de instrumentação virtual para análise offline e escalonamento temporal de matrizes hexadecimais brutas.

2. Requisitos de Hardware e Dependências
Hardware:
- Raspberry Pi 5 (Mínimo 2GB RAM) operando Raspberry Pi OS.
- MKS Canable Pro V2.0 (Configurado com firmware candlelight).
- Transceptor MCP2515 e Arduino UNO Rev3 (Exclusivo para simulação em bancada).

Dependências de Software (Python 3.9+):
- python-can (Integração com abstração SocketCAN)
- tkinter (Renderização de IHM)

3. Organização do Conjunto de Dados (Data Provenance)
Os registros de validação estão alocados no diretório /data:
- /data/raw/: Matrizes hexadecimais brutas capturadas no campo. Inclui o tráfego cedido de um distribuidor Kuhn Accura e a instrumentação dinâmica de um trator John Deere 7230J.
- /data/ground_truth/: Dicionário de PGNs e gabarito analítico de conversão de escala e deslocamento (offset) baseados no Digital Annex da SAE.
- /data/processed/: Dados de telemetria já decodificados, estratificados por categorias operacionais e comparativos de latência (jitter temporal) frente à interface padrão-ouro (PEAK PCAN-USB Pro).

5. Auditoria de Qualidade de Software
As métricas de Complexidade Ciclomática de McCabe (MCC) e a análise estática executadas nas funções centrais de decodificação estão disponíveis em /tests/software_metrics/mccabe_radon_results.txt. A arquitetura atual reporta um índice médio correspondente à Classe A de testabilidade.
