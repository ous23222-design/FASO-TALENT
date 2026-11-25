# Faso Talent — kit de démarrage

Application web progressive (PWA) de démonstration : accueil, studio, import d'instrumentales, deux pistes vocales, effets de pré-écoute, brouillons locaux, capture vidéo, profil et interface de demande de paiement Wave.

## Ce qui fonctionne dans cette version
- Interface responsive téléphone / ordinateur.
- Import d'une instrumentale audio depuis l'appareil et lecture.
- Enregistrement micro de la voix principale et d'une deuxième piste (permission microphone requise).
- Préréglages de pré-écoute, réverbération, écho, présence et contrôle de volume.
- Sauvegarde de médias dans IndexedDB et liste de brouillons locale.
- Import ou capture vidéo (HTTPS requis pour la caméra).
- Ajout local d'instrumentales gratuites ou premium.
- QR Wave intégré et formulaire de demande de validation manuelle.
- PWA avec cache hors ligne des fichiers de l'application.

## Limites à connaître — ne pas présenter comme plateforme de production
Cette archive est un front-end local de départ, pas un service musical public complet. Les profils, brouillons, instrumentales et demandes Wave sont enregistrés sur l'appareil et ne sont pas partagés entre utilisateurs. L'interface admin locale n'est pas protégée et ses validations ne donnent aucun droit réel. La publication publique, les vrais comptes, les likes, commentaires, abonnements, messagerie, stockage cloud et contrôle de paiement ne sont pas encore connectés.

Les presets Hard Tune et autres sont des réglages de pré-écoute simplifiés. Il ne s'agit pas d'un véritable algorithme Auto-Tune / correction de hauteur professionnelle. Le mix export expérimental peut dépendre du navigateur et ne garantit pas une qualité studio. Les prises peuvent être téléchargées séparément.

## Tester sur Android
1. Décompresser l'archive.
2. Créer un dépôt GitHub `faso-talent`.
3. Envoyer le CONTENU du dossier `faso-talent-complet` à la racine du dépôt en conservant les dossiers `css`, `js`, `assets`, `supabase`.
4. Dans GitHub : Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save.
5. Attendre le déploiement. Ouvrir l'URL HTTPS GitHub Pages sur Android.
6. Autoriser le microphone et la caméra. Installer via le menu du navigateur → Ajouter à l'écran d'accueil.

## Pour une vraie plateforme multi-utilisateur
1. Créer un projet Supabase.
2. Exécuter `supabase/schema.sql` dans SQL Editor.
3. Créer les buckets Storage `audio`, `videos`, `covers` avec des règles d'accès strictes. Les brouillons doivent rester privés ; seules les chansons explicitement publiques sont lisibles publiquement.
4. Ajouter une authentification Supabase et connecter le front-end avec l'URL et la clé `anon` publique. Ne jamais mettre la clé `service_role` dans le navigateur ni dans GitHub.
5. Créer une Edge Function réservée aux admins pour approuver un paiement après vérification dans Wave, puis activer l'abonnement 30 jours ou débloquer l'instrumentale concernée. Le client ne doit jamais pouvoir s'accorder lui-même le premium.
6. Ajouter des règles de modération, signalement, suppression, limites de taille, sauvegardes et conditions d'utilisation avant l'ouverture publique.

## Paiements Wave
Le QR fourni est dans `assets/payments/wave-qr.png`. Le formulaire demande une référence de transaction. L'archive n'interroge pas Wave et ne peut pas confirmer un transfert automatiquement. Le titulaire doit contrôler le paiement dans Wave avant de valider via un back-office sécurisé. Ne demande jamais le code PIN Wave, mot de passe ou OTP d'un utilisateur.

## Audio et vidéo
Le navigateur demande l'autorisation du micro/caméra. Ces fonctions requièrent HTTPS (GitHub Pages convient). La compatibilité MediaRecorder varie selon les téléphones. Le vrai pitch correction, les effets avancés en temps réel et un export multipiste fiable nécessitent un moteur audio spécialisé et des tests sur appareils réels.
