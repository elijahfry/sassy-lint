# Config File

### Configuration Options
When passing options directly to `Sassy-lint` option `config-file` will tell Sassy lint the path to a custom config file. `config-file` should be set to a path plus file name relative to where Sassy lint is being run from OR an absolute path. If not included, Sassy lint will attempt to find the closest config file, or fall back to the default one.

### Config File Options

You may specify a config file in your current config file as follows:

```yaml
options:
  config-file: my-folder/my-other-config.yml
rules:
  no-ids: 2
```

The config file loaded from the `config-file` option will be treated as a base config file and as such will be extended with the rules and options in your main config. The path of this must be either an absolute path or a path relative to your main config file.

**Absolute path**

`/root/my/projects/config/extend/.sassy-lint.yml`

**Relative path**

`extra-config/.sassy-lint.yml`

## Example

**Project Structure**
```
my-project/
 - .sassy-lint-A.yml
 - sub-folder/
   - .sassy-lint-B.yml
```

**.sassy-lint-A.yml**
```yml
options:
  config-file: sub-folder/.sassy-lint-B.yml
rules:
  no-ids: 1
```

**.sassy-lint-B.yml**
```yml
rules:
  no-ids: 2
  no-important: 1
```

**start Sassy-lint from the my-project directory**

`sassy-lint -c .sassy-lint-A.yml`


In the scenario above the first config would load and merge the second config recursively.

The resulting config you could expect would be:

```yml
options:
  config-file: sub-folder/.sassy-lint-B.yml
rules:
  no-ids: 1
  no-important: 1
```

Notice how the B config's `no-ids` rule is ignored as we are 'extending' A from B.

There is no limit to how many config files can be loaded, but please do be aware of circular dependencies.
