# AI Agent - GitHub Pages Publisher (Versione Sicura)

Questo progetto permette all'AI Agent di pubblicare automaticamente contenuti su GitHub Pages in modo sicuro.

## ⚠️ Sicurezza dei Token

**IMPORTANTE:** GitHub ha una funzione di "Push Protection" che blocca automaticamente i push contenenti segreti hardcoded nei file. Questo script implementa le best practices di sicurezza:

- **Il token viene usato SOLO come variabile d'ambiente**
- **Mai hardcodare token nei file di configurazione**
- **Il token non viene mai committato nel repository**

## Configurazione

### 1. Genera un Personal Access Token (PAT) su GitHub

Vai su GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)

Clicca su "Generate new token (classic)" e seleziona:
- **repo** - Full control of private repositories
- **workflow** - Update GitHub Action workflows

### 2. Configura il Token

Esporta il token come variabile d'ambiente **PRIMA** di eseguire lo script:

```bash
export GITHUB_TOKEN='ghp_il_tuo_token_qui'
```

Il token non sarà salvato in nessun file!

### 3. Esegui il Publisher

```bash
chmod +x deploy.sh
./deploy.sh
```

## Come Funziona

1. **Verifica Sicurezza:** Lo script controlla che il token sia impostato come variabile d'ambiente
2. **Configura Git:** Imposta l'identità Git e aggiorna l'URL remote con credenziali temporanee
3. **Genera Contenuto:** Crea il file index.html con il messaggio "Ciao Mondo"
4. **Deploy:** Esegue commit e push al repository

## Struttura del Progetto

```
agent-github-publisher-v2/
├── deploy.sh          # Script principale di pubblicazione
├── index.html         # Pagina generata automaticamente
├── README.md          # Questo file
└── .git/              # Repository Git inizializzato
```

## Dopo l'Uso

Per sicurezza, cancella la variabile d'ambiente dopo l'uso:

```bash
unset GITHUB_TOKEN
```

## Risoluzione Problemi

### Errore: "Token not found"
Assicurati di aver esportato il token:
```bash
export GITHUB_TOKEN='ghp_xxx'
echo $GITHUB_TOKEN  # Verifica che sia visibile
```

### Errore: "Push cannot contain secrets"
Il token è stato trovato in un file. Non hardcodare MAI i token.

### Errore: "Resource not accessible by personal access token"
Il token non ha i permessi necessari. Assicurati di aver selezionato lo scope "repo".

### Errore: "Repository not found"
Verifica che il repository esista e che l'utente abbia accesso:
- Repository: `katelkum/ai-agent-site`
- URL: https://github.com/katelkum/ai-agent-site

## Best Practices di Sicurezza

1. **Mai hardcodare segreti** nei file di codice
2. **Usare variabili d'ambiente** per i token
3. **Rotare regolarmente** i token (cambiali periodicamente)
4. **Usare lo scope minimo necessario** per il token
5. **Cancellare i token non usati** da GitHub

## Riferimenti

- [Documentazione GitHub sui token](https://docs.github.com/en/authentication/keeping-your-account-and-secure/managing-your-personal-access-tokens)
- [Push Protection](https://docs.github.com/en/code-security/concepts/secret-security/about-push-protection)
- [Best practices per i segreti](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions)

## Licenza

MIT License - Progetto educativo per AI Agent
