# entrance-plando

A tool for editing custom entrance connections in the OoTMM combo randomizer.

Although entrance plando is technically supported in the OoTMM web generator (v33.0), custom entrances currently do not display. This tool allows you to directly edit a config file downloaded from the web generator, and add entrances from [entrances.yml](https://github.com/OoTMM/OoTMM/blob/master/data/defs/entrances.yml). The updated config can then re-upload to the OoTMM web generator with plando connections. 

Though it should work with entrance shuffling, certain combinations of entrances may cause generator errors, be overridden by the generator, or cause weird polarity. See troubleshooting notes.


# Instructions
1. Export a config file from OoTMM. The [YAML file](https://github.com/OoTMM/OoTMM/blob/master/data/defs/entrances.yml) can be found in the OoTMM repo.
2. Download the entrance_mapper.html file or clone this repo.
3. Open entrance_mapper.html in a browser.
4. Load the config file and YAML file. It will require an internet connection to fetch the YAML parser.**
5. Edit entrances within the app. You will need to assign two-way entrances manually.
6. When finished, click "Download updated.json." Review file differences.
7. Import updated.json into OoTMM. You may want to re-export the config file to make sure it uploaded correctly.
8. Try generating a seed.
9. Review the spoiler log to see if any custom entrance connections were skipped.

**By default, the app fetches the YAML parser from Cloudflare’s CDN. To use the app without an internet connection, download js-yaml.min.js and place it in the same directory as entrance_mapper.html. Then, you can edit this line to reference the parser locally:
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/js-yaml/4.1.0/js-yaml.min.js"></script>
```

# Troubleshooting
If an error occurs during world generation, try removing individual entrance plando connections. Certain entrances, such as those connected to end bosses, may not work. If it fails to generate the item pool, you could try shuffling more item locations, increasing the number of items, or adjusting entrance polarity in the OoTMM entrance shuffle settings.


# Files Required
1. A YAML file containing entrances
3. A config file in which to edit plando entrance connections


# YAML file
This file serves as the entrance database.

Entries in the YAML file are expected to follow a general template. Here are a couple of non-exhaustive examples:

```
BFBB_SPAWN_POINT:
{
    game: bfbb,
    id: 0x000,
    type: spawn-point,
    maps: [NONE, NONE],
    areas: ['BFBB SPAWN POINT', "BFBB Mary's House"],
    debug: ['COMMON', "Mary's House"]
}

GG_CAVE_EXIT_MONKEY_PLAYGROUND:
{
    game: gg,
    id: 0x1234,
    type: cave-exit,
    maps: [NONE, GG_CHAD_CITY],
    areas: ['GG Monkey Playground', 'GG Chad City Northwest'],
    reverse: GG_CAVE_MONKEY_PLAYGROUND
}
```


# Config (JSON) file
This is the config file containing OoTMM seed settings.
Expected JSON structure:

```
{
    "data": {
        // Other config properties...
        "settings": {
            // Other settings...
            "plando": {
                "entrances": {
                    // Your custom entrances will appear here.
                    "SOURCE_ENTRANCE": "DESTINATION_ENTRANCE"
                }
            }
        }
    }
}
```
