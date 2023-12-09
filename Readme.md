Shortcirtcuit-xt compile the dirty/wrong way, don´t try this at home, seriously!:
Pre requirements:
cd
sudo apt install -y build-essential libcairo-dev libxkbcommon-x11-dev libxkbcommon-dev libxcb-cursor-dev libxcb-keysyms1-dev libxcb-util-dev libxrandr-dev libxinerama-dev libxcursor-dev libasound2-dev libjack-jackd2-dev libwebkit2gtk-4.0-37 libwebkit2gtk-4.0-dev libcurl4-openssl-dev 
#Compile CMAKE
VER=3.28.0
wget -c https://github.com/Kitware/CMake/releases/download/v${VER}/cmake-${VER}.tar.gz
tar -xf cmake*.tar.gz
cd cmake*/
./bootstrap
gmake
sudo make install

#Get Shortcircuit-xt code:
git clone https://github.com/surge-synthesizer/shortcircuit-xt.git
cd shortcircuit-xt
cmake -Bignore/build -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS="-O2 -march=native -mtune=native"
#Edit the generated files to delete -march=nehalem, this is dirty, but works from the ignorance:
nano ignore/build/src/CMakeFiles/scxt-core.dir/flags.make
nano ignore/build/src-ui/CMakeFiles/scxt-ui.dir/flags.make
nano ignore/build/clients/juce-plugin/CMakeFiles/scxt_plugin_CLAP.dir/flags.make
nano ignore/build/clients/juce-plugin/CMakeFiles/scxt_plugin.dir/flags.make
nano ignore/build/clients/juce-plugin/CMakeFiles/scxt_plugin_Standalone.dir/flags.make
nano ignore/build/clients/juce-plugin/CMakeFiles/scxt_plugin_VST3.dir/flags.make
#Obviously save every change:
cmake --build ignore/build --config Release --target scxt_plugin_All

The compiled will be in:
ignore/build/clients/juce-plugin

CLAP  is empty. Only VST3 and Standalone. I zipped and leave in this repo but you need to have the install part anyway, but dont need to compile cmake, only work on Pi 4b 4gb or Pi 400.
