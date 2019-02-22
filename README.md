
    phive install --copy
    composer install
    find src/ -name=*.php | xargs php -l
    phploc --count-tests --log-csv build/logs/phploc.csv --log-xml build/logs/phploc.xml src/ test/
    pdepend --jdepend-xml=build/logs/jdepend.xml --jdepend-chart=build/pdepend/dependencies.svg --overview-pyramid=build/pdepend/overview-pyramid.svg src/
    phpmd src/ xml build/phpmd.xml --reportfile build/logs/pmd.xml
    phpcs --report=checkstyle --standard=phpcs.xml --report-file=build/logs/checkstyle.xml --extensions=php src/
    phpcpd --log-pmd build/logs/pmd-cpd.xml --names-exclude *Test.php src/

    phpdbg -qrr tools/phpunit -c phpunit.xml
    phpdox