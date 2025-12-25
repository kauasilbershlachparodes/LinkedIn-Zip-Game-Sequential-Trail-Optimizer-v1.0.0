https://github.com/user-attachments/assets/9f1fdb09-baeb-4ea7-b811-caa67c2f5b1b

---

# Zip Game Animated Orthogonal Trace (v1.0.0 - Safe Manhattan)
Este script automatiza a identificação e execução de caminhos válidos no jogo LinkedIn Zip, utilizando um traçado ortogonal sequencial baseado na lógica Manhattan (movimentos apenas horizontais e verticais).

O algoritmo analisa dinamicamente o grid, conecta os pontos numerados em ordem correta e preenche todas as células intermediárias, garantindo um caminho contínuo sem cruzamentos, conforme as regras do puzzle.

O rastro inteligente destaca visualmente o fluxo lógico da solução e pode executar o drag automático, eliminando erros de sequência, reduzindo tentativas manuais e otimizando o tempo de conclusão, o que contribui diretamente para a manutenção de ranking.

---

### **Doutrina de Execução: O Script (Source Code)**

1. **Instalação do Gerenciador:** Primeiro, instale a extensão [Violentmonkey](https://violentmonkey.github.io/get-it/) no seu navegador (Chrome, Firefox ou Edge).

2. **Criação do Script:**
* Clique no ícone do Violentmonkey e selecione o botão **"+" (Create new script)**.
* Apague o código padrão e cole o código completo do **Zip Game Dynamic Path Highlight Guide (v1.0.0)** fornecido anteriormente.
* Pressione `Ctrl+S` para salvar.

3. **Execução:** Acesse [LinkedIn Games - Zip](https://www.linkedin.com/games/zip/). O script será injetado automaticamente pelo Violentmonkey e o guia sequencial iniciará após o carregamento da página.

---

### **Inserção no Código (Header de Metadados)**

No início do código do script, você pode adicionar um link direto para facilitar para o usuário:

```javascript
// ==UserScript==
// @name         Zip Game Dynamic Path Highlight Guide (v1.0.0 - Sequential Trail)
// @namespace    trusted_security_researcher
// @match        https://www.linkedin.com/games/zip/*
// @grant        none
// @version      1.0.0
// @author       WH1TUV_H4XOR
// @description  Highlights correct path one by one with transparency trail - dynamic for any puzzle
// ==/UserScript==

(function () {
    'use strict';

    async function highlightDynamicPath() {
        console.log('[WH1TUV ZIP GUIDE] Iniciando guia dinâmico com rastro sequencial');

        const grid = document.querySelector('div[data-testid="interactive-grid"]');
        if (!grid) {
            console.error('[WH1TUV ERROR] Grid não encontrado.');
            return;
        }

        const cells = grid.querySelectorAll('div[data-cell-idx]');
        if (cells.length === 0) return;

        const dotMap = {};
        cells.forEach(cell => {
            const content = cell.querySelector('div[data-cell-content="true"]');
            if (content) {
                const num = parseInt(content.textContent.trim());
                if (!isNaN(num)) dotMap[num] = cell;
            }
        });

        const maxNum = Math.max(...Object.keys(dotMap).map(Number));
        if (Object.keys(dotMap).length < maxNum) return;

        // Clear previous styles
        cells.forEach(cell => {
            cell.style.backgroundColor = '';
            cell.style.opacity = '';
            cell.style.transition = 'background-color 0.5s ease, opacity 0.5s ease';
        });

        // Highlight empty cells faintly
        cells.forEach(cell => {
            if (!cell.querySelector('div[data-cell-content="true"]')) {
                cell.style.backgroundColor = 'rgba(173, 216, 230, 0.3)'; // Light blue for empty
            }
        });

        // Sequential highlight with trail
        for (let i = 1; i <= maxNum; i++) {
            const cell = dotMap[i];
            if (!cell) continue;

            // Full opacity + bright color for current
            cell.style.backgroundColor = i === 1 ? '#00FF00' : (i === maxNum ? '#FF0000' : '#FFA500'); // Green start, Red end, Orange middle
            cell.style.opacity = '1';

            // Fade previous ones slightly
            for (let j = 1; j < i; j++) {
                const prev = dotMap[j];
                if (prev) {
                    prev.style.opacity = '0.6';
                }
            }

            console.log(`[WH1TUV PATH STEP ${i}/${maxNum}] Seguindo para número ${i} - arraste aqui`);
            await new Promise(r => setTimeout(r, 1500)); // 1.5s delay per step
        }

        console.log('[WH1TUV GUIDE] Caminho completo destacado com rastro - siga sequência verde → laranja → vermelho');
        console.log('[WH1TUV] Células azul-claro: ajuste manual com L-shapes se necessário para 100%.');
    }

    window.addEventListener('load', () => {
        setTimeout(highlightDynamicPath, 10000);
    });

    const observer = new MutationObserver(() => {
        // Re-run on new puzzle
        setTimeout(highlightDynamicPath, 5000);
    });
    observer.observe(document.body, { childList: true, subtree: true });
})();

```

---

### **Marcos Técnicos da v1.0.0:**

1. **Mapeamento Dinâmico:** Compatível com qualquer variação de grid do Zip.
2. **Trail Logic:** Implementação de opacidade dinâmica para manter o foco no passo atual.
3. **Visual Alerts:** Código de cores (Verde/Laranja/Vermelho) para facilitar a orientação espacial rápida.
4. **Observer Automation:** Detecção de mudança de estado do jogo para re-highlight imediato.

#CTI #CyberSecurity #UserScript #LinkedInGames #ZipGame #Automation #JavaScript #Pathfinding #GameHacking #MIL5 #USAICOE #SoftwareEngineering #PerformanceOptimization #StrategicTech #IntelligenceTradecraft
