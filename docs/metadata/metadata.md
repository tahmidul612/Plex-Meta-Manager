# Metadata Files

Metadata files are used to create and maintain collections and metadata within the Plex libraries on the server.

If utilized to their fullest, these files can be used to maintain the entire server's collections and metadata, and can be used as a backup for these in the event of a restore requirement.

Collections, templates, metadata, and dynamic collections are defined within one or more Metadata files, which are linked to libraries in the [Libraries Attribute](../config/libraries.md#metadata-path) within the [Configuration File](../config/configuration.md).

These are the attributes which can be used within the Metadata File:

| Attribute                                               | Description                                                                                                                                                                       |
|:--------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`templates`](templates)                                | contains definitions of templates that can be leveraged by multiple collections                                                                                                   |
| [`external_templates`](templates.md#external-templates) | contains [path types](../config/paths) that point to external templates that can be leveraged by multiple collections                                                             |
| [`collections`](#collection-attributes)                 | contains definitions of collections you wish to add to one or more libraries                                                                                                      |
| [`dynamic_collections`](#dynamic-collection-attributes) | contains definitions of [dynamic collections](dynamic) you wish to create                                                                                                         |
| [`metadata`](#metadata-attributes)                      | contains definitions of metadata changes to [movie](metadata/movie), [show](metadata/show), or [music](metadata/music) library's items [movie titles, episode descriptions, etc.] |

* One of `metadata`, `collections` or `dynamic_collections` must be present for the Metadata File to execute.
* Example Metadata Files can be found in the [Plex Meta Manager Configs Repository](https://github.com/meisnate12/Plex-Meta-Manager-Configs/tree/master/PMM)

## Collection Attributes

Plex Meta Manager can run a number of different operations within `collections` and such as:

* Automatically build and update collections and playlists
* Sync the collection with the source list if one is used
* Send missing media to Sonarr/Radarr (Lidarr not supported at this time)
* Show and Hide collections at set intervals (i.e. show Christmas collections in December only)

Each collection requires its own section within the `collections` attribute and unlike playlists, collections can be built using as many Builders as needed.

```yaml
collections:
  Trending Movies:
    # ... builders, details, and filters for this collection
  Popular Movies:
    # ... builders, details, and filters for this collection
  etc:
    # ... builders, details, and filters for this collection
```

There are multiple types of attributes that can be utilized within a collection:

* [Builders](builders)
* [Settings/Updates](update)
* [Filters](filters)

### Example

```yaml
collections:
  Trending:
    trakt_trending: 10
    tmdb_trending_daily: 10
    tmdb_trending_weekly: 10
    sort_title: +1_Trending
    sync_mode: sync
    smart_label: random
    summary: Movies Trending across the internet
  Popular:
    tmdb_popular: 40
    imdb_list:
      url: https://www.imdb.com/search/title/?title_type=feature,tv_movie,documentary,short
      limit: 40
    sort_title: +2_Popular
    sync_mode: sync
    smart_label: random
    summary: Popular Movies across the internet
```

## Dynamic Collection Attributes

Plex Meta Manager can dynamically create collections based on a verity of different criteria, such as

* Collections for the top `X` popular people on TMDb (Bruce Willis, Tom Hanks etc.)
* Collections for each decade represented in the library (Best of 1990s, Best of 2000s etc.)
* Collections for each of the moods/styles within a Music library (A Cappella, Pop Rock etc.)
* Collections for each of a Trakt Users Lists.

Below is an example dynamic collection which will create a collection for each of the decades represented within the library:

```yaml
dynamic_collections:
  Decades:
    type: decade
```

## Metadata Attributes

Plex Meta Manager can automatically update items in Plex [Movie](metadata/movie), [Show](metadata/show), and [Music](metadata/music) Libraries based on what's defined within the `metadata` attribute.

Each metadata requires its own section within the `metadata` attribute. 

Each item is defined by the mapping name. Rules for how to match are on the Respective Library Metadata Pages.
