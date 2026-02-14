
# 📚 **VORTEXCORE - DOCUMENTAÇÃO COMPLETA 

```markdown
# 🌀 VORTEXCORE

![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)
![Paper](https://img.shields.io/badge/Paper-1.21.11-blue)
![Java](https://img.shields.io/badge/Java-21-orange)

**Sistema completo de Clãs, Vilas, Dungeons e Guerras para Minecraft Paper 1.21.11**

---

## 📋 ÍNDICE
- [📥 Instalação](#-instalação)
- [⚙️ Configuração](#️-configuração)
- [👑 Comandos de Clã](#-comandos-de-clã)
- [🏘️ Comandos de Vilas](#️-comandos-de-vilas)
- [🌀 Comandos de Dungeons](#-comandos-de-dungeons)
- [⚔️ Comandos de Guerra](#️-comandos-de-guerra)
- [🚚 Comandos de Logística](#-comandos-de-logística)
- [📜 Comandos de Quests](#-comandos-de-quests)
- [👤 Comandos de Chat](#-comandos-de-chat)
- [🎯 Placeholders](#-placeholders)
- [🔧 Permissões](#-permissões)
- [❓ FAQ](#-faq)

---

## 📥 INSTALAÇÃO

### **Requisitos:**
- Servidor **Paper 1.21.11** ou superior
- **Java 21** ou superior
- **Vault** (para economia)
- **PlaceholderAPI** (opcional, para placeholders)
- **WorldEdit** (opcional, para schematics de dungeons)

### **Passo a passo:**
1. Baixe o arquivo `VortexCore-1.0.0.jar`
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
    max-players: 5

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

## 👑 COMANDOS DE CLÃ

### **Comandos Públicos**
| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/clan criar <tag> <nome>` | Cria um novo clã | `vortexcore.clan.create` |
| `/clan entrar <tag>` | Entra em um clã (precisa de convite) | `vortexcore.clan.join` |
| `/clan sair` | Sai do clã atual | `vortexcore.clan.join` |
| `/clan info [tag]` | Informações do clã | - |
| `/clan membros` | Lista membros do clã | - |
| `/clan chat` | Alterna chat do clã | - |

### **Comandos de Líder/Co-líder**
| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/clan expulsar <jogador>` | Expulsa membro do clã | `vortexcore.clan.manage` |
| `/clan convidar <jogador>` | Convida jogador para o clã | `vortexcore.clan.manage` |
| `/clan aliados` | Lista aliados do clã | `vortexcore.clan.alliance` |
| `/clan alianca add <tag>` | Forma aliança com outro clã | `vortexcore.clan.alliance` |
| `/clan alianca remove <tag>` | Dissolve aliança | `vortexcore.clan.alliance` |
| `/clan upgrade` | Melhora o nível do clã | `vortexcore.clan.upgrade` |
| `/clan disband` | Dissolve o clã | `vortexcore.clan.disband` |

### **Comandos de CITY**
| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/clan city info` | Informações da CITY do clã | `vortexcore.clan.city` |
| `/clan city set <vila>` | Define uma vila como CITY | `vortexcore.clan.city` |

### **Exemplos:**
```bash
# Criar um clã
/clan criar TEST "Clã Teste"

# Convidar jogador
/clan convidar Steve

# Ver informações
/clan info TEST

# Formar aliança
/clan alianca add ALLY

# Definir CITY
/clan city set capital
```

---

## 🏘️ COMANDOS DE VILAS

### **Comandos Públicos**
| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/vila criar <nome>` | Cria uma nova vila | `vortexcore.village.create` |
| `/vila info [nome]` | Informações da vila | - |
| `/vila recursos` | Recursos totais do clã | - |
| `/vila depositar` | Deposita itens na vila | `vortexcore.village.manage` |
| `/vila retirar <ferro> <ouro> <raros>` | Retira recursos da vila | `vortexcore.village.manage` |

### **Comandos de Upgrade**
| Comando | Descrição | Requisito |
|---------|-----------|-----------|
| `/vila melhorar` | Melhora o nível da vila | Nível 1+ |
| `/vila porto` | Constrói um porto (marítimo) | Nível 3 |
| `/vila dungeon` | Constrói portal de dungeon | Nível 2 |
| `/vila defesa` | Gerencia guardas da vila | Nível 2+ |
| `/vila muros` | Constrói muros defensivos | Nível 3 |

### **Comandos de Vulnerabilidade**
| Comando | Descrição | Exemplo |
|---------|-----------|---------|
| `/vila vulnerabilidade <inicio> <fim>` | Define janela vulnerável | `/vila vulnerabilidade 20:00 22:00` |
| `/vila vulnerabilidade <inicio> <horas>` | Define por duração | `/vila vulnerabilidade 20:00 4` |

### **Exemplos:**
```bash
# Criar vila (deve estar a 500+ blocos de outras)
/vila criar capital

