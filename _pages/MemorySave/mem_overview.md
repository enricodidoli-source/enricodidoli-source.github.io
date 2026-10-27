---
layout: archive
title: "MemorySave: RAM Management in Python"
permalink: /mem_overview/
author_profile: true
---

# MemorySave: RAM Management in Python

Out Of Memory (OOM) errors are a common issue when working with large-scale data processing in Python, particularly when working within free Google Colab environments. Standard garbage collection (`gc.collect()`) often fails to instantly release memory back to the system. Even deleting variables manually (`del var`) does not always work due to persistent references, hidden duplications, or variables passed as function parameters.

**`MemorySave`** is a Python utility class created to handle RAM management efficiently by combining optimized disk serialization with cache cleaning.

---

Below you can find a quick usage example, or you can go to the repository by clicking the button below.

[View Source Code](https://github.com/enricodidoli-source/memory-save){: .btn .btn--primary}

---

## 🎯 Usage Example

Here is a practical example showing how to initialize `MemorySave`, save datasets to disk, and restore them only when needed in the execution:

```python
# 0. Clone the repository and import the class 
!pip install git+https://github.com/enricodidoli-source/memory-save.git

import pandas as pd
from memory_utils import MemorySave

# 1. Initialize MemorySave with a temporary cache directory
mem = MemorySave(base_dir="./temp_var")

# 2. Simulate large data (e.g., a list of pandas DataFrames)
df_list = [pd.DataFrame({'col': range(1000000)}) for _ in range(3)]

# 3. Save to disk (Parquet for DataFrame lists, Pickle for general objects) 
# and automatically clear RAM
mem.save_and_clear(
    variables=[df_list], 
    variables_names=["heavy_dataset"], 
    clear=True,        # Deletes variables and triggers deep RAM cleanup
    force=True         # Overwrites if heavy_dataset is already cached
)

# 4. Inspect currently cached variables
mem.show_vars()

def df_mean(df_list=None, mem=None):
    if mem:
        # 5. Reload variables into local scope only when required for computation
        (df_list,) = mem.load_variables(["heavy_dataset"])
    for df in df_list:
        print(df.mean())
    return

# 6. DO NOT pass saved heavy variables (df_list) directly to functions 
# to avoid pointer duplication and memory retention in stack frames!
df_mean(df_list=None, mem=mem)

# 7. Safely remove specific cached variables or wipe the workspace upon completion
mem.remove_var(["heavy_dataset"])
mem.close()
```

---

| Method | Parameters | Description |
| :--- | :--- | :--- |
| `save_and_clear` | `variables`: list, `variables_names`: list, `custom_dir`: str, `clear` : bool, `force`: bool | Automatically detects variable types. Saves lists of DataFrames using `.parquet` partitions for performance and generic Python objects via `.pkl`. Deletes the passed variables friom the RAM when `clear=True`. |
| `load_variables` | `variables_names`: list | Reads requested objects back from disk (`parquet` chunks or `pickle` files) and returns them as a tuple. |
| `remove_var` | `variables_names`: list | Deletes specific saved variables from disk (removing directory trees or `.pkl` files) and updates internal tracking dictionary. |
| `is_var` | `variables_names`: list | Returns a dictionary indicating whether specified variable names currently exist in the cache. |
| `show_vars` | None | Prints all currently tracked variables with their disk storage paths. |
| `add_external_path`| `external_path`: list, `var_name`: str | Allows the registration of a pre-saved external directory/file paths directly into the tracking dictionary. |
| `show_path` | None | Returns the current base directory path used for temporary variable storage. |
| `close` | None | Deletes the entire temporary workspace directory and resets tracking dictionary. |
