# Competitive Programming Toolkit

This repository is a small toolkit for competitive programming setup work, not a repo for storing solved problems.

Its main purpose is:

- storing reusable C++ data structures and snippets in [`lib.cpp`](/D:/RYAN/programming/Competitive/lib.cpp)
- keeping the base C++ template in [`A.cpp`](/D:/RYAN/programming/Competitive/A.cpp)
- providing a helper script in [`script.py`](/D:/RYAN/programming/Competitive/script.py) to generate contest files and run local tests

## What the script does

The script supports three main workflows:

- create contest files such as `A.cpp`, `B.cpp`, `C.cpp`, ...
- generate Java files as `A.java`, `B.java`, `C.java`, ...
- compile and grade files against local test cases

The batch wrapper [`competitive.bat`](/D:/RYAN/programming/Competitive/competitive.bat) simply forwards all arguments to `script.py`.

## Requirements

- Windows
- Python available as `python`
- MinGW g++ available at `C:/msys64/mingw64/bin/g++.exe`
- Optional: `javac` and `java` in `PATH` if you want Java support

If your compiler path is different, update `GPP` near the top of [`script.py`](/D:/RYAN/programming/Competitive/script.py).

## Commands

You can call the script directly:

```powershell
python script.py <command> ...
```

Or use the batch wrapper:

```powershell
competitive <command> ...
```

### Create files

Create C++ files in a target directory:

```powershell
competitive create contest 4
```

This creates:

- `contest/A.cpp`
- `contest/B.cpp`
- `contest/C.cpp`
- `contest/D.cpp`
- `contest/include/`
- `contest/compile_commands.json`

Create Java files:

```powershell
competitive create contest 4 --lang java
```

Create both C++ and Java files:

```powershell
competitive create contest 4 --lang both
```

Default language is `cpp`.

### Grade all files in the current directory

Run this from inside a contest folder:

```powershell
competitive grade
```

This will:

- scan the current directory for `.cpp` and `.java` files
- compile each file
- match `A` to the first test, `B` to the second test, and so on
- compare output with expected output

### Test one file

Run this from inside a contest folder:

```powershell
competitive testone A.cpp
```

You can also test Java files:

```powershell
competitive testone B.java
```

## Test layout

The script supports two test layouts.

Preferred layout:

```text
tests/
  in/
    1.txt
    2.txt
  out/
    1.txt
    2.txt
```

Fallback layout:

```text
tests/
  1.in
  1.out
  2.in
  2.out
```

For the fallback layout, output files are detected by extension:

- `.out`
- `.ans`
- `.expected`

Files are matched in alphabetical order. That means:

- `A.cpp` or `A.java` uses the first input/output pair
- `B.cpp` or `B.java` uses the second pair
- `C.cpp` or `C.java` uses the third pair

## Notes

- `A.cpp` in the repo root is the source template used when generating new C++ files.
- `lib.cpp` is a personal snippet/data-structure file and is not used automatically by the generator.
- `compile_commands.json` is generated for created C++ directories to improve editor tooling.