# Depositar recursos (segure o item na mão)
/vila depositar

# Retirar recursos
/vila retirar 64 32 0

# Melhorar vila
/vila melhorar

# Definir vulnerabilidade
/vila vulnerabilidade 20:00 22:00
```

---

## 🌀 COMANDOS DE DUNGEONS

### **Comandos Públicos**
| Comando | Descrição | Custo |
|---------|-----------|-------|
| `/dungeon list` | Lista dungeons disponíveis | Grátis |
| `/dungeon info <id>` | Informações da dungeon | Grátis |
| `/dungeon entrar <id>` | Entra na dungeon | 5 barras de ouro |
| `/dungeon sair` | Sai da dungeon atual | Grátis |

### **Comandos Admin (Criação de Dungeons)**
| Comando | Descrição |
|---------|-----------|
| `/dungeon admin create <id>` | Cria novo template |
| `/dungeon admin delete <id>` | Deleta template |
| `/dungeon admin config <id> nome <valor>` | Define o nome |
| `/dungeon admin config <id> tempo <min>` | Tempo limite |
| `/dungeon admin config <id> nivel <n>` | Nível recomendado |
| `/dungeon admin config <id> exp <xp>` | XP de recompensa |
| `/dungeon admin config <id> dif <EASY/MEDIUM/HARD>` | Dificuldade |

### **Comandos de Schematics (WorldEdit)**
| Comando | Descrição |
|---------|-----------|
| `/dungeon admin schematic <id> <nome>` | Importa schematic |
| `/dungeon admin testschem <nome>` | Testa schematic |
| `/dungeon admin edit <id>` | Entra no modo edição |
| `/dungeon admin save <id>` | Salva configurações |

### **Comandos de Spawners**
```bash
/dungeon admin spawner add <id> <nome> <mob> <count> <delay> <maxMobs>
/dungeon admin spawner remove <id> <nome>
```
**Exemplo:** `/dungeon admin spawner add teste sala1 ZOMBIE 3 100 5`

### **Comandos de Boss**
```bash
# Configurar boss (olhe para o local)
/dungeon admin boss set <id> <mob> <nome> <vida> <dano>

# Adicionar drop do boss
/dungeon admin boss drop <id> <chance>
```
**Exemplo:** `/dungeon admin boss set teste RAVAGER "&4Balrog" 500 25`

### **Comandos de Loot de Mobs**
```bash
# Configurar loot para mobs (segure o item)
/dungeon admin mobloot <id> <mob> <chance> <min> <max>
```
**Exemplo:** `/dungeon admin mobloot teste ZOMBIE 0.3 1 3`

### **Comandos de Spawn dos Jogadores**
```bash
# Definir onde os jogadores aparecem
/dungeon admin setspawn <id>
```

### **Exemplo Completo - Criando uma Dungeon:**
```bash
# 1. Criar template
/dungeon admin create moria
/dungeon admin config moria nome "&7Minas de Moria"
/dungeon admin config moria tempo 25
/dungeon admin config moria dif HARD

# 2. Importar schematic
/dungeon admin schematic moria dungeon_moria

# 3. Editar e configurar
/dungeon admin edit moria
/dungeon admin spawner add moria sala1 ZOMBIE 3 100 5
/dungeon admin boss set moria RAVAGER "&4Balrog" 500 25
/dungeon admin mobloot moria ZOMBIE 0.3 1 3

