## php cli bookworm container

Creating a new build with tag '8.4' without multi-arch support:

    $ PHP_TAG=8.4 && docker build --build-arg PHP_TAG=$PHP_TAG  -t php-cli-laravel:$PHP_TAG -f ./Dockerfile .
    $ docker tag php-cli-laravel:8.4 metalmanufactures/php-cli-laravel:8.4
    $ docker login 
    $ docker push metalmanufactures/php-cli-laravel:8.4

Sometimes the base php image bakes in libraries in minor versions. For example the tokenizer library. You can run this to check that:

    $ docker run --rm php:8.4-cli-laravel php -i | grep -i token

Creating a new build with tag '8.4' **with** multi-arch support:

    $ docker buildx build --platform linux/arm64,linux/amd64 --push -t metalmanufactures/php-cli-laravel:8.4 -f ./Dockerfile .

If you see the error "multiple platforms feature is currently not supported for docker drive" above, run the following `$ docker buildx create --use` and then run `docker buildx ls` to make sure `linux/arm64,linux/amd64` is listed.
