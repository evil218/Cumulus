
Cumulus
=======================================

Cumulus is a crossplatform "rendezvous" service to assist P2P connection in RTMFP peer's communication. In RTMFP protocol, Cumulus plays the server role.
Cumulus can be used as a library to include in your "publisher" software, or be installed as a service on your server computer.

We remind you that Cumulus is licensed under the [GNU General Public License], so **CumulusLib can't be linked with any closed source project** (see [license]).

Status
------------------------------------
Cumulus is in development, we work to make it stable, but much work remains to be done. For this moment only few scenarios work.
If you are a developer **help us** to evolve and enhance Cumulus, else you can always make a **donation** ([us]|[eu]) for that we spent more time on it, in fact it's not technical skills that hinder us but lack of time.
Also with the intention to understand better the exchange between a official RTMFP server and a Flash client, we have created a [worketable] to facilitate sharing of information exchanged and its presentation.

Usage
------------------------------------

### CumulusService

CumulusService executable includes the following argument launch options, to a developement usage:

- **help**,
displays help information about command-line usage.

- **cirrus=url**,
cirrus url to activate a "man-in-the-middle" mode in bypassing flash packets to the official cirrus server of your choice.

- **dump[=file]**,
enables packet traces in the console. Optionnal *file* argument also allows a file dumping. Often used with *cirrus=url* option to observe flash/cirrus exchange.

- **middle**,
enables middle traces if dump option is activated. Otherwise it does nothing.

- **log=level**,
log level argument beetween 0 and 8 : none, fatal, critic, error, warn, note, info, debug, trace. Default value is 6 (note), all logs until info level are displayed.

Command-line way is preferred during development and test usage. To statically configure the service the better practice is a optionnal configuration file to the installation directory.
The possible configurations are:

- **port**,
equals 1935 by default (RTMFP server default port), it's the port used by CumulusService to listen incoming RTMFP requests.

- **keepAliveServer**,
time in milliseconds for periodically sending packets keep-alive with server, 15000 ms by default.

- **keepAlivePeer**,
time in milliseconds for periodically sending packets keep-alive between peers, 10000 ms by default.

The configuration file must have *CumulusService* as base name and can be a *ini*, *xml*, or *properties* file type, as you like (personnal choice of preferred style).

**CumulusService.ini**

    ;Cumulus server configurations
    port = 1985 
	keepAlivePeer = 10000
	keepAliveServer = 15000

**CumulusService.xml**

    <config>
      <port>1985</port>
	  <keepAlivePeer>10000</port>
	  <keepAliveServer>15000</port>
    </config>

**CumulusService.properties**

    # Cumulus server port
    port=1985
	keepAlivePeer=10000
	keepAliveServer=15000

If this configuration file doesn't exist, default values will be used.

### CumulusLib

CumulusService is almost a empty project, it includes just a main.cpp file which uses all CumulusLib API.
Looks its file content is still the best way to learn to play with ;-)

A brief overview:

    #include "RTMFPServer.h"

    using namespace Cumulus;
    ...
    RTMFPServer server;
    server.start();
    ...
    server.stop();
	
### Flash side

If your Cumulus instance is stared in local, Flash client can connect it by a classical NetConnection:

    _netConnection.connect("rtmfp://localhost/");

Here the port has its default value 1935. If you configure a different port on CumulusService you must indicate this port in the URL (after localhost, of course).

In "man-in-the-middle" mode (see command-line argument *cirrus* in usage part) you must indacted on side flash your Cirrus key developer.
	
	_netConnection.connect("rtmfp://localhost/KEY");
	
Of course "KEY" must be replaced by your Cirrus development key.

__notice:__ The *ipMulticastMemberUpdatesEnabled* NetGroup mode is not supporter for this moment.

Build
------------------------------------

Cumulus source code is crossplatform.

### Dependencies

Cumulus has the following dependencies:

- [OpenSSL] is required.

- [Poco] in its Basic edition is required.

### Building
**Windows**

Visual Studio 2008 file solutions and projects are included.
It seeks the external librairies in "External/lib" folder and external includes in "External/include" folder at the root project.

**Linux/Unix**

CumulusLib building manipulation are:

	make
	make install
	make uninstall
	make clean

CumulusService builds simply with:

	make

Thanks
------------------------------------
Special thanks to Key2 and Andrei of [C++ RMTP Server] who by their preliminary work has made this project possible.


[C++ RMTP Server]: [http://www.rtmpd.com] "www.rtmpd.com"
[GNU General Public License]: http://www.gnu.org/licenses/ "www.gnu.org/licenses"
[license]: https://github.com/OpenRTMFP/Cumulus/raw/master/LICENSE "LICENSE"
[OpenSSL]: http://www.openssl.org/ "www.openssl.org"
[Poco]: http://pocoproject.org/ "pocoproject.org" 
[worketable]: http://openrtmfp.github.com/Cumulus/ "Cumulus Worketable"
[us]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=M24B32EH2GV3A "Donation US"
[eu]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=QPWT9V67YWSGG "Donation EU"
        

















