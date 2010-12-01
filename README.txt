MOODLE DEVELOPMENT VISUALISATION IN GOURCE
==========================================

This repository contains useful resources to render Moodle (http://moodle.org)
development visualisation using Gource (http://code.google.com/p/gource/)

Once you have Gource installed on your computer, use the moodle.log from this
repository to visualise the Moodle development history.

    # gource moodle.log

To display Moodle logo and user avatars from moodle.org pages:

    # gource --logo logo.png \
             --highlight-users \
             --hide filenames,mouse,progress \
             --user-image-dir usr/ moodle.log

I have found the following parameters suitable for an interactive animation:

    # gource --fullscreen --seconds-per-day 0.5 --auto-skip-seconds 1 \
             --multi-sampling --logo logo.png --title 'http://moodle.org' \
             --highlight-users --hide filenames --user-image-dir usr/ moodle.log

To render MPEG video with the visualisation:

    # gource --viewport 1280x720 --seconds-per-day 0.5 --auto-skip-seconds 1 \
             --logo logo.png --title 'http://moodle.org' --highlight-users \
             --hide bloom,filenames,mouse,progress --user-image-dir usr/ \
             moodle.log --output-framerate 25 --output-ppm-stream - | \
      ffmpeg -y -b 3000K -r 25 -f image2pipe -vcodec ppm -i - \
             -vcodec libx264 -vpre libx264-default moodle.mp4
