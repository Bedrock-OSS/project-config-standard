# project-config-standard

This standard aims to provide the specification of a JSON config file for Minecraft projects that provides a common foundations for all tools in the corresponding ecosystem to build upon.

## `config.json` File

The following TypeScript interfaces describe the structure of this file.

```typescript
interface ConfigJson {
	/**
	 * Defines the type of a project
	 */
	type: 'minecraftBedrock' | 'minecraftJava'

	/**
	 * The name of the project
	 */
	name: string

	/**
	 * Creators of the project
	 *
	 * @example ["solvedDev", "Joel ant 05"]
	 */
	authors: string[]

	/**
	 * The Minecraft version this project targets
	 *
	 * @example "1.17.0"/"1.16.220"
	 */
	targetVersion: string

	/**
	 * Experimental gameplay the project intends to use.
	 * Exact mapping of strings to experimental gameplay toggles needs to be specified later.
	 *
	 * @example ["upcomingCreatorFeatures", "cavesAndCliffs"]
	 */
	minecraftExperiments: string[]

    	/**
    	 * Additional capabilities the project wants to use
    	 * 
    	 * @example ["scriptingAPI", "gameTestAPI"]
    	 */
    	capabilities: string[]

	/**
	 * The namespace used for the project. The namespace "minecraft" is not a valid string for this field.
	 *
	 * @example "my_project"
	 */
	namespace: string

	/**
	 * Maps the id of packs this project contains to a path relative to the config.json
	 *
	 * @example { "behaviorPack": "./BP", "resourcePack": "./RP" }
	 */
	packs: {
		[
			packId:
				| 'behaviorPack'
				| 'resourcePack'
				| 'skinPack'
				| 'worldTemplate'
				| 'dataPack'
		]: string
	}

	/**
	 * Allows users to define additional data which is hard to find for tools
	 * (e.g. scoreboards setup inside of a world)
	 *
	 * @example { "names": { "include": ["solvedDev"] } }
	 */
	packDefinitions: {
		families: PackDefinition
		tags: PackDefinition
		scoreboardObjectives: PackDefinition
		names: PackDefinition
	}

	/**
	 * Tools can create their own namespace inside of this file to save tool specific data and settings
	 *
	 * @example { "bridge": { "darkTheme": "bridge.default.dark", "lightTheme": "bridge.default.light" } }
	 */
	[uniqueToolId: string]: any
}

interface PackDefinition {
	/**
	 * Optional: Define e.g. the type of a scoreboard objective
	 *
	 * @example "dummy"
	 */
	type?: string
	/**
	 * Strings to exclude from a tool's collected data
	 */
	exclude: string[]
	/**
	 * String to add to a tool's collected data
	 */
	include: string[]
}
```

## Project Structure

A common project structure for a Minecraft Bedrock project following this standard looks like this:

```
- MyProject/
  - BP/
  - RP/
  - SP/
  - WT/
  - config.json
```

The specification only handles the config.json file at the root of the project. The exact folder names of individual packs can change based on its content.
