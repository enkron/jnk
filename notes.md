# notes
## Closures
We want to define code in one place in our program,
but only execute that code where we actually need the result.
This is a use case for closures

## Patterns
Using primitive values when a complex type would be more appropriate is
an anti-pattern known as primitive obsession.

## Docker
### Docker volumes:
one of the most common use cases for this is to share a directory that
holds your application code. You modify the application code on your host
machine, and those changes are detected by the application server running inside the Docker container.

### RUN and ENTRYPOINT
RUN and ENTRYPOINT are two different ways to execute a script.
RUN means it creates an intermediate container, runs the script and freeze the new state of that container in a new intermediate image. The script won't be run after that: your final image is supposed to reflect the result of that script.

ENTRYPOINT means your image (which has not executed the script yet) will create a container, and runs that script

## Bash
### Strict mode
```bash
#!/bin/bash

set -eu -o pipefail -o posix

function main() {
    echo hello
}

main "${@}"
```
