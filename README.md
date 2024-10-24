# 🚀Symfony UX Live Component : Créez un système de recherche pour les utilisateurs sans JavaScript

Ce guide vous montre comment utiliser **Symfony UX** Live Component pour créer un système de recherche en temps réel des utilisateurs 🔍 sans écrire une seule ligne de JavaScript 🚫💻.

## Qu'est-ce que Symfony UX Live Component ? 🧩

**Symfony UX Live Component** est une solution pratique pour créer des interfaces réactives sans écrire de **JavaScript** 🖥️. Inspiré de **Livewire et Phoenix LiveView** ⚡, il permet d’interagir en temps réel ⏱️ avec les utilisateurs, en utilisant uniquement PHP 🐘 et Twig 🧶.
Plus besoin d’AJAX 🚀, tout se fait côté serveur, simplifiant ainsi le développement d’interfaces dynamiques sans recourir à des technologies front-end complexes.

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
Que ce soit pour un projet existant ou un nouveau 💡, **Docker** permet de configurer rapidement un environnement complet (**PHP** 🐘, **MySQL** 🐬, **Symfony** 🌐) sans souci technique local.
Intégrez un Live Component sans écrire de JavaScript 🎯, ajoutez-le simplement à votre projet.
Pour un nouveau projet, suivez **mon guide Docker** 🐳 sur GitHub et configurez Symfony avec **Live Component** en quelques minutes ⏱️.

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

**Symfony UX Live Component** permet de créer des applications réactives sans complexité. Que ce soit pour un projet existant ou avec Docker 🐳, vous pouvez facilement mettre en place une recherche en temps réel sans JavaScript 💻.
Docker simplifie la configuration, alors suivez mon guide GitHub et lancez-vous dans cette aventure !

👉[Mon Repository GitHub](https://github.com/abdelhakmireda/Environnement-D-veloppement-Docker-Symfony) 📦.

