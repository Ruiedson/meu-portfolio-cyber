# Write-Up: PwnDrive Academy

**ATIVO:** PWNDRIVE ACADEMY (PWNTILLDAWN)  
**Autor:** H3XMZ  
**Data do Comprometimento:** 14 de Julho de 2026  
**Classificação:** Portfólio Técnico de Segurança Ofensiva  

---

## 1. Sumário Executivo

Este documento técnico detalha o processo de identificação, validação e exploração de segurança realizado no ativo PwnDrive Academy através da plataforma de laboratórios PwnTillDawn.

O objetivo deste teste foi simular a atuação de um atacante real sob a ótica de um Hacker Ético, mapeando a superfície de ataque exposta e demonstrando o impacto de negócio caso uma vulnerabilidade crítica fosse explorada por cibercriminosos.

Durante a análise, foi identificada uma falha crítica de execução remota de código (RCE) no protocolo de compartilhamento de arquivos SMBv1 (MS17-010 / EternalBlue). A exploração bem-sucedida permitiu comprometer integralmente a integridade do servidor Windows Server 2008 R2, garantindo acesso com o maior nível de privilégio existente no sistema operacional (`NT AUTHORITY\SYSTEM`).

---

## 2. Escopo do Alvo

O escopo da atividade foi limitado estritamente ao endereço IP disponibilizado pelo laboratório:

*   **Nome do Ativo:** PwnDrive Academy
*   **Endereço IP Alvo:** `10.150.150.11`
*   **Sistema Operacional:** Windows
*   **Dificuldade Oficial:** Fácil (Easy)
*   **IP de Ataque (VPN):** `10.66.66.114` (Interface `tun0`)

![Escopo do Alvo](./assets/1_escopo.png)

---

## 3. Fase de Reconhecimento & Varredura (Reconnaissance)

### 3.1 Estabelecimento do Túnel VPN
A conexão com o segmento de rede interna do laboratório foi realizada de forma segura através do protocolo OpenVPN. Devido à necessidade de criação e controle de adaptadores de rede virtuais (`tun`), o comando foi inicializado utilizando privilégios de superusuário (`sudo`).

```bash
sudo openvpn PwnTillDawn.ovpn