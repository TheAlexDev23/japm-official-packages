# Creating a JAPM package

JAPM packages are json files with metadata about the package as well as instructions for the installation and removal of the package.

The json file should be named package.json and located under:
`<the repo url>/packages/<package_name>/package.json`.
If this format is not followed the package would be considered corrupted or not found. And would not be installed by the package manager.

To submit a new package make a pull request and wait for approval.

## Format of the json file is the following:

```
{
	"name": "package name",
	"version": "1.0.0",
	"dependencies": [
		"package1",
		"package2",
		"package3"
	],
	"buuild dependencies": [
		"package1",
		"package2",
		"package3"
	],
	"files": [
		{
			"file name": "file1",
			"url": "https://url.of/file1"
		},
		{
			"file name": "file2",
			"url": "https://url.of/file2"
		},
		{
			"file name": "file3",
			"url": "https://url.of/file2"
		}
	],
	"pre install": [
		"system command 1",
		"system command 2",
		"system command 3",
	],
	"install": [
		"system command 1",
		"system command 2",
		"system command 3",
	],
	"post install": [
		"system command 1",
		"system command 2",
		"system command 3",
	],
	"remove": [
		"system command 1",
		"system command 2",
		"system command 3",
	]
}
```

### Explanation:

- name: the name of the package
- version: the version of the package
- description: additional information about the package
- dependencies: an array of strings with the names of other packages that are needed as dependencies
- files: an array of objects each representing a file that is needed to install or build the package:
	- URL: this field shows from where the package would be downloaded
	- file name: relative directory (to the installation folder) of the file that would be downoaded from URL.
- pre or post isntall: commands that will be ran before and after package install use this to setup install configuration and cleanup.
- install: array of string representing commands to install the package
- remove: same as install but for removal


### Limitations
- Install/remove commands cannot reach over **5000** characters in total. Consider using a script downloaded as a file if this is an issue for you.
- Install or remove instructions can't under no circumstance contain a semicolon, due to the way JAPM manages lists.
- If at least 1 field is not present the package is considered corrupted. If you don't have the need for some fields (ex. post install) just leave them empty but still define them in your .json file.

### Variables that can be used 

- `${project_dir}` This would be replaced with the directory where this package's files are downloaded to.

