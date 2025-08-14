# Generic heatmap plotting

Overview
--------
This Python script processes tabular data from multiple Excel files in a folder, generates hierarchical-clustered heatmaps for each file, and saves both the heatmaps and the ordered list of row labels.
It is designed for datasets where the first two columns contain identifiers (e.g., IDs and gene names) followed by numerical measurements.

Features
--------
- Processes all Excel files in a given folder
- Uses hierarchical clustering for rows (optional dendrogram)
- Truncates long names for better display
- Dynamically adjusts figure size based on dataset dimensions
- Clips numerical values to a fixed range for consistent coloring
- Saves:
  - Heatmap as PNG and PDF
  - Ordered labels after clustering as a separate Excel file

Dependencies
------------
Install the required packages with:
    pip install pandas seaborn matplotlib numpy scipy openpyxl

Usage
-----
1. Set your input and output folders in the script:
   - input_folder — Folder containing .xlsx files
   - output_folder — Folder where heatmaps and label files will be saved

2. Prepare your Excel files:
   - First two columns: unique identifier + descriptive name
   - Next columns: numeric values for heatmap

3. Run the script:
    python heatmap_script.py

4. Output:
   - <file_basename>.png and <file_basename>.pdf heatmaps
   - <file_basename>_ordered_labels.xlsx with clustered row order

Customization
-------------
- Color map: Change cmap='OrRd' to any seaborn/matplotlib colormap
- Clipping range: Modify vmin and vmax in sns.clustermap
- Clustering:
  - row_cluster=True enables row clustering
  - col_cluster=False disables column clustering
- Font sizes: Adjust in:
    plt.setp(clustergrid.ax_heatmap.yaxis.get_majorticklabels(), fontsize=8)
    plt.setp(clustergrid.ax_heatmap.xaxis.get_majorticklabels(), fontsize=7)
- Figure size scaling is automatically calculated from the number of rows and columns but can be overridden by editing height and adjusted_width

Example Workflow
----------------
If your input_folder contains:
    sample1.xlsx
    sample2.xlsx

and you run the script with:
    input_folder = "path/to/excel_files"
    output_folder = "path/to/output_heatmaps"

It will produce:
    output_heatmaps/sample1.png
    output_heatmaps/sample1.pdf
    output_heatmaps/sample1_ordered_labels.xlsx
    output_heatmaps/sample2.png
    output_heatmaps/sample2.pdf
    output_heatmaps/sample2_ordered_labels.xlsx
