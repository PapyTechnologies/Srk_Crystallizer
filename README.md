# SRK-Crystallizer v2.1 (Industrial Engine)

Micro-moteur MCP d'édition chirurgicale de code à empreinte mémoire zéro, distribution binaire native C durcie (Anti-REA) et rollback atomique matériel.

---

## 1. RÉSUMÉ EXÉCUTIF

**SRK-Crystallizer v2.1** résout le goulet d'étranglement économique et physique des agents de code autonomes (Claude, OpenCode, Codex, Gemini) :
1. **Élimination de la réécriture intégrale :** Remplace les réécritures complètes de fichiers par des micro-patchs chirurgicaux atomiques (`srk_patch`).
2. **Préservation du KV-Cache :** Cartographie compacte des signatures AST (`srk_map`) et extraction ciblée (`srk_read`) pour diviser le flux de tokens d'entrée par plus de deux.
3. **Inviolabilité & Sécurité atomique :** Validation syntaxique AST in-memory avant écriture disque, protection anti-écrasement de secrets masqués, contrôle strict de collision SHA-256 (Stale SHA) et basculement atomique de pointeur de fichier (`os.replace`).
4. **Durcissement binaire natif :** Binaire x86-64 compilé en code machine natif via Nuitka C + Link-Time Optimization (LTO) scellé sans bytecode Python intermédiaire, immunisé contre les décompilateurs et agents de rétro-ingénierie (Anti-REA).

---

## 2. SYNTHÈSE DES MESURES & BENCHMARKS INDUSTRIELS [MESURÉ]

### Benchmark Comparatif A/B (Fichier système réel de 814 lignes)
Mesuré au tokenizer officiel `cl100k_base` via `tiktoken` :

| Métrique de Consommation | Condition Standard | SRK-Crystallizer v2.1 | Réduction Réelle [MESURÉ] |
| :--- | :---: | :---: | :---: |
| **Tokens d'Entrée (Input, poids x1.25)** | 9 268 tokens | 4 441 tokens | **-52.08%** |
| **Tokens de Sortie (Output, poids x5.0)** | 9 283 tokens | 15 tokens | **-99.84%** |
| **Total Tokens Bruts** | 18 551 tokens | 4 456 tokens | **-75.98%** |
| **Unités Quota Pondérées** | **58 000.00** | **5 626.25** | **-90.30%** |

$$\text{Formule Quota Officielle} = (\text{Tokens}_{\text{Entrée}} \times 1.25) + (\text{Tokens}_{\text{Sortie}} \times 5.0)$$

### Session Multi-Tours Déterministe (10 modifications séquentielles consécutives)
- **Tokens Entrée cumulés :** 8 992 vs 93 175 (**-90.35%**)
- **Tokens Sortie cumulés :** 110 vs 93 285 (**-99.88%**)
- **Économie Quota cumulé (10 tours) :** **-97.98%**

### Suite des 4 Épreuves de Robustesse Extrême
1. **Épreuve 1 (Formats & Encodages) :** Support natif mix CRLF/LF, texte arabe (`سيرفر`), accents et emojis. Diff chirurgical exact sur 1 ligne, zéro diff parasite.
2. **Épreuve 2 (Concurrence & Race Condition) :** 2 clients concurrents sur le même hash initial : exactement 1 commit valide (`OK`), 1 rejet immédiat (`ERR_STALE_SHA`), zéro corruption.
3. **Épreuve 3 (Stress AST & Grande Échelle) :** Parsing et patch validés sur 2 704 lignes avec structures asynchrones profondes sans dépassement de récursion ni fuite RAM.
4. **Épreuve 4 (Micro-Latence Locale CPU sur 50 itérations) :**
   - `srk_map` : Médiane = **74.97 ms** (Moyenne = 78.33 ms)
   - `srk_read` : Médiane = **76.22 ms** (Moyenne = 81.32 ms)
   - `srk_patch` : Médiane = **166.74 ms** (Moyenne = 179.10 ms)

---

## 3. GUIDE D'INTÉGRATION CLIENTS MCP

Le serveur MCP communique via le protocole standard JSON-RPC sur les flux `stdio`.

### Intégration Claude Desktop (`claude_desktop_config.json`)
```json
{
  "mcpServers": {
    "srk-crystallizer": {
      "command": "bin/srk-crystallizer.exe"
    }
  }
}
```

### Intégration OpenCode (`opencode.json`)
```json
{
  "mcp": {
    "srk-crystallizer": {
      "type": "local",
      "command": [
        "bin/srk-crystallizer.exe"
      ],
      "enabled": true
    }
  }
}
```

---

## 4. INTÉGRITÉ DU BINAIRE OFFICIEL

Pour vérifier l'authenticité et l'intégrité de l'exécutable compilé sans altération :

- **Fichier :** `bin/srk-crystallizer.exe`
- **Format :** Binaire natif x86-64 autonome (`onefile`, LTO, Stripped)
- **Taille :** 23 931 904 octets (22.82 Mo)
- **Empreinte SHA-256 officielle :**
  ```text
  89787a6dc5954054f3e037dd1b37a719f4c0499fd70da0278d82e626dbe87294
  ```

---

## 5. PROPRIÉTÉ INTELLECTUELLE & LICENCE

## License & Rights
This project is distributed under the Proprietary Binary Distribution License.  
Free to use and integrate across personal and enterprise MCP clients.  
Copyright © 2026 **PapyTechnologies**. All rights reserved.
