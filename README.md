### 1.1 Install required tools

Install a C/C++ build environment such as Microsoft Visual
Studio 2012.  Compilers supported by Oracle libraries are found in
[Oracle documentation](https://docs.oracle.com/en/database/) for each version, for example
[Oracle Database Client Quick Installation Guide 12c Release 1 (12.1) for Microsoft Windows x64 (64-Bit)](https://docs.oracle.com/database/121/NXCQI/toc.htm#NXCQI108).

Install the Python 2.7 MSI from
[www.python.org](https://www.python.org/downloads).  Select the
customization option to "Add python.exe to Path".

If you use a 32-bit Node.js, make sure to use a 32-bit Oracle client
during build and run time.  Otherwise use a 64-bit Node.js with a
64-bit Oracle client.  The instructions below use a 64-bit stack.

### 1.2 Install Node.js

Install the 64-bit Node.js  MSI (e.g. node-v0.12.7-x64.msi) from
[nodejs.org](http://nodejs.org/download/).  Make sure the option to
add the Node and npm directories to the path is selected.

### 1.3 Install the free Oracle Instant Client ZIPs

Building and running node-oracledb needs appropriate Oracle client
libraries installed first.  These libraries:

- are included in (i) Oracle database, or (ii) in the full Oracle client, or (iii) in Oracle Instant Client.  You need one of these.
- must be version 11.2 or greater
- must match the Node.js 32 or 64-bit architecture

If you need appropriate Oracle client libraries, then download the
free Instant Client **Basic** and **SDK** ZIP files from
[Oracle Technology Network](http://www.oracle.com/technetwork/topics/winx64soft-089540.html).

Extract `instantclient_basic-windows.x64-12.1.0.2.0.zip` and
`instantclient_sdk-windows.x64-12.1.0.2.0.zip` to the same directory.

Optionally rename the resulting Instant Client directory to the
default location used by the node-oracledb installer:

```
ren C:\instantclient_12_1 C:\oracle\instantclient
```

Add the directory to `PATH`.  For example on Windows 7, update `PATH` in
Control Panel -> System -> Advanced System Settings -> Advanced ->
Environment Variables -> System variables.

If you have multiple versions of Oracle libraries installed, make sure
the desired version occurs first in the path.

### 1.4 Install the add-on

Start Visual Studio and open a Developer Command Prompt within it.

Use `set PATH` in the shell to confirm the Python, Node.js and Oracle
directories are correctly set.  If they are not, then set `PATH`
manually in the shell, or set it in the System Properties panel and
restart the command shell.

Make sure the Microsoft Visual Studio environment variables are set
appropriately.  Use `set PATH` and verify it contains your Visual
Studio paths.  If they are not set, use vcvars64.bat (or vcvars.bat if
you building with 32-bit binaries) to set the environment.
Alternatively you can open the 'Developer Command Prompt for Visual
Studio' which has environment variables already configured.

Tell the installer where to locate the Oracle client libraries and
header files by setting the `OCI_LIB_DIR` and `OCI_INC_DIR` variables.

These variables are only needed during installation, not at run time.

For Instant Client use:

```
set OCI_LIB_DIR=C:\oracle\instantclient\sdk\lib\msvc
set OCI_INC_DIR=C:\oracle\instantclient\sdk\include
```

If you are installing with a local database or the full Oracle client,
then locate the Oracle directory and set the node-oracle installer
variables similar to:

```
set OCI_LIB_DIR=C:\oracle\product\12.1.0\dbhome_1\oci\lib\msvc
set OCI_INC_DIR=C:\oracle\product\12.1.0\dbhome_1\oci\include
```

Also make sure that `PATH` contains `C:\oracle\product\12.1.0\dbhome_1\bin`.

If you are behind a firewall you may need to set your proxy, for
example:

```
set http_proxy=http://my-proxy.example.com:80/
```

Install node-oracledb from the
[NPM registry](https://www.npmjs.com/package/oracledb):

```
npm install oracledb
```

### 1.5 Run an example program

Download the
[example programs](https://github.com/oracle/node-oracledb/tree/master/examples) from GitHub.

Edit `dbconfig.js` and set the database credentials to your
environment:

```
module.exports = {
  user          : "hr",
  password      : "welcome",
  connectString : "localhost/XE"
};
```

Run one of the examples:
	
```
node select1.js
```