# 4. Salvar e testar
/dungeon admin save moria
/dungeon entrar moria
```

---

## ⚔️ COMANDOS DE GUERRA

| Comando | Descrição | Permissão |
|---------|-----------|-----------|
| `/guerra declarar <vila>` | Declara guerra a uma vila | `vortexcore.war.declare` |
| `/guerra info` | Informações da guerra atual | - |
| `/guerra objetivos` | Ver objetivos da guerra | - |
| `/guerra rendição` | Rende-se na guerra atual | `vortexcore.war.surrender` |

### **Fluxo da Guerra:**
1. Declare guerra a uma vila vulnerável
2. Após 5 minutos, 3 totens aparecem
3. Atacantes devem destruir os 3 totens
4. Defensores devem proteger os totens por 30 minutos
5. Se todos totens forem destruídos → Vila conquistada
6. Se a vila for a CITY do clã, o líder vira boss

---

## 🚚 COMANDOS DE LOGÍSTICA

| Comando | Descrição | Requisitos |
|---------|-----------|------------|
| `/transporte criar <origem> <destino> terra` | Cria transporte terrestre | Vilas do mesmo clã |
| `/transporte criar <origem> <destino> mar` | Cria transporte marítimo | Vilas com porto |
| `/transporte atacar` | Ativa modo ataque por 30s | Clã em guerra |
| `/transporte proteger` | Ativa modo escolta | Ser do mesmo clã |

### **Estradas**
Estradas construídas com blocos específicos dão bônus de velocidade:
- `STONE_BRICKS`, `OAK_PLANKS`, `COBBLESTONE`, `STONE_SLAB`
- Cada nível de estrada dá +10% de velocidade

---

## 📜 COMANDOS DE QUESTS

| Comando | Descrição |
|---------|-----------|
| `/quest progress` | Ver progresso das quests |
| `/quest skip` | Pular quests (custa 32 ouro) |
| `/quest skip confirm` | Confirma skip |

### **Requisitos para criar clã (configuráveis):**
- ⏱️ Jogar por X minutos
- ⚒️ Coletar X recursos
- ⚔️ Matar X monstros

---

## 👤 COMANDOS DE CHAT

| Comando | Descrição |
|---------|-----------|
| `/chat` | Alterna chat do clã |
| `/chat <mensagem>` | Envia mensagem diretamente no chat do clã |

**No chat do clã:** Todas as mensagens vão apenas para membros do clã

---

## 🎯 PLACEHOLDERS

### **Placeholders para Clãs**
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

### **Placeholders para CITY**
| Placeholder | Descrição |
|-------------|-----------|
| `%vortex_city_name%` | Nome da CITY |
| `%vortex_city_totems%` | Totens ativos/total |
| `%vortex_city_villages%` | Vilas da CITY |
| `%vortex_city_max_villages%` | Máx. vilas da CITY |
| `%vortex_city_villages_display%` | Vilas atuais/máx |

### **Placeholders para Dungeons**
| Placeholder | Descrição |
|-------------|-----------|
| `%vortex_dungeon_status%` | Em dungeon? |
| `%vortex_dungeon_name%` | Nome da dungeon |
| `%vortex_dungeon_time%` | Tempo decorrido |
| `%vortex_dungeon_time_remaining%` | Tempo restante |
| `%vortex_dungeon_progress%` | Progresso em % |
| `%vortex_dungeon_kills%` | Kills do jogador |
| `%vortex_dungeon_boss%` | Status do boss |

### **Placeholders para Recursos**
| Placeholder | Descrição |
|-------------|-----------|
| `%vortex_resources_iron%` | Total de ferro |
| `%vortex_resources_gold%` | Total de ouro |
| `%vortex_resources_rare%` | Total de raros |
| `%vortex_resources_display%` | Display formatado |

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
| `vortexcore.war.surrender` | Render-se | OP |
| `vortexcore.dungeon.enter` | Entrar em dungeon | true |
| `vortexcore.dungeon.admin` | Admin de dungeons | OP |
| `vortexcore.logistics.transport` | Criar transporte | true |
| `vortexcore.logistics.attack` | Atacar transporte | true |

---

## ❓ FAQ

### **Como criar um clã?**
```bash
1. Complete as quests com /quest progress
2. /clan criar TAG "Nome do Clã"
```

### **Como criar a CITY do clã?**
```bash
1. Crie uma vila
2. /clan city set <nome_da_vila>
```

### **Como criar uma dungeon?**
```bash
1. /dungeon admin create moria
2. /dungeon admin schematic moria dungeon_moria
3. /dungeon admin edit moria
4. Configure spawners e boss
5. /dungeon admin save moria
```

### **Como declarar guerra?**
```bash
1. Espere a vila ficar vulnerável (janela configurada)
2. /guerra declarar <vila>
```

### **Como transportar recursos?**
```bash
/transporte criar <origem> <destino> terra
# Ou por mar (se tiver portos)
/transporte criar <origem> <destino> mar
```

### **Preciso de WorldEdit?**
Só para criar dungeons com schematics. O resto do plugin funciona sem.

---

## 📝 LICENÇA

MIT License - Use, modifique e distribua livremente.

## 👥 CONTRIBUIDORES

- **Codex_Melo** - Desenvolvedor principal
- **yggdrasil_Melo** - Desenvolvedor principal

---

**VortexCore v1.0.0 - 2026** 🚀
```
