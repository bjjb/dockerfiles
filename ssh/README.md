An SSH service with a login for the user who built it

Expects one build argument: `user`, and you should copy your RSA public key
into the build directory before you build, so it can be added to the user's
`.ssh/authorized_keys`.
