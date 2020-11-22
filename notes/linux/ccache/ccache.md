Setup CCACHE at localhost
=====================


## Install CCACHE at Ubuntu/Debain
<pre><code># Install package
console> sudo apt install -y ccache

# update symbol links
console> /usr/sbin/update-ccache-symlinks

# set as the desired maximum buffer size
console> ccache -M 50G  
</code></pre>


## Modify .bashrc

<pre><code>console> vim ~/.bashrc
<pre><code> # Add following line at the end of .bashrc
 export PATH="/usr/lib/ccache:$PATH"
</code></pre></code></pre>

<pre><code># Apply change and check
console> source ~/.bashrc
console> echo $PATH
</code></pre>

## Apply to cmake Project

If your project had create make file by cmake, please remove the build directroy first, and re-camke again.

<pre><code>console> cd ${PATH_OF_YOUR_PROJECT}
console> rm -r build
console> mkdir build
console> cd build
console> cmake ../
</code></pre>

Check the working compiler is detected as /usr/lib/ccache/cc, or corresponding compiler at /usr/lib/ccache/

<pre><code>dana@Dana:/project/dana/github/libCabbage/build$ cmake ../
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
-- Check for working C compiler: /usr/lib/ccache/cc
-- Check for working C compiler: /usr/lib/ccache/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/lib/ccache/c++
-- Check for working CXX compiler: /usr/lib/ccache/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found PkgConfig: /usr/bin/pkg-config (found version "0.29.1") 
</code></pre>

Once the compiler detected correct, you could rebuild the project now.
<pre><code>console> cd ${PATH_OF_YOUR_PROJECT}
# first time make, it woul take more time for compile
console> make

# for most project, we need clear the project and rebuild again.
console> make clean

# with CCACHE, you will see the time of build is faster then first time building
console> make 
</code></pre>