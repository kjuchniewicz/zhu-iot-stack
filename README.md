# Mosquitto

Polecenia poniżej uruchamiany w kontenerze.

```bash
# Utworzy nowy plik z hasłami, doda użytkownika i zapyta o hasło
mosquitto_passwd -c /mosquitto/config/pwfile user1
# Doda użytkownika i zapyta o hasło
mosquitto_passwd /mosquitto/config/pwfile user2
# Usuwanie użytkownika
mosquitto_passwd -D /mosquitto/config/pwfile <user-name-to-delete>
```

# Node Red

Poleceniem w kontenerze tworzy za hashowane hasło

```bash
nodered npx node-red <user-name> hash-pw
# Np. HASH = $7$101$R2B7lTnhbxRDKZxb$GZBSsqwt/4ZD6vJl9eZ6c+p9qfFpTYnAuPY8wXa4HEQi06sFfih9AYfd3JvYjhpAa6xAbDn22NYctpYk+ojfaw==
```

Nastepnie w pliku nodered\config\settings.js znajdujemy poniższy kod od komentujemy. Potem podmieniamy użytkownika na tego użytego w poleceniu powyżej, a hasło wynikowym hashem.

```javascript
adminAuth: {
        type: "credentials",
        users: [{
            username: "<user-name>",
            password: "HASH",
            permissions: "*"
        }]
    },
```

Restartujemy kontener
