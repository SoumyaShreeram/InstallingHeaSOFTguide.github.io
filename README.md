<h1 id="installing-heasoft-on-windows-to-run-xspec">Installing HEAsoft on Windows to run Xspec</h1>
<p>The High Energy Astrophysics software, HEAsoft, is used by researchers for the analysis of astronomical data by using the multiple packages and tools provided. The guide details the installation of the software on a windows pc. </p>
<h2 id="1-downloading-the-software">1. Downloading the software</h2>
<p>The software can be downloaded from the official HEASARC website:
    <code>https://heasarc.nasa.gov/lheasoft/download.html</code></p>
<p>a) <strong>STEP 1 - Select the type of software</strong>
    Select the <em>SOURCE CODE DISTRIBUTION</em> option by clicking on the <code>Source code</code> checkbox. It is preferable to select this option if you wish to run your own models on Xspec. It will then display the list of supported platforms and ask you to select the operating system you would be using to compile the HEAsoft code. Since the software works best on Linux distributions and Mac OS X, we will have to go for the <code>PC- Cygwin</code> option for a Windows pc. </p>
<p>   <strong>Aside:</strong> To learn more about <em>Cygwin</em>, visit this <a href="https://www.cygwin.com/">website</a>. In short, it provides a Linux-like environment required for HEAsoft to function smoothly on Windows.</p>
<p>b) <strong>STEP 2 - Download the desired packages</strong>
    Select <em><code>All</code></em> and click on <em>Submit</em>. You should notice the <em>heasoft-6.24src.tar.gz</em> file downloading in the assigned directory.</p>
<h2 id="2-setting-up-cygwin-and-the-pre-requisites-for-heasoft">2. Setting up Cygwin and the pre-requisites for HEAsoft</h2>
<p>As mentioned earlier, you will need Cygwin to run HEAsoft. </p>
<p>a) Visit the <a href="https://cygwin.com/install.html">cygwin installation website</a>, and click on  <em>Run <strong>setup-x86.exe</strong></em> for the <em><code>32-bit version of Windows</code></em>. The next step is selecting the packages during installation. </p>
<p>b) Select the following <code>packages</code> from the drop-down menu and click on the check-box:</p>
<ol>
<li><p>DEVEL: gcc-core, gcc-fortran, gcc-g++, make</p>
</li>
<li><p>INTERPRETERS: perl, python, python-devel</p>
</li>
<li><p>LIBS: libcrypt-devel, libncurses-devel, libreadline-devel, libXt-devel</p>
</li>
<li><p>X11: xinit</p>
</li>
</ol>
<p>c) The <a href="https://heasarc.gsfc.nasa.gov/lheasoft/install.html">official HEAsoft installation guide</a>  details all the pre-requisites required for installation of the software: </p>
<p>   The <strong><code>pre-requisites</code></strong> are:
   <em>Perl, X11, GNU make, C, C++, Fortran, and Perl compilers</em>. </p>
<p> All of which are obtained while downloading the packages mention in <strong>2.b)</strong> during Cygwin installation. We are finally on track to start installing the software! </p>
<h2 id="3-installation-of-heasoft">3. Installation of HEAsoft</h2>
<p>a) <strong>EXPORTING</strong></p>
<p>   Open the Cygwin terminal by going to the <em>start</em> menu and searching for <em>cygwin</em>. You will then need to make sure that the correct set of compilers are chosen by the <em>configure</em> script. You would need to <code>specify the path to the installed compilers</code> [downloaded in step <strong>2.b) 4)</strong> ] while executing the <a href="https://www.tutorialspoint.com/unix_commands/export.htm">export</a> command.</p>
<pre><code>$    <span class="hljs-keyword">export</span> CC=<span class="hljs-regexp">/usr/</span>bin/gcc

$    <span class="hljs-keyword">export</span> CXX=<span class="hljs-regexp">/usr/</span>bin/g++

$    <span class="hljs-keyword">export</span> FC=<span class="hljs-regexp">/usr/</span>bin/gfortran

