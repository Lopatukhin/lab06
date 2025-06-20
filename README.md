ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~$ export GITHUB_USERNAME=Lopatukhin
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~$ export GITHUB_EMAIL=thegoldenorder112@gmail.com
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~$ alias edit=nano
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~$ alias gsed=sed
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~$ cd ${GITHUB_USERNAME}/workspace
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace$ pushd .
~/Lopatukhin/workspace ~/Lopatukhin/workspace
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace$ source scripts/activate
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab05 projects/lab06
Cloning into 'projects/lab06'...
remote: Enumerating objects: 192, done.
remote: Counting objects: 100% (192/192), done.
remote: Compressing objects: 100% (105/105), done.
remote: Total 192 (delta 62), reused 188 (delta 61), pack-reused 0 (from 0)
Receiving objects: 100% (192/192), 1.03 MiB | 3.88 MiB/s, done.
Resolving deltas: 100% (62/62), done.
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace$ cd projects/lab06
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git remote remove origin
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab06
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
> ' CMakeLists.txt
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION\
>   \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
> ' CMakeLists.txt
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_TWEAK 0)
> ' CMakeLists.txt
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_PATCH 0)
> ' CMakeLists.txt
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_MINOR 1)
> ' CMakeLists.txt
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_MAJOR 0)
> ' CMakeLists.txt
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git diff
diff --git a/CMakeLists.txt b/CMakeLists.txt
index 0a53d1f..1300333 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -7,6 +7,13 @@ option(BUILD_EXAMPLES "Build examples" OFF)
 option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
+set(PRINT_VERSION_MAJOR 0)
+set(PRINT_VERSION_MINOR 1)
+set(PRINT_VERSION_PATCH 0)
+set(PRINT_VERSION_TWEAK 0)
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
 
 add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
 
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ touch DESCRIPTION && edit DESCRIPTION
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ touch ChangeLog.md
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ export DATE="`LANG=en_US date +'%a %b %d %Y'`"
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat > ChangeLog.md <<EOF
> * ${DATE} ${GITHUB_USERNAME} <${GITHUB_EMAIL}> 0.1.0.0
- Initial RPM release
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat > CPackConfig.cmake <<EOF
> include(InstallRequiredSystemLibraries)
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "static C++ library for printing")
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_RPM_PACKAGE_NAME "print-devel")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "print")
set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> include(CPack)
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cat >> CMakeLists.txt <<EOF
> include(CPackConfig.cmake)
EOF
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ gsed -i 's/lab05/lab06/g' README.md
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git add .
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git commit -m"added cpack config"
[master 0ba9f9b] added cpack config
 5 files changed, 32 insertions(+), 1 deletion(-)
 create mode 100644 CPackConfig.cmake
 create mode 100644 ChangeLog.md
 create mode 100644 DESCRIPTION
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git tag v0.1.0.0
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ git push origin master
Username for 'https://github.com': Lopatukhin
Password for 'https://Lopatukhin@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 2.80 KiB | 2.80 MiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Lopatukhin/lab06
   773cced..1939920  master -> master
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.4s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ilia_lopatukhin/Lopatukhin/workspace/projects/lab06/_build
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cd _build
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06/_build$ cpack -G "TGZ"
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/ilia_lopatukhin/Lopatukhin/workspace/projects/lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06/_build$ cd ..
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.10 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value.  Or, use the <min>...<max> syntax
  to tell CMake that the project requires at least <min> but has been updated
  to work with policies introduced by <max> or earlier.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/ilia_lopatukhin/Lopatukhin/workspace/projects/lab06/_build
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ cmake --build _build --target package
[100%] Built target print
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/ilia_lopatukhin/Lopatukhin/workspace/projects/lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ mkdir artifacts
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ mv _build/*.tar.gz artifacts
ilia_lopatukhin@Ilia-lopatukhin-Y3-Max:~/Lopatukhin/workspace/projects/lab06$ tree artifacts
artifacts
└── print-0.1.0.0-Linux.tar.gz

1 directory, 1 file

