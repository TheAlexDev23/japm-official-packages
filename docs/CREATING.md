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
	"description": "package description",
	"dependencies": [
		"package1",
		"package2",
		"package3"
	],
	"build dependencies": [
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

The order of statemetns shouldn't matter, but try to use the standart for more readability.

- name: the name of the package
- version: the version of the package
- description: additional information about the package
- dependencies: an array of strings with the names of other packages that are needed as dependencies
- files: an array of objects each representing a file that is needed to install or build the package:
	- URL: this field shows from where the package would be downloaded
	- file name: directory to download to. Don't write a full directory like /tmp/file.sh rather a relative one like files/file.sh, and it will be downloaded in each package's directory. You can later access that directory within commands using [variables](#variables-that-can-be-used).
- pre or post install: commands that will be ran before and after package install use this to setup install configuration and cleanup.
- install: array of string representing commands to install the package
- remove: same as install but for removal

### Limitations
- Install/remove commands cannot reach over **5000** characters in total. Consider using a script downloaded as a file if this is an issue for you.
- Install or remove instructions can't under no circumstance contain a semicolon, due to the way JAPM manages lists.
- If at least 1 field is not present the package is considered corrupted. If you don't have the need for some fields (ex. post install) just leave them empty but still declare them in your .json file.

### Variables that can be used 

- `${package_dir}` Use this in comands and it will be automatically replaced by the direcotry of the package. Files are downloaded under `dir of package`+`file name (in json)`. 
