# Test7

## Use case

One wants to use the original sources of a package (of the Stackage/Hackage repository), to modify it's files locally, and in order to investigate or contribute to improvement - without using tarball files.

Source: https://www.sw4sd.com/hasksheet/doku.php?id=toolsetup:buildingapackagelocally
See also https://github.com/JoergBrueggmann/Test6

## Procedure - without tarball files

    unpack the package that should be obtained as source code
        command:

        stack unpack random

        or command with dedicated version number:

        stack unpack random-1.2.1

        output:

        Unpacked random (from Hackage) to C:\Qsync\SwEng\GitHub\JB\SandBox\Test7\random-1.2.1\

    change the current directory
        command:

        cd random-1.2.1

    initialise the folder of the package (here `random-1.2.1`), will create file `stack.yaml`
        command:

        stack init

        output:

        Looking for .cabal or package.yaml files to use to init the project.
        Using cabal packages:
        - .\

        Selecting the best among 20 snapshots...

        * Matches https://raw.githubusercontent.com/commercialhaskell/stackage-snapshots/master/lts/18/25.yaml

        Selected resolver: https://raw.githubusercontent.com/commercialhaskell/stackage-snapshots/master/lts/18/25.yaml
        Initialising configuration using resolver: https://raw.githubusercontent.com/commercialhaskell/stackage-snapshots/master/lts/18/25.yaml
        Total number of user packages considered: 1
        Writing configuration to file: stack.yaml
        All done.

    change the current directory back to the main one
        command:

        cd ..

    to `stack.yaml` of main project, add package with relative path (here `./random-1.2.1`) to section `packages` !!!

    extract

    #   - auto-update
    #   - wai
    packages:
    - .
    - ./random-1.2.1

    # Dependency packages to be pulled from upstream that are not in the resolver.
    # These entries can reference officially published versions as well as

    to `package.yaml` of main project add dependency to package (here `random`) with constraint (here ` == 1.2.1`) to section `dependencies`
        extract

        .
        .
        .
        # common to point users to the README.md file.
        description:         Please see the README on GitHub at <https://github.com/githubuser/Test7#readme>

        dependencies:
        - base >= 4.7 && < 5
        - random == 1.2.1

        library:
          source-dirs: src
        .
        .
        .

    delete cabal-file (here `Test7.cabal`), if any

    build the main project
        command:

        stack build

        output:

        random> configure (lib)
        random> Configuring random-1.2.1...
        random> build (lib)
        random> Preprocessing library for random-1.2.1..
        random> Building library for random-1.2.1..
        random> copy/register
        random> Installing library in C:\Qsync\SwEng\GitHub\JB\SandBox\Test7\.stack-work\install\f1fb6c00\lib\x86_64-windows-ghc-8.10.7\random-1.2.1-HT6KBuAXK636deJWA2IfmN
        random> Registering library for random-1.2.1..
        Building all executables for `Test7' once. After a successful build of all of them, only specified executables will be rebuilt.
        Test7 > configure (lib + exe)
        Test7 > Configuring Test7-0.1.0.0...
        Test7 > build (lib + exe)
        Test7 > Preprocessing library for Test7-0.1.0.0..
        Test7 > Building library for Test7-0.1.0.0..
        Test7 > [1 of 2] Compiling Lib
        Test7 > [2 of 2] Compiling Paths_Test7
        Test7 > Preprocessing executable 'Test7-exe' for Test7-0.1.0.0..
        Test7 > Building executable 'Test7-exe' for Test7-0.1.0.0..
        Test7 > [1 of 2] Compiling Main
        Test7 > [2 of 2] Compiling Paths_Test7
        Test7 > Linking .stack-work\dist\274b403a\build\Test7-exe\Test7-exe.exe ...
        Test7 > copy/register
        Test7 > Installing library in C:\Qsync\SwEng\GitHub\JB\SandBox\Test7\.stack-work\install\f1fb6c00\lib\x86_64-windows-ghc-8.10.7\Test7-0.1.0.0-7rSbgHQwCYG6qywGwlMXqh
        Test7 > Installing executable Test7-exe in C:\Qsync\SwEng\GitHub\JB\SandBox\Test7\.stack-work\install\f1fb6c00\bin
        Test7 > Registering library for Test7-0.1.0.0..
        Completed 2 action(s).

