# Retina

A Max standalone application which enables custom RGB palettes for the modern Novation Launchpads. Its most notable features unlocked are top lights conversion, support for the side LED (Launchpad Pro only) and custom color palettes.

Retina can run on any Windows or macOS-based computer, and requires Max 7 to be installed. The application takes input from other  applications (such as Ableton Live) and modifies it before outputting it to the Launchpad. It’s designed to be used with Live (all editions are supported – including Lite), but it should work with any other DAW or app if it uses the Drum Rack Layout for lightshows.

## State of the project

As of today, Retina has for the most part been abandoned. Its features have been fully superseded by [the Launchpad Firmware Utility](https://fw.mat1jaczyyy.com). In addition to supporting the X and MK3, it works by directly modifying the palette stored on the Launchpad's firmware, ensuring no CPU hogging. Retina today is only really useful for MK2 users looking to get Top Lights without Max for Live.

After the release of Retina 2.1, ideas sparked that made it possible to use as Max for Live device, which would bypass additional installation procedures required to make Retina work. Several approaches to this were tried, however none worked in full, thus the the "3.0" update was never finished. You can find what's left of those in `/experimental`.

## Max for Live attempts

The first attempt used [imp.midiout](https://www.theimpersonalstereo.com/max-externals), which is a M4L external that exposes direct access to MIDI ports. This would work in Live 9 (which normally blocks SysEx - this is why we need direct access) and Live 10. This approach works perfectly on macOS, however fails miserably on Windows. Achieving direct access from M4L would require receiving another handle to the desired MIDI port from the Windows OS, which simply doesn't work even with the Novation USB driver. Windows normally only allows a MIDI port to be used with a single application. With the Novation USB driver, we can use it from as many apps as we want, but we can't open the port twice from the same application, which works on macOS.

The second attempt utilized Live 10's new SysEx functionality to output directly through Live. This approach was not intended for Live 9, but there are still several issues with this. On macOS, the SysEx output lags terribly. On Windows, there is no lag, however heavier light effects would cause other M4L devices to 'crash' and stop processing data, causing blocks in the chain and the project file slowly losing out on functionality. You can see a showcase of these issues [here](https://www.youtube.com/watch?v=Vu0NhpsgKME) (I was not aware of the Windows bug at the time of making the video).

The third attempt was only theoretical - after reaching out to Novation about the problem, they proposed implementing a private API on their driver which would allow me to directly talk with the Launchpad without a MIDI port, over a MIDI-like communication protocol. They would enable the API for the Launchpads in their driver (they already have it implemented AND working for the Circuit in [Isotonik's Circuit Editor PRO](https://isotonikstudios.com/product/circuit-editor-pro/)) and share a DLL file that accesses the API on Windows. On macOS, I would fall back to the first attempt which worked there, thus achieving full functionality across Live 9 and 10 on both OSes. However, Novation went silent on this one, and never did their part.

This is just another example of Novation promising then [going quiet and never following through](https://github.com/mat1jaczyyy/lpp-performance-cfw/pull/20). It's sad very little people know how scummy their practices are towards developers who are enthusiastic about their product and volunteering to write software for it. 
