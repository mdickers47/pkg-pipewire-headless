pipewire-headless: This is an arch package that will drop in all the
(many) configuration files that have to be modified to get pipewire
working as a system service, disassociated from a session belonging to
a logged-in user.

This will configure the system-wide pipewire the way I want it to work,
which is:

+ local ALSA fakery is set up so that any naive process opening ALSA
  for output will go to pipewire
+ local pipewire socket in /run/pipewire is owned by pipewire:audio with
  mode 0660, such that any pw-cli process (etc) run in group 'audio' should
  work
+ pipewire-pulse takes unrestricted commands from tcp port 4713 on all
  interfaces, such that 'pactl -s servername' (etc) from anywhere works
+ pipewire has a RTP receiver listening on port 46000 on all interfaces

This should be a reasonable scheme for the use case that is "having a
DSP on the LAN that can be used or controlled from anywhere on the LAN."
You would not want to connect it to the internet.

If you want a slightly different configuration, have fun figuring out
the dozens of configuration files, in a mishmash of lua and pidgin JSON,
that pipewire scatters across no fewer than 9 directories (3 each for
pipewire, pipewire-pulse, and wireplumber).  Don't forget the 5 systemd
units might have to be modified too!

After installing you will need to:

+ `systemctl enable pipewire`
+ `systemctl enable pipewire-pulse`
+ `systemctl enable wireplumber`

If you want everything showing up at the RTP receiver to come directly
out the speakers, then somewhere you will have to also do this:

+ `pw-link -Ilio # should see a bunch of things`
+ `pw-link 37 49 # patch thing 37 -> 49`

2023-12-06 mikeyd
