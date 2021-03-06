## v0.4.2

The role that aws-runas assumed and the profile it used are now exposed as
`AWS_RUNAS_ASSUMED_ROLE_ARN` and `AWS_RUNAS_PROFILE`, respectively. These can be
used in scripts to track the profile being used or the role ARN used, in case
this data is needed later, or for troubleshooting purposes.

## v0.4.1

Fixed the escape sequence in the bash shell prompt indicator so that it has the
`\[` and `\]` enclosures - this fixes issues that the prompt was having with
line wrapping.

## v0.4.0

 * Dropping support for Ruby 2.1. You will need at least Ruby 2.2.6 to be using
   this gem now. If you have a version below this, please use a v0.3.x version.
 * MFA entry is no longer hidden from the terminal - you will see the digits you
   enter now.
 * Added a special indicator to `bash` prompts when running interactively. This
   prompt displays your running profile, like so: `(AWS:default)`. When running
   via --no-role, the indicator is just `(AWS)`. This should help to distinguish
   any AWS shells you may be running from regular ones.

## v0.3.1

This update sets `AWS_SDK_CONFIG_OPT_OUT` before the `aws-sdk` Ruby gem is
loaded to start assuming roles, to disable newer AWS Ruby SDK functionality that
allows the assumption of roles from `~/.aws/config` directly through the
toolchain. This conflicts with `aws-runas`'s own config file handling and breaks
in scenarios where one may want a default `~/.aws/config` file but no
credentials (ie: instance profiles).

## v0.3.0

Add session only features:

 * Add the `--no-role` command to load a profile and just get a
   session token, instead of assuming a role.
 * Changed default behaviour so that if `AWS_SESSION_TOKEN` exists, no MFA
   is loaded - this allows the assumption of multiple roles from within
   the same session.
 * `--no-role` will fail if a MFA serial is not present (it's pretty much
   useless - you will just be getting a session for the same access
   key/secret key with the same level of privilege that you did before).


## v0.2.0

 * `$SHELL` is now supported - if this environment variable exists, the shell
   in it will be launched.
 * Windows support:
  * `cmd.exe` is set as the default shell on non-Cygwin Windows systems.
  * Fixes to support mingw32 such as IO flushing and detection of a lack of
    `noecho` support.

## v0.1.3

 * Fixed #3 (better handling of invalid profile name).
 * Added guard for invalid file as well.

## v0.1.2

 * Fixed #1 and #2 (default credentials fallback bug and overzealous version
   restrictions).
