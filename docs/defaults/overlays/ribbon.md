# Ribbon Overlays

The `ribbon` Default Overlay File is used to create a ribbon overlay based on the Top Lists of various sites on each 
item within your library.

![](images/ribbon.png)

## Requirements & Recommendations

Supported Overlay Level: Movie, Show

## Supported Ribbon

| Ribbon                          | Key               | Weight |
|:--------------------------------|:------------------|:-------|
| Oscars Best Picture             | `oscars`          | `180`  |
| Oscars Best Director            | `oscars_director` | `170`  |
| Golden Globe Winner             | `golden`          | `160`  |
| Golden Globe Director           | `golden_director` | `150`  |
| BAFTA Winner                    | `bafta`           | `140`  |
| Cannes Winner                   | `cannes`          | `130`  |
| Berlinale Winner                | `berlinale`       | `120`  |
| Venice Winner                   | `venice`          | `110`  |
| Sundance Winner                 | `sundance`        | `100`  |
| Emmys Winner                    | `emmys`           | `90`   |
| Critic's Choice Winner          | `choice`          | `80`   |
| Independent Spirit Award Winner | `spirit`          | `70`   |
| César Winner                    | `cesar`           | `60`   |
| IMDb Top 250                    | `imdb`            | `50`   |
| Rotten Tomatoes Certified Fresh | `rotten`          | `40`   |
| Metacritic Must See             | `metacritic`      | `30`   |
| Common Sense Selection          | `common`          | `20`   |
| Razzies Winner                  | `razzie`          | `10`   |

## Config

The below YAML in your config.yml will create the overlays:

```yaml
libraries:
  Movies:
    overlay_files:
      - pmm: ribbon
  TV Shows:
    overlay_files:
      - pmm: ribbon
```

## Template Variables

Template Variables can be used to manipulate the file in various ways to slightly change how it works without having to 
make your own local copy.

Note that the `template_variables:` section only needs to be used if you do want to actually change how the defaults 
work. Any value not specified will use its default value if it has one if not it's just ignored.

??? abstract "Variable Lists (click to expand)"

    * **File-Specific Template Variables** are variables available specifically for this PMM Defaults file.

    * **Overlay Template Variables** are additional variables shared across the PMM Overlay Defaults.

    ??? example "Default Template Variable Values (click to expand)"

        | Variable            | Default  |
        |:--------------------|:---------|
        | `horizontal_offset` | `0`      |
        | `horizontal_align`  | `right`  |
        | `vertical_offset`   | `0`      |
        | `vertical_align`    | `bottom` |
        
    === "File-Specific Template Variables"

        | Variable                     | Description & Values                                                                                                    |
        |:-----------------------------|:------------------------------------------------------------------------------------------------------------------------|
        | `use_all`                    | **Description:** Used to turn on/off all keys. <br>**Default:** `true` <br>**Values:** `true` or `false`                |
        | `weight_<<key>>`<sup>1</sup> | **Description:** Controls the weight of the Overlay. Higher numbers have priority.<br>**Values:** Any Number            |
        | `style`                      | **Description:** Controls the color of the ribbon. <br>**Default:** `yellow` <br>**Values:** `yellow, gray, black, red` |

        1. Each default overlay has a `key` that when calling to effect a specific overlay you must replace `<<key>>` 
        with when calling.

    === "Overlay Template Variables"

        {%
           include-markdown "../overlay_variables.md"
        %}
    
???+ example "Example Template Variable Amendments"

    The below is an example config.yml extract with some Template Variables added in to change how the file works.
    
    ```yaml
    libraries:
      Movies:
        overlay_files:
          - pmm: ribbon
            template_variables:
              style: black
              weight_metacritic: 35
              use_common: false
    ```
