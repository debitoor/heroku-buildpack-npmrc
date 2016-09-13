# heroku-buildpack-npmrc
A Heroku buildpack for overriding the .npmrc file in the build directory with the contents of a config var. Useful for authorizing with npm when installing private packages.

## Configure Multiple Buildpacks
### _Option 1:_ Heroku CLI or Dashboard
Add the buildpack to your Heroku app either using the CLI or the Heroku dashboard. The `heroku-buildpack-npmrc` needs to run before any buildpack using npm. In the following example, it runs before the `heroku/nodejs` buildpack.
```bash
$ heroku buildpacks:set --index 1 https://github.com/debitoor/heroku-buildpack-npmrc.git
$ heroku buildpacks:add heroku/nodejs
```

### _Option 2:_ Use `heroku-buildpack-multi`
Instead of setting the buildpacks directly with Heroku they can also be configured using a `.buildpacks` in combination with [`heroku-buildpack-multi`]( https://github.com/heroku/heroku-buildpack-multi).

``` bash
$ heroku buildpacks:set https://github.com/heroku/heroku-buildpack-multi.git  
```

The same example given for the CLI use would have the following `.buildpacks` file.

``` bash
$ cat .buildpacks
https://github.com/debitoor/heroku-buildpack-npmrc.git
https://github.com/heroku/heroku-buildpack-nodejs.git
```

## Configure Config Var
Add the NPMRC config var in Heroku with the contents of your .npmrc file.

``` bash
 $ heroku config:set NPMRC=//registry.npmjs.org/:_authToken=00000000-0000-0000-0000-000000000000
```
