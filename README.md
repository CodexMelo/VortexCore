🌀 VortexCore
![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)
![Paper](https://img.shields.io/badge/Paper-1.21.11-blue)
![Java](https://img.shields.io/badge/Java-21-orange)
![License](https://img.shields.io/badge/license-MIT-green)

🌀 **VortexCore v1.0.6**

**Sistema completo de Clãs, Vilas, Dungeons e Guerras para Minecraft Paper 1.21.11+**

Transforme seu servidor em um MMO real: clãs como cidades, guerras estratégicas com totens + boss líder, logística física limitada, dungeons por vila (com grupos de até 6 jogadores), cooldown individual e economia integrada via Vault.

**[⬇️ Download JAR](https://github.com/CodexMelo/VortexCore/releases) • [GitHub](https://github.com/CodexMelo/VortexCore)**

> ✅ **VERSÃO 1.0.6** \- Versão estável e otimizada! Reporte bugs nas Issues do GitHub

---

## 📋 ÍNDICE
* [📥 Download](#-download)
* [📥 Instalação](#-instalação)
* [⚙️ Configuração](#️-configuração)
* [🆕 Novidades da 1.0.6](#-novidades-da-106)
* [👑 Comandos de Clã](#-comandos-de-clã)
* [🏘️ Comandos de Vilas](#️-comandos-de-vilas)
* [🏛️ Comandos de Cidade (CITY)](#️-comandos-de-cidade-city)
* [🌀 Comandos de Dungeons](#-comandos-de-dungeons)
* [👥 Comandos de Grupos (Party)](#-comandos-de-grupos-party)
* [⚔️ Comandos de Guerra](#️-comandos-de-guerra)
* [🚚 Comandos de Logística](#-comandos-de-logística)
* [📜 Comandos de Quests](#-comandos-de-quests)
* [👤 Comandos de Chat](#-comandos-de-chat)
* [🎯 Placeholders](#-placeholders)
* [🔧 Permissões](#-permissões)
* [❓ FAQ](#-faq)
* [📝 Licença](#-licença)

---

## 📥 DOWNLOAD

O arquivo do plugin está hospedado no GitHub Releases.

**⬇️ [BAIXAR VORTEXCORE 1.0.6](https://github.com/CodexMelo/VortexCore/releases/download/v1.0.6/VortexCore-1.0.6.jar)**

**Alternativa:** [Ver todas as releases](https://github.com/CodexMelo/VortexCore/releases)

---

## 📥 INSTALAÇÃO

### **Requisitos:**
* Servidor **Paper 1.21.11** ou superior
* **Java 21** ou superior
* **Vault** (obrigatório)
* **PlaceholderAPI** (recomendado para placeholders)
* **WorldEdit** (opcional, para schematics de dungeons)

### **Passo a passo:**
1. Baixe o arquivo `VortexCore-1.0.6.jar` do link acima
2. Coloque na pasta `plugins/` do seu servidor
3. Reinicie o servidor
4. Configure os arquivos em `plugins/VortexCore/`

---

## ⚙️ CONFIGURAÇÃO

### **config.yml**
```yaml
# Sistema de Clãs
clans:
  max-tag-length: 5
  max-name-length: 20
  min-players: 1
  protection-new-clan-days: 0

  level-requirements:
    1:
      exp: 0
      max-villages: 1
      logistics-bonus: 1.0
    2:
      exp: 1000
      max-villages: 2
      logistics-bonus: 1.1
    3:
      exp: 3000
      max-villages: 3
      logistics-bonus: 1.2
    4:
      exp: 7000
      max-villages: 4
      logistics-bonus: 1.3
    5:
      exp: 15000
      max-villages: 5
      logistics-bonus: 1.5

# Sistema de Vilas
villages:
  min-distance-between: 500
  max-name-length: 20
  base-production: 10
  vulnerability-window: "20:00-22:00"

  level-requirements:
    1:
      storage: 10000
      features: []
    2:
      storage: 25000
      features: ["dungeon_portal"]
    3:
      storage: 50000
      features: ["dungeon_portal", "port", "walls"]

  dungeon:
    entry-cost: "5 gold_ingot"
    cooldown-minutes: 5
    time-limit-minutes: 30
    max-players: 6

# Sistema de Guerra
wars:
  declaration-cooldown-hours: 24
  preparation-minutes: 5
  duration-minutes: 30
  objectives-to-win: 3

  rewards:
    attacker-win: "village_ownership"
    defender-win: "500 exp, protection_7_days"
    draw: "200 exp"

# Sistema de Economia
economy:
  daily-upkeep-enabled: true
  base-upkeep-cost: 100.0
  village-upkeep-multiplier: 50.0
  level-upkeep-multiplier: 25.0

  resource-values:
    iron: 0.5
    gold: 2.0
    rare: 50.0

  taxes:
    normal: 0.10  # 10%
    allied: 0.05  # 5%
    enemy: 0.25   # 25%

# Sistema de Logística
logistics:
  transport:
    land-speed: 0.4
    sea-speed: 0.6
    road-bonus-per-level: 0.1

  roads:
    blocks:
      - "STONE_BRICKS"
      - "OAK_PLANKS" 
      - "COBBLESTONE"
      - "STONE_SLAB"
    mob-spawn-reduction: 0.15

# Mensagens
messages:
  clan-created: "§aClã %tag% criado com sucesso!"
  village-created: "§aVila %name% criada com sucesso!"
  war-declared: "§cGuerra declarada contra %village%!"
  dungeon-entered: "§eEntrando na dungeon %name%!"
  transport-created: "§aTransporte criado! Leve os recursos com cuidado."

  errors:
    clan-tag-exists: "§cEsta tag já está em uso!"
    not-in-clan: "§cVocê não está em um clã!"
    not-leader: "§cApenas o líder pode fazer isso!"
    insufficient-resources: "§cRecursos insuficientes!"
```

### **quests.yml**
```yaml
# Configuração de Quests
quests:
  new_clan_requirements:
    enabled: true
    requirements:
      - type: "PLAY_TIME"
        description: "Jogar por 10 minutos"
        value: 600
      - type: "COLLECT_RESOURCES"
        description: "Coletar 64 Ferro"
        item: "IRON_INGOT"
        amount: 64
      - type: "KILL_MOBS"
        description: "Matar 10 monstros"
        mob_types: ["ZOMBIE", "SKELETON"]
        amount: 10
    skip_cost:
      enabled: true
      items:
        - type: "GOLD_INGOT"
          amount: 32
```

---

## 🆕 NOVIDADES DA 1.0.6

### ✨ **Novas Funcionalidades**
| Funcionalidade | Descrição |
|----------------|-----------|
| **Sistema de Grupos (Party)** | `/grupo criar`, convidar, entrar juntos na dungeon |
| **Portal Funcional** | Clique no bloco roxo (CRYING_OBSIDIAN) para entrar |
| **Limite de Dungeons** | 2 dungeons simultâneas por vila |
| **Cooldown Individual** | 2 horas após sair da dungeon |
| **Barra de Progresso** | Visual no cooldown |
| **Comandos Admin** | `/clan addxp`, `/clan setlevel`, `/clan setexp` |

### 🔧 **Otimizações**
- Timer de spawners: 1s → 2s (-50% CPU)
- Timer principal: 1s → 3s (-66% CPU)
- Limite de 3 spawns por execução
- Remoção de logs de debug do console

---

## 👑 COMANDOS DE CLÃ

| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/clan criar <tag> <nome>` | Cria um novo clã | `vortexcore.clan.create` |
| `/clan entrar <tag>` | Entra em um clã | `vortexcore.clan.join` |
| `/clan sair` | Sai do clã atual | `vortexcore.clan.join` |
| `/clan info [tag]` | Informações do clã | - |
| `/clan membros` | Lista membros do clã | - |
| `/clan expulsar <jogador>` | Expulsa membro | `vortexcore.clan.manage` |
| `/clan convidar <jogador>` | Convida jogador | `vortexcore.clan.manage` |
| `/clan aliados` | Lista aliados | `vortexcore.clan.alliance` |
| `/clan alianca add <tag>` | Forma aliança | `vortexcore.clan.alliance` |
| `/clan alianca remove <tag>` | Dissolve aliança | `vortexcore.clan.alliance` |
| `/clan upgrade` | Melhora o clã | `vortexcore.clan.upgrade` |
| `/clan disband` | Dissolve o clã | `vortexcore.clan.disband` |
| `/clan city info` | Info da CITY | `vortexcore.clan.city` |
| `/clan city set <vila>` | Define CITY | `vortexcore.clan.city` |
| `/clan territorio` | Info do território | - |
| `/clan chat` | Alterna chat do clã | - |

### **Comandos Admin**
| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/clan addxp <qtd> [tag]` | Adiciona XP ao clã | `vortexcore.admin` |
| `/clan setlevel <nivel> [tag]` | Define nível do clã | `vortexcore.admin` |
| `/clan setexp <xp> [tag]` | Define XP do clã | `vortexcore.admin` |
| `/clan forcesave` | Força salvamento | `vortexcore.admin` |
| `/clan reload` | Recarrega config | `vortexcore.admin` |

---

## 🏘️ COMANDOS DE VILAS

| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/vila criar <nome>` | Cria nova vila | `vortexcore.village.create` |
| `/vila info [nome]` | Info da vila | - |
| `/vila recursos` | Recursos do clã | - |
| `/vila depositar` | Deposita itens | `vortexcore.village.manage` |
| `/vila retirar <ferro> <ouro> <raros>` | Retira recursos | `vortexcore.village.manage` |
| `/vila melhorar` | Melhora vila | `vortexcore.village.manage` |
| `/vila porto` | Constrói porto (lvl 3) | `vortexcore.village.manage` |
| `/vila dungeon` | Lista dungeons | `vortexcore.village.manage` |
| `/vila dungeon confirmar <id>` | Vincula dungeon | `vortexcore.village.manage` |
| `/vila defesa` | Mostra defesas | - |
| `/vila defesa contratar <qtd>` | Contrata guardas | `vortexcore.village.manage` |
| `/vila muros` | Constrói muros (lvl 3) | `vortexcore.village.manage` |
| `/vila vulnerabilidade <inicio> <fim>` | Janela vulnerável | `vortexcore.village.manage` |

---

## 🏛️ COMANDOS DE CIDADE (CITY)

| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/clan city info` | Informações da CITY | - |
| `/clan city set <vila>` | Define uma vila como CITY | Líder |
| `/clan territorio` | Info do território atual | - |

---

## 🌀 COMANDOS DE DUNGEONS

### **Públicos**
| Comando | Descrição |
|---------|-----------|
| `/dungeon list` | Lista dungeons disponíveis |
| `/dungeon info <id>` | Informações da dungeon |
| `/dungeon entrar <id>` | Entra na dungeon (custa 5 ouro) |
| `/dungeon sair` | Sai da dungeon atual |

### **Admin**
| Comando | Descrição |
|---------|-----------|
| `/dungeon admin create <id>` | Cria template |
| `/dungeon admin delete <id>` | Deleta template |
| `/dungeon admin config <id> nome <valor>` | Configura nome |
| `/dungeon admin config <id> tempo <min>` | Tempo limite |
| `/dungeon admin config <id> nivel <n>` | Nível recomendado |
| `/dungeon admin config <id> exp <xp>` | XP de recompensa |
| `/dungeon admin config <id> dif <EASY/MEDIUM/HARD>` | Dificuldade |
| `/dungeon admin schematic <id> <nome>` | Importa schematic |
| `/dungeon admin testschem <nome>` | Testa schematic |
| `/dungeon admin edit <id>` | Modo edição |
| `/dungeon admin save <id>` | Salva configurações |
| `/dungeon admin spawner add <id> <nome> <mob> <count> <delay> <maxMobs>` | Adiciona spawner |
| `/dungeon admin spawner remove <id> <nome>` | Remove spawner |
| `/dungeon admin boss set <id> <mob> <nome> <vida> <dano>` | Configura boss |
| `/dungeon admin boss drop <id> <chance>` | Drop do boss |
| `/dungeon admin mobloot <id> <mob> <chance> <min> <max>` | Loot de mobs |
| `/dungeon admin setspawn <id>` | Spawn dos jogadores |

---

## 👥 COMANDOS DE GRUPOS (PARTY)

| Comando | Descrição |
|---------|-----------|
| `/grupo criar <dungeon>` | Cria um novo grupo (não entra) |
| `/grupo entrar <líder>` | Entra em um grupo existente |
| `/grupo sair` | Sai do grupo atual |
| `/grupo convidar <jogador>` | Convida jogador |
| `/grupo expulsar <jogador>` | Expulsa jogador (líder) |
| `/grupo listar` | Lista grupos ativos |
| `/grupo info` | Informações do grupo |
| `/grupo iniciar` | Inicia a dungeon (leva todos) |

---

## ⚔️ COMANDOS DE GUERRA

| Comando | Descrição |
|---------|-----------|
| `/guerra declarar <vila>` | Declara guerra |
| `/guerra info` | Informações da guerra |
| `/guerra objetivos` | Objetivos da guerra |
| `/guerra rendição` | Rende-se |
| `/guerra rendição confirmar` | Confirma rendição |

---

## 🚚 COMANDOS DE LOGÍSTICA

| Comando | Descrição |
|---------|-----------|
| `/transporte criar <origem> <destino> terra` | Transporte terrestre |
| `/transporte criar <origem> <destino> mar` | Transporte marítimo |
| `/transporte atacar` | Modo ataque (30s) |

---

## 📜 COMANDOS DE QUESTS

| Comando | Descrição |
|---------|-----------|
| `/quest progress` | Progresso das quests |
| `/quest skip` | Pular quests (custa 32 ouro) |
| `/quest skip confirm` | Confirma skip |

---

## 👤 COMANDOS DE CHAT

| Comando | Descrição |
|---------|-----------|
| `/chat` | Alterna chat do clã |
| `/chat <mensagem>` | Envia mensagem no chat do clã |
| `!mensagem` | Envia para o clã (qualquer lugar) |

---

## 🎯 PLACEHOLDERS

| Placeholder | Descrição |
|-------------|-----------|
| `%vortex_clan_tag%` | Tag do clã |
| `%vortex_clan_name%` | Nome do clã |
| `%vortex_clan_level%` | Nível do clã |
| `%vortex_clan_exp%` | Experiência atual |
| `%vortex_clan_next_exp%` | Exp para próximo nível |
| `%vortex_clan_exp_progress%` | Progresso em % |
| `%vortex_clan_members%` | Número de membros |
| `%vortex_clan_max_members%` | Máximo de membros |
| `%vortex_clan_members_display%` | Membros atuais/máx |
| `%vortex_clan_villages%` | Vilas do clã |
| `%vortex_clan_max_villages%` | Máximo de vilas |
| `%vortex_clan_villages_display%` | Vilas atuais/máx |
| `%vortex_clan_bonus%` | Bônus logística |
| `%vortex_clan_upkeep%` | Custo de manutenção |
| `%vortex_clan_days%` | Dias desde criação |
| `%vortex_city_name%` | Nome da CITY |
| `%vortex_city_totems%` | Totens ativos/total |
| `%vortex_city_villages%` | Vilas da CITY |
| `%vortex_city_max_villages%` | Máx. vilas da CITY |
| `%vortex_city_villages_display%` | Vilas atuais/máx |
| `%vortex_village_name%` | Nome da vila atual |
| `%vortex_village_level%` | Nível da vila atual |
| `%vortex_village_resources%` | Recursos da vila atual |
| `%vortex_dungeon_status%` | Em dungeon? |
| `%vortex_dungeon_name%` | Nome da dungeon |
| `%vortex_dungeon_time%` | Tempo decorrido |
| `%vortex_dungeon_time_remaining%` | Tempo restante |
| `%vortex_dungeon_progress%` | Progresso em % |
| `%vortex_dungeon_kills%` | Kills do jogador |
| `%vortex_dungeon_boss%` | Status do boss |
| `%vortex_resources_iron%` | Total de ferro |
| `%vortex_resources_gold%` | Total de ouro |
| `%vortex_resources_rare%` | Total de raros |
| `%vortex_resources_display%` | Display formatado |
| `%vortex_war_status%` | Status da guerra |
| `%vortex_war_objectives%` | Objetivos da guerra |
| `%vortex_war_time%` | Tempo restante da guerra |

---

## 🔧 PERMISSÕES

| Permissão | Descrição | Default |
|-----------|-----------|---------|
| `vortexcore.admin` | Acesso total | OP |
| `vortexcore.clan.create` | Criar clã | true |
| `vortexcore.clan.disband` | Dissolver clã | OP |
| `vortexcore.clan.manage` | Gerenciar membros | OP |
| `vortexcore.clan.alliance` | Gerenciar alianças | OP |
| `vortexcore.clan.upgrade` | Melhorar clã | OP |
| `vortexcore.clan.city` | Gerenciar CITY | OP |
| `vortexcore.village.create` | Criar vila | true |
| `vortexcore.village.manage` | Gerenciar vilas | OP |
| `vortexcore.war.declare` | Declarar guerra | true |
| `vortexcore.dungeon.enter` | Entrar em dungeons | true |
| `vortexcore.dungeon.admin` | Admin de dungeons | OP |
| `vortexcore.logistics.transport` | Criar transporte | true |
| `vortexcore.logistics.attack` | Atacar transporte | true |

---

## ❓ FAQ

### **O plugin é gratuito?**
Sim! VortexCore é completamente gratuito e open-source.

### **Precisa de Vault?**
Sim, o Vault é obrigatório para o funcionamento da economia.

### **Os dados são salvos?**
Sim, tudo é persistido em um banco de dados SQLite (`vortex.db`).

### **O que acontece com os portais após reiniciar?**
O plugin recria automaticamente os metadados dos portais ao iniciar.

### **Qual o limite de jogadores por dungeon?**
6 jogadores por dungeon, e no máximo 2 dungeons simultâneas por vila.

### **Tem cooldown para entrar na dungeon?**
Sim, 2 horas após sair da dungeon (cooldown individual).

---



**Desenvolvido com ❤️ por [Codex_Melo](https://github.com/CodexMelo) e [yggdrasil_Melo](https://github.com/yggdrasilMelo)** 🎮🚀

## 📝 LICENÇA

**All Rights Reserved** - Todos os direitos reservados.

Copyright (c) 2025 Codex_Melo & yggdrasil_Melo

✅ **Permitido:**
- Uso em servidores
- Distribuição gratuita

❌ **Proibido:**
- Venda do plugin
- Uso comercial sem autorização
- Remoção dos créditos

---

## 👥 AUTORES

- **Codex_Melo** - Desenvolvedor principal
- **yggdrasil_Melo** - Desenvolvedor principal

---

## 📢 SUPORTE

- **GitHub:** [https://github.com/CodexMelo/VortexCore](https://github.com/CodexMelo/VortexCore)
- **Issues:** [https://github.com/CodexMelo/VortexCore/issues](https://github.com/CodexMelo/VortexCore/issues)

---

**VortexCore v1.0.5-ALFA - 2026** 🚀
```
