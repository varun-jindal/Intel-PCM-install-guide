# Intel-PCM-install-guide
### Download PCM :
```bash
git clone https://github.com/opcm/pcm.git
cd path/to/pcm_directory
make
```
### Generate doxygen API reference :
```bash
sudo apt-get install doxygen   # Install doxygen
doxygen Doxyfile               # Generate documentation
cd ./html                      # Default directory where file is created
```
Open any html file, whole document will open
### To setup tools:
```bash
sudo apt-get install msr-tools           # Install msr-tools
sudo su                                  # Become root user
echo 0 >  /proc/sys/kernal/nmi_watchdog  # Disable nmi_watchdog
modprobe msr./pcm.x 60(delay in seconds) # To check if program is working
```

### Compiling c++ programs:
We need libpcm.so dynamic library to compile c++ files. For that
```bash
cd pcm.so
make
```
In pcm.so directory, it generates libpcm.so using recipe in Makefile and probably using "c_example.c" using "dlfcn.h" library and "dlopen(), dlsym()" function.

#### Now copy the generated library back to pcm folder and export the library path to LD_LIBRARY_PATH:
```bash
cp libpcm.so ./..
export LD_LIBRARY_PATH=/home/<username>/pcm:$LD_LIBRARY_PATH
```  
Keep the code "file.cpp" in pcm directory.

### Compile using:
g++ -std=c++11 file.cpp -o output -L ./ -lpcm

### Using PCM to get stats for c++ programs:
Simply execute generated output file to get stats:
```bash
./output
```

## Everytime when new terminal session is run, one needs to
* Change to root user
* Execute modprobe msr (NMI watchdog is automatically disabled)
* export library path of “libpcm.so” // Adding to bashrc is not working, dont know why
* Then execute code


## References:
[technicalstuff.wordpress]https://technicalandstuff.wordpress.com/2015/05/15/using-intels-pcm-in-linux-and-inside-c/
[docs.it4i.cz]https://docs.it4i.cz/software/debuggers/intel-performance-counter-monitor/




