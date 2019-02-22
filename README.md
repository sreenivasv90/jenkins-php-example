
    phive install --copy
    composer install
    find src/ -name "*.php" | xargs php -l
    tools/phploc --count-tests --log-csv build/logs/phploc.csv --log-xml build/logs/phploc.xml src/ test/
    vendor/bin/pdepend --jdepend-xml=build/logs/jdepend.xml --jdepend-chart=build/pdepend/dependencies.svg --overview-pyramid=build/pdepend/overview-pyramid.svg src/
    phpmd src/ xml build/phpmd.xml --reportfile build/logs/pmd.xml
    tools/phpcs --report=checkstyle --standard=phpcs.xml --report-file=build/logs/checkstyle.xml --extensions=php src/
    tools/phpcpd --log-pmd build/logs/pmd-cpd.xml --names-exclude "*Test.php" src/
    phpdbg -qrr tools/phpunit -c phpunit.xml
    tools/phpdox -f build/phpdox.xml