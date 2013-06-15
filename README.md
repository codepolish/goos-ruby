# GOOS in Ruby

My attempt at implementing the auction sniper example from part II of *Growing
Object-Oriented Software, Guided By Tests*. I've tagged the repository at the
end of each chapter (currently I've only done chapters 10 and 11).

## Tools

### XMPP

The [Vines](http://www.getvines.org/) XMPP server is started and stopped
automatically by the tests.

For the client I tried [xmpp4r](http://home.gna.org/xmpp4r/) and
[xmp4r-simple](https://github.com/blaine/xmpp4r-simple), but couldn't get
either of them to work properly, so ended up with
[Blather](https://github.com/adhearsion/blather).  This runs in
[EventMachine](http://rubyeventmachine.com/) so has to be started in its own
thread to avoid blocking the rest of the application.

### GUI

I considered using Swing to keep close to the book, but that would have
restricted the app to only running on JRuby. I tried Tk and Qt, but couldn't
figure out any easy way of testing them, and they didn't seem to take
particularly well to being run in separate threads.

In the end, I settled on [GTK+](http://www.gtk.org/). The default Mac version
runs in X Windows and is fairly ugly, but it exposes all its widgets cleanly so
I can poke them and assert things about them from the end-to-end tests.

### Testing

I'm using [Cucumber](http://cukes.info/) for end-to-end/acceptance tests, and
[RSpec](http://rspec.info/) for unit tests.

To test the UI, I'm just calling methods directly on the main Gtk::Window
object (which still runs as normal and can be seen on the screen as the tests
run).
