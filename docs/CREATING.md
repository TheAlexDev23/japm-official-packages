# Creating a JAPM package

JAPM packages are json files with metadata about the package as well as instructions for the installation and removal of the package.

The json file should be named package.json and located under:
`<the repo url>/packages/<package_name>/package.json`.
If this format is not followed the package would be considered corrupted or not found. And would not be installed by the package manager.

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
	"files": [
		{
			"name": "file1",
			"url": "https://url.of/file1"
		},
		{
			"name": "file2",
			"url": "https://url.of/file2"
		},
		{
			"name": "file3",
			"url": "https://url.of/file2"
		}
	],
	"install": [
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
- dependencies: an array of strings with the names of other packages that are needed as dependencies
- files: an array of objects each representing a file that is needed to install or build the package:
	- URL: this field shows from where the package would be downloaded
	- name: relative directory (to the installation folder) of the file that would be downoaded from URL.
- install: array of string representing commands to install the package
- remove: same as install but for removal

### Variables that can be used 

- `${project_dir}` This would be replaced with the directory that the files are downloaded to (for now it's: `/tmp/japm/<package name>/<file name>`)

