MOODLE DEVELOPMENT VISUALISATION IN GOURCE
==========================================

This repository contains useful resources to render Moodle (http://moodle.org)
development visualisation using Gource (http://code.google.com/p/gource/)

Once you have Gource installed on your computer, use the moodle.log from this
file to visualise the Moodle development history

    $ gource moodle.log

To display Moodle logo and user avatars from moodle.org pages:

    $ gource --logo logo.png \
             --highlight-users \
             --hide filenames,mouse,progress \
             --user-image-dir usr/ moodle.log

To render MPEG video with the visualisation:

    $ gource --viewport 1024x768 --time-scale 2 --auto-skip-seconds 1 \
             --seconds-per-day 1 --logo logo.png --highlight-users \
             --hide filenames,mouse,progress moodle.log \
             --output-framerate 25 --output-ppm-stream - |
             ffmpeg -vpre libx264-default -y -b 3000K -r 25 \
                    -f image2pipe -vcodec ppm -i - \
                    -vcodec libx264 moodle.mp4