$    <span class="hljs-keyword">export</span> PYTHON=<span class="hljs-regexp">/usr/</span>bin/python
</code></pre><p><em>Aside</em>: You can check if the above commands are exported by typing the following:</p>
<pre><code>$    <span class="hljs-built_in">export</span> -p 
</code></pre><p>This will show all the exported variables on the current shell.</p>
<p>b) <strong>UNZIPPING AND CONFIGURING</strong>    </p>
<p>  You will have to go to the directory in which you downloaded the <em>heasoft-6.24src.tar.gz</em> file and unzip the tar file using the command:</p>
<pre><code>$    tar -zxvf heasoft-<span class="hljs-number">6.24</span>src.tar.gz
</code></pre><p> You will now need to run the main configure script to probe the system for libraries, header files, compilers, etc., and then generate the Makefile. This can be done by typing in the following:</p>
<pre><code>$    cd heasoft-<span class="hljs-number">6.24</span>/BUILD_DIR/
$    ./configure
$    make
$    make install
</code></pre><p>The above commands could take 3+ hours to execute. If the installation is on your laptop, make sure your laptop is charged during the process. Finally, type:</p>
<pre><code>$    ./configure &gt; config.<span class="hljs-keyword">out</span> <span class="hljs-number">2</span>&gt;&amp;<span class="hljs-number">1</span> &amp; 
</code></pre><p>c) <strong>STARTING THE BUILD PROCESS</strong></p>
<p>For source code distribution, the build process must be initiated. The output is recommended to be written out in a log file. This step could also take a long time based on the computer used. You can build in the background and check what is going on in real time:</p>
<pre><code>$    make &gt; build.<span class="hljs-built_in">log</span> <span class="hljs-number">2</span>&gt;&amp;<span class="hljs-number">1</span> &amp;
$    tail -f build.<span class="hljs-built_in">log</span>
</code></pre><h2 id="4-initialization-and-setup">4. Initialization and Setup</h2>
<p>For initializing the software:</p>
<pre><code>$    export HEADAS=<span class="hljs-regexp">/path/to</span><span class="hljs-regexp">/your/installed</span><span class="hljs-regexp">/heasoft-6.24/i</span>686-pc-cygwin
$    . $HEADAS/headas-init.sh
</code></pre><p><strong>Note:</strong> The following set up of <em>alias</em> is not mandatory rather is a step to make it convinient for the user when initiating Xspec repeatedly. The last two lines of code would have to be executed everytime if the <em>alias</em> is not set. </p>
<p>To set up an <a href="https://en.wikipedia.org/wiki/Alias_(command">alias</a>, first you would need to open the ./bashr or ./cshrc file in your preferred text editor. Go to the end of the file and add the <em>alias</em>:</p>
<pre><code>$    Notepad ~/.bashrc
$    <span class="hljs-built_in">alias</span> heainit=<span class="hljs-string">". <span class="hljs-variable">$HEADAS</span>/headas-init.sh"</span>
</code></pre><p>When you log out and log back in, the <em>.bashrc</em> file would be installed. </p>
<h2 id="5-post-installation">5. Post-installation</h2>
<p>Additional problems exist with Perl modules under Cygwin. For that purpose, at the end of the installation you must go to the <em>cygwin</em> directory and run;</p>
<pre><code>$    /bin/perlrebase
</code></pre><p>Then exit the <em>cygwin</em> shell and start "ash" by opening <em>Start Menu -&gt; Run</em> and type "C:/cygwin/bin/ash". Then type into the <em>ash</em> terminal:</p>
<pre><code>$    /bin/rebaseall
</code></pre><p>Exit ash if no errors appear and go back to the Cygwin terminal. In the Cygwin terminal, type:</p>
<pre><code>$    startx
</code></pre><p>Congrats! You have now completed the installation and can run HEAsoft on your Windows computer. For further information on how to use Xspec, you can have a look at the <a href="https://heasarc.gsfc.nasa.gov/xanadu/xspec/XspecManual.pdf">manual</a>. In the new windows which opens, upon typing <em>startx</em> on the Cygwin shell; you can initiate Xspec by typing <em>heainit</em> (if <em>alias</em> has been set) followed by <em>xpsec</em>. This should get Xspec running on your computer, have fun! </p>
<p><em>Written by</em>: Soumya Shreeram, <em>Last Updated</em>: 06/08/2018</p>
