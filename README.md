# UCalgary Racing Firmware

[What is a "monorepo"?](https://monorepo.tools/#what-is-a-monorepo)

http://wiki.ucalgaryracing.ca/books/electrical-ICh/page/setting-up-for-development-2025

## Organization
```
ucr-firmware-monorepo/
├─── applications/          <-- Top-level code and build config files that generate a binary
│    ├── front_controller/
│    │    ├── inc/
│    │    │    └── ...
│    │    ├── src/
│    │    │    ├── main.c
│    │    │    └── ...
│    │    ├── CMakeLists.txt
│    │    └── ...
│    ├── rear_controller/
│    │    └── ...
│    └── ...
├─── components/            <-- Code that abstracts a certain function (ie drivers), is pulled into applications
│    └── ...
├─── documentation/         <-- Any documentation aside from README files
│    └── ...
├─── external/              <-- Code not developed by UCR (see notes below on 'external')
│    └── ...
├─── manifest/
│    └── west.yml           <-- west manifest (see notes below on 'Developing with Zephyr')
└─── ...
```

## `external` Folder
Ideally external code in this folder should be version-controlled via either git submodules or west (see notes below on 'Developing with Zephyr'). But sometimes this is not possible (closed-source code available as a .zip, etc), so it's ok to just upload a folder here as long as it's organized properly.

## Notes on west/Zephyr
Using Zephyr without using it's 'west' tool is a massive pain. west is a 'multi-tool' that performs a number of utility functions for developing with Zephyr, one of them is dependancy management and version control. For Zephyr development, this monorepo becomes a "west workspace", with `ucr-firmware-monorepo/` being the "topdir", and the `manifest` folder being the "manifest repo", which is actually not a repo itself but is tracked through our monorepo. the `west.yml` file tells west what dependencies we have (ie Zephyr and it's modules), and where to keep them (ie within the 'external' folder).

## Building
Details to come, there are many pitfalls/caveats with how to use CMake in combination with STM32CubeMX-generated CMake files, Zephyr, integration with CMake-Tools VSCode extension, building multiple applications at one vs individually, etc
