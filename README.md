# 🚀Symfony UX Live Component : Créez un système de recherche pour les utilisateurs sans JavaScript

Ce guide vous montre comment utiliser **Symfony UX** Live Component pour créer un système de recherche en temps réel des utilisateurs 🔍 sans écrire une seule ligne de JavaScript 🚫💻.

## Qu'est-ce que Symfony UX Live Component ? 🧩

**Symfony UX Live Component** est une solution ultra pratique permettant de créer des **interfaces réactives** et **dynamiques** sans écrire une seule ligne de **JavaScript** 🖥️. Inspiré par **Livewire** (pour **Laravel**) et **Phoenix LiveView** ⚡, **Symfony UX Live Component** permet d’interagir en **temps réel** ⏱️ avec vos utilisateurs, tout en restant sur du code **PHP** 🐘 et **Twig** 🧶.

Avec cette approche, plus besoin d’**AJAX** 🚀 ! Tout se passe côté **serveur**, ce qui simplifie le développement et la gestion des **composants interactifs**. **Symfony UX Live Component** est parfait pour les développeurs souhaitant créer des **interfaces dynamiques** sans se plonger dans des technologies front-end complexes.


## Installez Symfony UX Live Component 🛠️

Avant de pouvoir utiliser **Symfony UX Live Component** dans votre projet, voici les étapes à suivre pour l'installer :

**Installez le composant via Composer** 📦 :

```bash
composer require symfony/ux-live-component
```
**Si vous utilisez Webpack Encore**⚙️ :

```bash
npm install --force
npm run watch
```
Et voilà 🎉, **Symfony UX** Live Component est prêt à être utilisé pour rendre vos interfaces interactives en temps réel !

## Testez Symfony UX Live Component avec Docker ! 🐳
Si vous avez déjà un projet Symfony ou souhaitez en créer un nouveau pour tester **Symfony UX Live Component** 💡, **Docker** est votre meilleur ami 🤝 !
Il permet de configurer rapidement un environnement complet (**PHP** 🐘, **MySQL** 🐬, **Symfony** 🌐, etc.) sans vous soucier des détails techniques de votre machine locale.

Envie d’intégrer un Live Component dans un projet existant ? 
🎯 Vous pouvez le faire sans une seule ligne de **JavaScript** ! 
Il suffit de l’ajouter dans votre projet et de commencer à l’utiliser, comme illustré plus bas.

Si vous préférez créer un nouveau projet pour tester **Symfony UX Live Component**, **suivez mon guide Docker 🐳 sur GitHub !**
Mon dépôt fournit toutes les étapes nécessaires pour configurer un projet Symfony avec Live Component en quelques minutes ⏱️.

👉 [Mon Repository GitHub](https://github.com/abdelhakmireda/Environnement-D-veloppement-Docker-Symfony) 📦.

## Utilisation de Symfony UX Live Component : Recherche en temps réel 🔍

J'ai utilisé **Symfony UX** Live Component pour créer un système de recherche en temps réel des utilisateurs 👥. 
Grâce à cette fonctionnalité, vous pouvez rechercher un utilisateur et afficher les résultats **instantanément** 🕒, sans recharger la page 🌐.

### 📜 Composant PHP :

```bash
// src/Components/UserSearchComponent.php
namespace App\Twig\Components;

use App\Repository\UserRepository;
use Symfony\UX\LiveComponent\Attribute\AsLiveComponent;
use Symfony\UX\LiveComponent\Attribute\LiveProp;
use Symfony\UX\LiveComponent\DefaultActionTrait;

#[AsLiveComponent]
class UserSearch
{
    use DefaultActionTrait;

    #[LiveProp(writable: true)]
    public string $query = '';

    public function __construct(private UserRepository $userRepository) {}

    public function getResults(): array
    {
        return empty($this->query) 
            ? $this->userRepository->findAll()
            : $this->userRepository->findByQuery($this->query);
    }
}
```

### 🔍 Requête dans le repository avec des champs personnalisés :

```bash
// src/Repository/UserRepository.php
public function findByQuery(string $query): array
{
    return $this->createQueryBuilder('u')
        ->where('u.premier_champ LIKE :query OR u.deuxieme_champ LIKE :query')
        ->setParameter('query', '%' . $query . '%')
        ->getQuery()
        ->getResult();
}
```

### 🌐 Vue Twig :

```bash
{# templates/components/UserSearch.html.twig #}
<div {{ attributes }}>
    <div class="search-input">
        {{ ux_icon('tabler:search') }}
        <input type="search" data-model="query" placeholder="Rechercher...">
    </div>
    <table id="results-table">
        <thead>
            <tr>
                <th>Premier Champ</th>
                <th>Deuxième Champ</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            {% for result in this.getResults() %}
                <tr>
                    <td>{{ result.premierChamp }}</td>
                    <td>{{ result.deuxiemeChamp }}</td>
                    <td>
                        <a href="{{ path('edit_result', {'id': result.id}) }}">Modifier</a>
                    </td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
</div>
```

## Conclusion 🎯

En résumé, **Symfony UX Live Component** vous permet de créer des applications réactives sans complexité supplémentaire. 
Que vous ayez un projet Symfony déjà existant ou que vous souhaitiez expérimenter avec ses fonctionnalités via Docker 🐳, vous pouvez facilement mettre en place un système de recherche en temps réel sans écrire une seule ligne de JavaScript 💻.

Utiliser Docker simplifie également la configuration de votre environnement et vous permet de démarrer rapidement. 
N’hésitez pas à suivre mon guide sur GitHub pour vous lancer dans cette nouvelle aventure !

👉[Mon Repository GitHub](https://github.com/abdelhakmireda/Environnement-D-veloppement-Docker-Symfony) 📦.

