# Proof: Instant feedback on static web content

## Steps

1. Read config from `.proofrc`, if it exists
    1. If it doesn't exist then ask questions to form config
    1. Write config to .proofrc
1. Test ssh access; return error if not setup
1. Use `rsync` to push the selected target directory to the chosen subdirectory on the server.
1. Create a location directive file based on configuration and push it to `/etc/nginx/static-projects/` on the server.
1. Use `nginx -t` to test that everything is ok.
1. Reload nginx service

## Miscellaneous Thoughts

* Name of subdirectory should be configurable
* Target server name should be configurable
* Should allow for HTTP basic auth of specific subdirectories
* Should allow for whatever target directory (containing dist build) to be pushed

## Client Requirements

* Client **must** have abott's proof rsa keys (found in 1Password)
* Client **must** have an SSH config entry for the proof server

### Server Requirements

* Server **must** be setup with abott's rsa keys
* Server **must** allow the `abott` user passwordless login
* Server **must** allow the `abott` user passwordless `sudo`
* The `abott` user must be part of the `www-data` group
