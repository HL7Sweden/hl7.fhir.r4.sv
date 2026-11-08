# REVERSE_ENGINEERING_REPORT — hl7.fhir.r4.sv

## A. Diagnóstico geral

### Arquitetura identificada
Implementation Guide (IG) FHIR baseado em SUSHI para pacote de idioma sueco (HL7 Sweden / hl7.fhir.r4.sv). Estrutura:

- `input/hl7.fhir.r4.sv.xml`: definição do IG (id, canonical, version, fhirVersion, páginas, parâmetros)
- `input/translations/*.po`: 16 arquivos de tradução gettext para CodeSystems
- `input/pagecontent/`: páginas do IG (index.md, translation-principles.md, etc.)
- `input/resources/`: apenas `place-holder.txt` (nenhum recurso real)
- `ig.ini`: configuração do IG publisher
- `.github/workflows/validate-docs.yml`: CI para validar com Sushi e IG Publisher

### Tecnologias e dependências
- SUSHI / fsh-sushi
- FHIR R4 (fhirVersion: 4.0.1)
- IG Publisher (Jekyll-based)
- Nenhum recurso FHIR real (apenas place-holder.txt)

### Estado de manutenção
Branch default: main. Repositório: https://github.com/HL7Sweden/hl7.fhir.r4.sv. Versão 0.1.0.

### Mecanismos de testes existentes
Nenhum teste automatizado encontrado. CI workflow existe (validate-docs.yml) mas não testa conteúdo FHIR.

### Limitações da investigação
- SUSHI não instalado; build do IG não executado.
- REA 6.7.0 não operacional; análise estática apenas.

## B. Problemas encontrados

| ID | Título | Severidade | Status | Localização |
|----|--------|------------|--------|-------------|
| REA-sv-001 | `hl7.fhir.r4.sv.xml` usa `releaselabel` (minúsculo) | P3 | CONFIRMADO | `hl7.fhir.r4.sv.xml:46` |
| REA-sv-002 | Arquivo `translation-princples.md` (erro de ortografia) duplicado | P3 | CONFIRMADO | `input/pagecontent/translation-princples.md` |
| REA-sv-003 | `input/resources/` contém apenas `place-holder.txt` | P3 | CONFIRMADO | `input/resources/` |

### Detalhes dos problemas confirmados

**REA-sv-001 (P3, CONFIRMADO)**: O XML do IG usa o parâmetro `releaselabel` (tudo minúsculo) na linha 46. Embora algumas versões do SUSHI aceitem essa grafia, a forma canônica é `releaseLabel` (camelCase). Isso pode causar problemas de compatibilidade com versões mais rígidas do SUSHI.

Evidência: `hl7.fhir.r4.sv.xml:46` — `<parameter><code value="releaselabel"/><value value="Working Copy"/>