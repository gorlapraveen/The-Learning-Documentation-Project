1. I am experiencing problems to start Gnome Files (Nautilus) on Debian Testing (Buster). I noticed that after an upgrade (I don't know which) Nautilus started to delay some seconds to run.
   Running from console I found this error messages:

    ** (nautilus:23814): WARNING **: 18:19:23.023: Error on getting connection: Failed to load SPARQL backend: GDBus.Error:org.freedesktop.DBus.Error.NoReply: Message recipient disconnected from message bus without replying
    
    (nautilus:23814): GLib-GIO-CRITICAL **: 18:19:33.241: g_dbus_connection_signal_unsubscribe: assertion 'G_IS_DBUS_CONNECTION (connection)' failed
    
    (nautilus:23814): GLib-GObject-CRITICAL **: 18:19:33.241: g_object_unref: assertion 'G_IS_OBJECT (object)' failed
    
    (nautilus:23814): GLib-GObject-CRITICAL **: 18:19:33.241: g_object_unref: assertion 'G_IS_OBJECT (object)' failed



Sol:  I discovered that if you delete `~/.cache/tracker/` the problem is solved.
