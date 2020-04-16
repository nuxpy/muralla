Name

    This project is called: muralla. As a word in Spanish that references to a wall.

Description
 
    This project is focuses in a simple model in order to make some chains on Iptables through a "json" configure file.
    
    It has a tree structure like this:
    
        /etc/muralla/muralla.conf
        /etc/network/if-up.d/muralla-up             [Debian family]
        /etc/sysconfig/network-scripts/muralla-up   [CentOS family]
        /usr/sbin/muralla
        /usr/share/man/es/man1/muralla.1.gz
        /usr/share/man/es/man5/muralla.conf.5.gz
        /usr/share/man/man1/muralla.1.gz
        /usr/share/man/man5/muralla.conf.5.gz
    
    The file /usr/sbin/muralla contains the main script to execute muralla as a program. Only a superuser can execute the program.
    
    The file /etc/muralla/muralla.conf contains the configuration structure similar a json file scheme.
    
    The rest of files are references or manuals.
    
    You can read all of the source code, there is open to make changes and improves, this is an experimental version. Missing some options, parameters, and commands of Iptables to use through muralla.

Installation

    It has a little script for the installation:
    
        ./install
    
    Ensure that the install script has execute permissions.
    
    Also your system must has python3 or higher installed and the follow python libraries:
    
        * json
        * re
        * platform

License

    muralla. Handle Iptables on an easily way.
    Copyright (C) 2019  Félix Urbina

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.

