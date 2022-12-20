####code from fut branch
    /usr/bin/php7.3 /usr/local/bin/phive install --copy
    /usr/bin/php7.3 tools/composer install
    
    find src/ -name "*.php" | xargs /usr/bin/php7.3  -l
    /usr/bin/php7.3 tools/phploc --count-tests --log-csv build/logs/phploc.csv --log-xml build/logs/phploc.xml src/ test/
    /usr/bin/php7.3 vendor/bin/pdepend --jdepend-xml=build/logs/jdepend.xml --jdepend-chart=build/pdepend/dependencies.svg --overview-pyramid=build/pdepend/overview-pyramid.svg src/
    /usr/bin/php7.3 vendor/bin/phpmd src/ xml phpmd.xml --reportfile build/logs/pmd.xml
    /usr/bin/php7.3 tools/phpcs --report=checkstyle --standard=phpcs.xml --report-file=build/logs/checkstyle.xml --extensions=php src/
    /usr/bin/php7.3 tools/phpcpd --log-pmd build/logs/pmd-cpd.xml --names-exclude "*Test.php" src/
    /usr/bin/phpdbg7.3 -qrr tools/phpunit -c phpunit.xml
    /usr/bin/php7.3 tools/phpdox -f phpdox.xml
