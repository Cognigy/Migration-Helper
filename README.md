# Cognigy v3 to v4 Migration-Helper
Version: 1.0.6

This tool helps to migrate Cognigy.AI v3 export packages to Cognigy.AI v4, taking advantage of some of the most advanced features that Cognigy.AI v4 is offering.

It is a command line interface (CLI) tool, available for the following platforms:

- Linux
- MacOS
- Windows

Example: `./migrator-linux -a YOUR_API_KEY -h https://api-trial.cognigy.ai -f EXPORT.ZIP`

>Please see "Limitations" below to see what can be auto-migrated and what can't.

## Options

Use --help to see all the options on the command line.

| Option | Option Long Form            | Description                                                                              | Default                         |
| ------ | --------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------- |
| -a     | --api-key <apiKey>          | change the used apiKey to connect to the target server                                   | -                               |
| -f     | --file <file>               | the exported 3.x project                                                                 | -                               |
| -h     | --host <host>               | the host url to the target api server                                                    | "https://api-trial.cognigy.ai") |
| -s     | --snapshot <snapname>       | the name of the snapshot to create                                                       | -                               |
| -n     | --projectname <name>        | the name of the project to create                                                        | -                               |
| -l     | --projectlocale <name>      | the name of the locale to use                                                            | -                               |
| -id    | --targetProject <projectId> | the id of the target project                                                             | -                               |
| -t     | --trainFlows                | start training of flows after creation                                                   | false                           |
| -r     | --removeproject             | remove project after migration                                                           | false                           |
| -sc    | --softconvert               | convert Say Node webchat & facebook tab content into default, but keep default if exists | false                           |
| -fc    | --forceconvert              | convert webchat & facebook data into default, overwrite default if exists                | false                           |
| -dc    | --deletechannel             | delete webchat & facebook channel data if converted to default                           | false                           |
| -o     | --output-dir <outputDir>    | the directory where to extract the files of the zip-File                                 | "./tmp"                         |
| -cl    | --do-cognigy-lexicons       | should import cognigy lexicons                                                           | false                           |
| -cf    | --do-cognigy-flows          | should import cognigy flows                                                              | false                           |
| -p     | --password <password>       | change the used password for unzipping the exported file                                 | -                               |
|        | --help                      | display help for command                                                                 | -                               |

### Advanced Examples

#### Provide Project Name & Locale
Example: `./migrator-linux -a YOUR_API_KEY -h https://api-trial.cognigy.ai -f EXPORT.ZIP -n testproject -l en-US -sc`

- Unzips EXPORT.ZIP
- Creates Agent Project 'testproject' with locale 'en-US'
- Migrates the project whilst converting webchat & facebook say node tab content into the new Cognigy.AI default tab, keeping original default tab content if it exists

#### Provide Project Name & Locale
Example: `./migrator-linux -a YOUR_API_KEY -h https://api-trial.cognigy.ai -f EXPORT.ZIP -n testproject -l en-US -s snap1 -r`

- Unzips EXPORT.ZIP
- Creates Agent Project 'testproject' with locale 'en-US'
- Migrated project
- Creates, packages and downloads snapshot 'snap1'
- Removes project from host afterwards

## Limitations

The Migration Helper can migrate the following resources:

- Flows
- Flow Nodes (except for Custom Modules)
- Flow Intents
- Lexicons
- Playbooks
- NLU Connectors
- Processes (will be converted to Flows)
- Endpoints

The following can't be migrated, as the concepts have changed in v4:

- Custom Modules (are now Extensions and must be re-built)
- Connections (were a different type of connection in v3)
- Secrets (are now Connections in v4)

## Release Notes

### 1.0.7

- Adds ability to convert switchFlow Nodes to Goto Nodes with injected Text and Data

### 1.0.6

- Added ability to train Flows after creation by using `-t`
- Renamed option to set target project IDs from `-t` to `-id`