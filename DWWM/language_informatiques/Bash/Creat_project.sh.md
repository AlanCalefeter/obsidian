# Demander le chemin
pwd
read -p "Entrez le chemin du dossier : " chemin

# Si le dossier existe, on s'y place
if [ -d "$chemin" ]; then
    cd "$chemin"
    echo "Chemin trouvé, positionné sur : $chemin"
else
    echo "Ce chemin n'existe pas."

    # Dossier par défaut
    cd /c/Users/29010-34-08/Desktop/LiberKey/MyApps/laragon/www 
    echo "Positionné sur le dossier imposé : /c/Users/29010-34-08/Desktop/LiberKey/MyApps/laragon/www "
fi
read -p "nom du projet : " structure

mkdir $structure && cd $structure && mkdir .well-known  assets img pages scss docs .editorconfig &&
touch LICENSE .browserslistrc 403.html 404.html README.md favicon.png index.html robots.txt sitemap.xml &&

mkdir assets/css/ assets/js/ assets/fonts img/icons scss/abstracts scss/base scss/components/ scss/layouts/ scss/pages scss/utilities docs/architecture/ docs/diagrams/ docs/security/ &&

touch .well-known/security.txt assets/css/style.css assets/css/style.css.map pages/about.html pages/article-details.html pages/blog.html pages/contact.html pages/cookies-policy.html pages/faq.html pages/legal-notice.html pages/portfolio.html pages/privacy-policy.html pages/project-details.html pages/search-results.html pages/service-details.html pages/services.html pages/team.html pages/terms-conditions.html pages/testimonials.html &&

touch assets/css/style.css assets/css/style.css.map assets/fonts/NotoSans-VariableFont.woff2 assets/fonts/OFL.txt assets/fonts/README.txt assets/js/app.js scss/abstracts/_functions.scss scss/style.scss scss/abstracts/_index.scss scss/abstracts/_mixins.scss scss/abstracts/_variables.scss scss/base/_fonts.scss scss/base/_global.scss scss/base/_index.scss scss/base/_reset.scss scss/base/_root.scss scss/base/_typography.scss scss/components/_buttons.scss scss/components/_card.scss scss/components/_icons.scss scss/components/_index.scss scss/layouts/_container.scss scss/layouts/_footer.scss scss/layouts/_header.scss scss/layouts/_index.scss scss/pages/_about.scss scss/pages/_home.scss scss/pages/_index.scss scss/utilities/_accessibility.scss scss/utilities/_alignment.scss scss/utilities/_display.scss scss/utilities/_flexbox.scss scss/utilities/_grid.scss scss/utilities/_index.scss scss/utilities/_spacing.scss scss/utilities/_visibility.scss docs/architecture/overview.md docs/workflow.md docs/README.md