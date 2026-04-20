# 📊 Sorting Algorithms Comparison

A C program that benchmarks five classic sorting algorithms across different array sizes and input types, then saves the results to CSV files for analysis.

## 🧮 Algorithms

| Algorithm          | Best Case  | Average Case | Worst Case | Space    |
| ------------------ | ---------- | ------------ | ---------- | -------- |
| **Bubble Sort**    | Ω(n)       | Θ(n²)        | O(n²)      | O(1)     |
| **Selection Sort** | Ω(n²)      | Θ(n²)        | O(n²)      | O(1)     |
| **Insertion Sort** | Ω(n)       | Θ(n²)        | O(n²)      | O(1)     |
| **Quick Sort**     | Ω(n log n) | Θ(n log n)   | O(n²)      | O(log n) |
| **Merge Sort**     | Ω(n log n) | Θ(n log n)   | O(n log n) | O(n)     |

## 📁 Project Structure

```
sorting-algorithms-comparison/
├── main.c              # Entry point — runs all tests
├── include/
│   ├── config.h        # Test parameters (array sizes, number of runs)
│   ├── sorting.h       # Sorting algorithm declarations
│   ├── testing.h       # Testing & timing utility declarations
│   └── array.h         # Array utility declarations
├── src/
│   ├── sorting.c       # Sorting algorithm implementations
│   ├── testing.c       # Testing, timing, and CSV output logic
│   └── array.c         # Array generation and copy utilities
└── data/
    ├── test_array.csv              # Generated test arrays (auto-created)
    ├── sorting_runtimes.csv        # Benchmark results (auto-created)
    ├── test_array_example.csv      # Sample test array output
    └── sorting_runtimes_example.csv # Sample runtime output
```

## ⚙️ Requirements

- **C compiler**: GCC or Clang
- **Standard libraries**: `stdio.h`, `stdlib.h`, `time.h`

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/parunchxi/sorting-algorithms-comparison.git
cd sorting-algorithms-comparison
```

### 2. Configure test parameters (optional)

Edit [`include/config.h`](include/config.h) to adjust the benchmark settings:

```c
const int START_SIZE = 1;       // Smallest array size to test
const int END_SIZE   = 10000;   // Largest array size to test
const int SIZE_STEP  = 1;       // Step between sizes
const int NUM_TESTS  = 10;      // Number of random-array tests per size
const int NUM_SORTS  = 5;       // Number of timed runs per algorithm per test
```

> **Note:** The default config (`END_SIZE = 10000`, `SIZE_STEP = 1`) generates a very large dataset and may take a long time. Increase `SIZE_STEP` or reduce `END_SIZE` for a quicker run.

### 3. Compile

```bash
gcc main.c -o sorting -lm
```

### 4. Run

```bash
./sorting
```

Progress is printed to the console. Results are saved automatically to the `data/` directory.

## 📄 Output Files

Two CSV files are created inside `data/` after each run:

### `test_array.csv`

Records every input array used in testing.

| Column    | Description                                |
| --------- | ------------------------------------------ |
| `test_id` | Unique test identifier                     |
| `size`    | Number of elements                         |
| `type`    | `0` = random, `1` = sorted, `2` = reversed |
| `array`   | Space-separated array values               |

### `sorting_runtimes.csv`

Records runtime (ms) for each algorithm on each test array.

| Column                    | Description                                    |
| ------------------------- | ---------------------------------------------- |
| `test_id`                 | Matches a row in `test_array.csv`              |
| `size`                    | Array size                                     |
| `type`                    | Input type (random / sorted / reversed_sorted) |
| `algorithm`               | Algorithm name                                 |
| `runtime_1` … `runtime_5` | Individual run times in milliseconds           |
| `runtime_avg`             | Average of all runs                            |

## 🔍 How It Works

For each array size from `START_SIZE` to `END_SIZE`:

1. **10 random arrays** are generated and tested.
2. **1 sorted array** is generated and tested.
3. **1 reverse-sorted array** is generated and tested.

Each test array is run through all five algorithms. Every algorithm is timed `NUM_SORTS` times on a fresh copy of the array, and the average runtime is recorded.

## 🛠️ Customization

- **Add a new algorithm**: Declare it in `include/sorting.h`, implement it in `src/sorting.c`, then add a `get_<algorithm>_runtime()` function in `src/testing.c` and call it inside `test_sorting_algorithms()`.
- **Change input types**: Modify `generate_array()` in `src/array.c`.
- **Analyze results**: Import `data/sorting_runtimes.csv` into Python (pandas/matplotlib), R, or Excel for visualization.
