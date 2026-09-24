# Rio 2026 — configuração do Firebase

1. No Firebase Console, ative Authentication > Sign-in method > Email/Password.
2. Crie o Cloud Firestore.
3. Nas regras do Firestore, restrinja cada documento ao usuário autenticado:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tripSync/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

4. No Web App do Firebase, use apenas apiKey, authDomain, projectId e appId públicos no aplicativo.
5. No Rio 2026, abra “Configurar conexão gratuita”, preencha esses quatro campos e salve.
6. Use a mesma conta de e-mail/senha nos dois celulares.

## Recuperação de senha

Na tela de sincronização existe o botão “Esqueci minha senha”. Ele usa o recurso oficial `sendPasswordResetEmail` do Firebase Authentication para enviar o link de redefinição ao e-mail da conta.
