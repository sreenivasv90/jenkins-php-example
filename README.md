
    phive install --copy
    composer install
    find src/ -name "*.php" | xargs php -l
    /usr/bin/php7.3 tools/phploc --count-tests --log-csv build/logs/phploc.csv --log-xml build/logs/phploc.xml src/ test/
    /usr/bin/php7.3 vendor/bin/pdepend --jdepend-xml=build/logs/jdepend.xml --jdepend-chart=build/pdepend/dependencies.svg --overview-pyramid=build/pdepend/overview-pyramid.svg src/
    /usr/bin/php7.3 vendor/bin/phpmd src/ xml phpmd.xml --reportfile build/logs/pmd.xml
    /usr/bin/php7.3 tools/phpcs --report=checkstyle --standard=phpcs.xml --report-file=build/logs/checkstyle.xml --extensions=php src/
    /usr/bin/php7.3 tools/phpcpd --log-pmd build/logs/pmd-cpd.xml --names-exclude "*Test.php" src/
    phpdbg -qrr tools/phpunit -c phpunit.xml
    tools/phpdox -f phpdox.xml