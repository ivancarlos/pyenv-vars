# luaenv-vars

This is a plugin for [luaenv](https://github.com/cehoffman/luaenv)
that lets you set global and project-specific environment variables
before spawning Lua processes.

## Installation

To install luaenv-vars, clone this repository into your
`~/.luaenv/plugins` directory. (You'll need a recent version of luaenv
that supports plugin bundles.)

    $ mkdir -p ~/.luaenv/plugins
    $ cd ~/.luaenv/plugins
    $ git clone https://github.com/cehoffman/luaenv-vars.git

## Usage

Define environment variables in an `.luaenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    DEBUG=1
    S3_BUCKET=mybucket

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `LUA_PATH`:

    LUA_PATH=$LUA_PATH:/u/shared/rocks/?.lua:/us/shared/rocks/?/init.lua

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

    JAVA_OPTS?=-server -Xmx768m -Xms768m -Xmn128m -Xss20m

In the above case, `JAVA_OPTS` will only be set if `$JAVA_OPTS` is
currently empty (i.e., if `[ -z "$JAVA_OPTS" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.luaenv/vars` file will be set
first. Then variables specified in `.luaenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.luaenv-vars` file in the current directory are set last.

Use the `luaenv vars` command to print all environment variables in the
order they'll be set.

## Version History

**1.2.0** (March 4, 2013)

* Converted from rbenv to luaenv
* Initial public release.

## License

&copy; 2012 Sam Stephenson, Chris Hoffman. Released under the MIT license. See
`LICENSE` for details.
