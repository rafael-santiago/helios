# A simple ffmpeg toolset

The idea under this toolset is to be extensible. So, "from factory" you will find few automations for commons tasks
that anybody could do using ffmpeg tool, which covers:

- A *MP4* conversor (internal task-name: ``mp4conversor``)
- An iPod encoder (internal task-name: ``ipodencoder``)
- A *FLV* to *MP4* encoder (internal task-name: ``avi2gif``)
- A *AVI* to *GIF* encoder (internal task-name: ``mp3fromvid``)
- An video audio extractor which saves the output as *MP3* (internal task-name: ``flv2mp4``)

## So, how to use it?

Personally, I like letting a forge directory prepared with an invocation file in order to make my life easy, because
commonly the use of ``ffmpeg`` tends to be sudden. Follows my forge project file:

        # "Forgefile.hsl"
        include ~/toolsets/ffmpeg/ffmpeg.hsl

        var inputs type list;
        var outputs type list;

        project my-ffmpeg-butler : toolset "ffmpeg-toolset" : $inputs, $outputs ;

        my-ffmpeg-butler.prologue() {
            $inputs = hefesto.sys.get_option("input");
            $outputs = hefesto.sys.get_option("output");
        }

Follows the ``.ivk`` file which resides in the same forge project file directory:

        --forgefiles=Forgefile.hsl --Forgefile-projects=my-ffmpeg-butler

Now, you have to consider the internal task-name of the operation that you want to perform. If this operation
not exists yet, you should extend the toolset by your own and it can be very intersting too.

Supposing that you want to convert a *.WMV* video to *.MP4*:

>``hefesto --input=the-wmv-input.wmv --output=the-mp4-output.mp4 --ffmpeg-task=mp4conversor``

Do you want to extract some audio from a video?

>``hefesto --input=the-mp4-output.mp4 --ffmpeg-task=mp3fromvideo

The toolset can infers the output file names if you do not inform them.

*Windows* users, if you need to supply a input file path with spaces you have to escape it. Look:

>``hefesto --input="\"C:\\Another\\Folder\\From Outer space\\sample.wmv\"" --output=here.mp4 --ffmpeg-task=mp4conversor

You can pass several files to be processed by the same task too:

>``hefesto --ffmpeg-task=mp3fromvideo --input=show-001.mp4,show-002.mp4,show-003.mp4 --output=song-001.mp3,song-002.mp3,song-003.mp3``

That is it!
Enjoy.
