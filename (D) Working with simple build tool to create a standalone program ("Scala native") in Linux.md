2025-04-12: work in progress

# (D) Working with simple build tool to create a standalone program ("Scala native") in Linux

If not yet happened, install the _clang_ compiler first. LLVM is not needed according to my tests. I used this description: https://www.cyberithub.com/how-to-install-clang-tool-on-ubuntu-or-debian-linux/ ("How to Install clang tool on Ubuntu or Debian Linux") and installed it like this:

_$ sudo apt install clang_

Then I checked version and availability:

_$ clang --version_

_Ubuntu clang version 18.1.3 (1ubuntu1)_

_Target: x86_64-pc-linux-gnu_

_Thread model: posix_

_InstalledDir: /usr/bin_

<br/>

Now open the Bash shell (Terminal) and set your working directory so that it will be **the parent directory of the later project root directory**:

_$ sbt new_  # create a new Scala project; this command also creates the project root directory

_Welcome to sbt new!_

_Here are some templates to get started:_
…

Select **option d)** with only pressing key [d] (and not pressing a following [ENTER]): _d) scala/scala3.g8 - Scala 3 seed template_

Now enter your project name (which is also the name of the project root directory in the filesystem of the OS):

_name [Scala 3 Project Template]: test_sbt_Linux_ # this is only an example project name

_Template applied in .\<project name>_

See also from this use case: https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(C)%20Working%20with%20simple%20build%20tool%20to%20run%20an%20app%20on%20the%20JVM%20in%20Windows%20with%20(3rd%20party)%20imports.md#select-option-d



(TBD)

<br/>

##_end
