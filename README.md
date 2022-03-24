# Tourmapper 

## What is this?

This is a script for generating maps from GPS tracking data and geo-tagged images (see an example here. 

## Usage 

The script runs in python 3 and wraps Folium / Leaflet, a very sophisticated library for producing interactive maps. 

Map generation is done using the `tourmapper.make_map()` function using the following arguments. All arguments should be passed as keyword arguments. 

### Required arguments 

- `gps_dir` string path to directory containing `.gpx` files, all of which will be loaded in ascending date order. Each file will be a separate trace on the map. 

### Optional arguments 
- `map_params` dict containing map-specific arguments passed to `folium.Map()` (see the Folium or Leaflet documentation)
- `outpath` string path to save output as `.html` file
- `image_dir` string path to directory containing `.jpeg/.jpg` images with GPS EXIF tags, all of which will be loaded
- `line_colours` string, or list of strings which will be cycled, of colours to use when plotting each `.gpx` file. These can either be simple names eg `red` or hex colour code `#3388ff`
- `ride_text` list of strings, same length as number of `.gpx` files, of text to insert on the marker at the end of each file's trace on the map 
- `remote_image_url` string URL stub for remote loading of images (see below section)
- `image_width` default 500, popup size for landscape images
- `image_height` default 400, popup size for portrait images 

## Map customisation 

demo tiles: https://github.com/leaflet-extras/leaflet-providers

## Local vs. remote images 

By default, images are embedded directly within the HTML file containing the map. This means the map and images are completely self-contained within that file, which makes it very easy to share them, but can lead to very large file sizes if there are lots of images. This could be a problem if you intend to put the map online as it can lead to long page load times. 

The alternative to this is to add the images as remote objects. This keeps the file size down, because they are not embedded into HTML, but means you need somewhere to store the images remotely (a website, hosting service etc) from which they will be loaded on-demand. Remote images can be added using the `remote_image_url` argument. 

Example: the `image_dir` contains the images `A.jpg`, `B.jpg` and `C.jpg`. To insert them as remote images instead of local, first place them on a remote host (for example, `yourwebsite.com/assets/images`). Pass this URL as the `remote_image_url` argument, and the images A,B,C will be inserted as follows: `yourwebsite.com/assets/images/A.jpg`, `yourwebsite.com/assets/images/B.jpg` etc. 

