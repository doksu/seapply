# seapply
seapply command for SELinux

The seapply command is used to apply differential^ SELinux configuation changes to a host and is designed for use with configuration management tools such as Ansible or puppet.

^ in contrast to `semanage -i`, seapply only rectifies differences between the running configuration and the supplied configuration, rather than reapplying all configurations, providing significantly better performance.

### Requirements

policycoreutils-python package on RHEL 6+ or Fedora-based distribution.

### Limitations

At this time, only RBACs configurations are supported.

### Usage

1.    Configure RBACs using semanage on a staging host, then export the configuration to json:

          seapply export /path/to/file.json

      Although not recommended, you can manually edit the JSON (for example: add line breaks and formatting for readability), keeping in mind that the roles specified in seluserRecords must be in alphabetical order.

      N.B. If no path is provided, the configuration is sent to stdout

2.    Test the configuration on a 2nd machine:

          seapply dryrun /path/to/file.json

3.    If no errors were raised, apply the configuration on the 2nd machine:

          seapply apply /path/to/file.json

4. Deploy the configuration to fleet via configuration management (Satellite 6 content views, etc.)
