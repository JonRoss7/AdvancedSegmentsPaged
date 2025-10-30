# AdvancedSegmentsPaged

Small educational simulators demonstrating segmented + paged address translation with page replacement (FIFO / LRU). The repo contains four incremental parts (PartOne..PartFour) that add features and robustness.

## Parts
- PartOne
  - Simple segmented+paged simulator.
  - Fixes applied: missing headers, PageTable initialization, safer frame allocation.
- PartTwo
  - Page directories with safer victim selection and frame bookkeeping.
  - Fixes applied: PageDirectory use, free/evict frame handling, bounds checks.
- PartThree
  - Interactive simulator with config-file loading and stress testing.
  - Fixes applied: reordered types (PageTable before PageDirectory), initialization, improved replacement logic.
- PartFour
  - Batch processing, CSV logging, robust fault reporting and latency accounting.
  - Fixes applied: full-featured translate API, CSV stress logs, batch file processor.

## Build & run (Dev container: Ubuntu 24.04.2 LTS)
Compile each part with g++ (C++17):
- PartOne
  - g++ -std=c++17 -O2 PartOne/partOne.cpp -o partOne
  - ./partOne
- PartTwo
  - g++ -std=c++17 -O2 PartTwo/partTwo.cpp -o partTwo
  - ./partTwo
- PartThree
  - g++ -std=c++17 -O2 PartThree/partThree.cpp -o partThree
  - ./partThree
- PartFour
  - g++ -std=c++17 -O2 PartFour/memory_simulator.cpp -o memory_simulator
  - ./memory_simulator

## Usage notes
- Programs prompt for:
  - Replacement algorithm (0 = FIFO, 1 = LRU)
  - Number of physical frames, page size, number of segments, etc.
- PartThree / PartFour support:
  - Load config from `config.txt` (format below)
  - Process batch files (one logical access per line)
  - Run stress tests that produce `results.txt` or CSV logs

## File formats
- Config (space-separated): segId dirSize tableSize protFlag
  - Example: `0 4 16 1`  (segment 0, 4 dir entries, 16 pages per table, read/write)
- Batch (space-separated): seg pageDir pageNum offset access
  - Example: `0 2 5 128 1`  (write access)

## Notes
- Educational simulators only (no real swap file or page contents).
- If you want, I can add a Makefile, example config/batch files, or run a build in the container.