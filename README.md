Heroku buildpack: Mono
======================

Consider this a work in-progress / hack.

Building via Vulcan
-------------------
1) Download mono tarball and extract into buildpack-mono/mono-2.10.2
http://www.mono-project.com/Compiling_Mono_From_Tarball

2) Tarzip source
cd mono-2.10.2 && tar czvf mono-src.tgz .

2) Issue vulcan build
vulcan build -s mono-src.tgz -p /tmp/mono210 -c "./autogen.sh --with-moonlight=no --enable-nls=no --prefix=/tmp/mono210 && ./configure --with-moonlight=no --enable-nls=no --prefix=/tmp/mono210 && make && make install"
vulcan build -s ./mono-2.10.2 -p /tmp/mono210 -c "./autogen.sh --with-moonlight=no --enable-nls=no --prefix=/tmp/mono210 && ./configure --with-moonlight=no --enable-nls=no --prefix=/tmp/mono210 && make && make install"

3) This will throw a 503 error, however the build is added to the database. As such, need to rebuild with the correct ID.



Usage
-----
    $ heroku create --stack cedar --buildpack http://github.com/BenHall/heroku-buildpack-mono
