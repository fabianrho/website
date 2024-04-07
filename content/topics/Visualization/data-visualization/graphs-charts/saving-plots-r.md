---
title: "Plot Saving in R: Techniques and Best Practices"
description: "Explore techniques for saving R plots using ggsave from the ggplot2 package, including dynamic file naming, version control, and directory management, to improve project organization and file management."
keywords: "R, ggsave, ggplot2, plot saving, data visualization, file management, version control, directory management"
date: 11-03-2024
weight: 
author: "Matthijs ten Tije"
authorlink: "https://tilburgsciencehub.com/contributors/matthijstentije/"
aliases:
  - /ggsave
  - /ggplot2/ggsave
---

## Overview
Saving your visualizations is essential for further analysis, sharing, or completing assignments. While copying figures to the clipboard offers a quick solution, saving figures in formats like PNG, JPG, or PDF is a preferable strategy. Transitioning from temporary to permanent storage methods ensures your work remains accessible and intact over time.

This article focusses on how to efficiently save visualizations in R using just one function. We'll explore the `ggsave()` function from the `ggplot2` package, which is the best practice tool for saving your figures. The `ggsave()` function introduces easy-to-use and customizable saving capabilities by allowing users to directly specify file names, dimensions, and resolution. Beyond the basic syntax for general use, we will delve into figure file management, including time stamping and organized file management strategies within the function.


## Saving Plots with Base R
Base `R` provides a simple, device-based approach for saving plots. This method involves three main steps: 
1. Opening a graphics device.
2. Plotting your data. 
3. Closing the device to finalize the file.
   
This process ensures visualizations are stored in a desired format, like PNG, JPG, or PDF. 

### Step 1: Open a Graphics Device
To save a plot, you first need to open a graphics device corresponding to your desired file format. `R` offers a variety of functions for this purpose, allowing you to specify file names and dimensions upfront. Use one of the following commands based on your format preference:

{{% codeblock %}}

```R
# Open a Graphics Device
pdf("Your-Graph-Name.pdf", width = 8, height = 6)
png("Your-Graph-Name.png", width = 800, height = 600)
jpeg("Your-Graph-Name.jpg", width = 800, height = 600)
```
{{% /codeblock %}}

### Step 2: Generate and Print Your Plot
After opening the appropriate device, first create your plot and second print it using the `print("Your-Graph-Name")`. Printing is necessary to transfer the plot from `R` to the file associated with the graphics device.

{{% codeblock %}}

```R
# Generate and Print your Plot
plot(x = mtcars$mpg, y = mtcars$wt, main = "Miles Per Gallon vs. Weight")
```
{{% /codeblock %}}

### Step 3: Close the Graphics Device
Finalize your file by closing the graphics device. This step saves and closes the file, ensuring your plot is stored as intended:

{{% codeblock %}}
```R
dev.off()
```
{{% /codeblock %}}

### Example Case: ggplot2 Plot
Here’s an example of how to apply these steps for saving `ggplot2` graphs:

{{% codeblock %}}
```R
library(ggplot2)
library(gapminder)

# Generate plots
plot1 <- ggplot(gapminder,
                aes(x = gdpPercap, y = lifeExp)) + 
                geom_point() + 
                labs(title = "Life Expectancy vs. GDP per Capita", 
                     x = "GDP per Capita", 
                     y = "Life Expectancy")

plot2 <- ggplot(gapminder, 
                aes(x = gdpPercap, y = lifeExp, color = continent)) + 
                geom_point() + 
                labs(title = "Life Expectancy vs. GDP per Capita by Continent", 
                     x = "GDP per Capita", 
                     y = "Life Expectancy")

# Save plots to PDF, specifying dimensions
pdf("ggplot_graphs.pdf", width = 8, height = 6)
print(plot1)  # First plot
print(plot2)  # Second plot
dev.off()

# Save a plot to PNG, adjusting resolution and size
png("ggplot_graph.png", width = 800, height = 600, res = 150)
print(plot1)  # Print the plot

# Close the Graphics Device
dev.off()
```

{{% /codeblock %}}

{{% tip %}}
_Quick Tip: Why Save Plots as PDFs?_

- **Scalability**: PDFs are vector-based, meaning that you can resize plots without losing clarity.
- **Quality Preservation**: PDFs maintain sharpness, avoiding the pixelation common in raster formats like PNG or JPG, making the the preffered option for presentations and detailed analysis.

{{% /tip %}}

## Saving Plots with ggsave()
While base `R` allows you to save your plots in 3 steps. The `ggsave()` function from the `ggplot2` package is the best practice for saving your R plots. `ggsave()` allows you to save your plots with just one function. 

For small projects or instances where only a single or a few visualizations is needed, the basic syntax provided by `ggsave()` is sufficient. This simplicity allows for the quick saving of plots without the need for extensive customization, making it an ideal choice for straightforward tasks.

### Syntax and Argument Overview
`ggsave()` automatically picks the file format from the extension of the provided filename. It defaults to saving the last displayed plot, but you have the flexibility to specify which plot to save:

{{% codeblock %}}

```R
ggsave(filename, # use .extension such as .png, .pdf, .jpeg
       plot = last_plot(), 
       path = NULL, 
       width = NA, 
       height = NA, 
       units = c("in", "cm", "mm", "px"), 
       dpi = 300, 
       ...)
```
{{% /codeblock %}}

Important arguments within the function are: 
- _filename_: Name and extension of the output file, dictating the format.
  - examples: .png, .pdf, etc. 
- _plot_: The ggplot or base R object to save, defaulting to the last plot shown.
- _path_: The directory for saving the file, using the current directory if not specified.
- _width, height_: Dimensions of the output file, with an option to specify units.
- _units_: Measurement units for plot dimensions ("in", "cm", "mm", "px").
- _dpi_: Resolution for raster formats, specified as dots per inch.

{{% codeblock %}}

```R
# Generate a ggplot
mtcars_scatterplot <- ggplot(mtcars, 
               aes(x = wt, y = mpg)) + 
               geom_point() + 
               ggtitle("Fuel Efficiency of Cars")

# Save the plot as a PNG with custom dimensions, resolution, and background color
ggsave("mtcars_fuel_efficiency.png", 
       plot = mtcars_scatterplot, 
       width = 10, 
       height = 6, 
       dpi = 300, 
       units = "in", 
       bg = "white")
```

{{% /codeblock %}}

## Expanding ggsave() Functionality Beyond Basics
The usage of `ggsave()` can be extended to the integration of more sophisticated techniques for file management. For example, by nesting other `R` functions. In this section, we will discuss some practicalities involving naming conventions, dynamic file naming using time stamping, and directory management. The example cases are building on top of each other, to create a structured `ggsave()` approach for your project's visual outputs.

### File Naming and Organization
Using a structured naming convention as a habit will be helpful in both project organization and ensuring your work is easily accessible in the future. By adhering to clear naming conventions, you make your files both informative and easy to find.

#### Principles for File Naming:
- _Descriptive Naming_: Clearly articulate the plot content in filenames (e.g., scatterplot_gdp_vs_life_expectancy.pdf) rather than using non-descriptive titles like figure1.pdf.
- _Compatibility_:  Choose filenames that are searchable and compatible across different platforms. Avoid spaces, special characters, or uppercase letters. Using underscores (_) or hyphens (-), and sticking to lowercase letters helps maintain consistency across systems.

In practice, applying these principles in `ggsave()` might look like this:
{{% codeblock %}}
```R
ggsave(
       filename = "scatterplot_gdp_vs_life_expectancy.pdf", 
       plot = "your_plot_object", 
       width = 8, 
       height = 6)
```
{{% /codeblock %}}


{{% tip %}}
Adopting `snake_case` for File Naming

For R projects, particularly when working with `SQL` databases or using the `tidyverse` package, it is recommended to adopt `snake_case` for naming variables, functions, and files (e.g., scatterplot_gdp_vs_life_expectancy). This practice not only ensures readability and database compatibility but also aligns with the naming conventions of the `tidyverse` package. More general avoid using dots in names to prevent confusion in non-R environments. 

{{% /tip %}}

### Time Stamping your output with ggsave()
We can use `ggsave()` together with a timestamp in the filename to give each iteration of a graph a unique name. This creates the ability to monitor changes and progress across as a visualization gets updated over time. This can be be beneficial when an older version of a visualization needs to be referred back to.

#### Adding a Timestamp to the File Name:

`R` offers built-in functionality that returns the current date and time: `Sys.Date()` for adding a date stamp for daily versioning, and `format(Sys.time(), "%Y%m%d_%H%M%S")` for a more granular timestamp that includes the exact time of creation. 

Automating the naming process to include the timestamp can streamline your workflow. By using `paste0()` in conjunction with `ggsave()` and the `Sys.Date()` or `Sys.time()` syntax you can generate output files that include the time the file was written in their file name.

Example of implementing a timestamp in a file name with `ggsave()`:

{{% codeblock %}}
```R
# Incorporate a timestamp directly in ggsave()
ggsave(
  filename = paste0("scatterplot_gdp_vs_life_expectancy", format(Sys.Date(), "%Y-%m-%d"), ".pdf"), 
  plot = "your_plot_object", 
  width = 11, 
  height = 8)
```
{{% /codeblock %}}

### Directory Structure with ggsave()
While the visualizations are now clear, version controlled and therefore unique, saving all visualizations could create a cluttered folder or directory. Therefore, organizing your plot files into directories maintains a clean and navigable project structure. `ggsave()` facilitates this by allowing you to specify the path where the file should be saved. Moreover, with the `create.dir` argument, it can create new directories directly from the function.


#### Path Specification
Properly structuring your directories to mirror the content or analysis phase improves your workflow. Therefore, it's a good practice to organize your files into directories that reflect the content or the stage of your analysis. In `ggsave()` you can specify the `path` to the directory where you want your plot saved, categorizing your files:

For example: 

{{% codeblock %}}

```R
# Saving a plot to a specific directory
ggsave(
  filename = paste0("scatterplot_gdp_vs_life_expectancy", format(Sys.Date(), "%Y-%m-%d"), ".pdf"), 
  plot = "your_plot_object",
  path = "my_project/analysis/figures/scatterplots" 
  width = 11, 
  height = 8)
```

{{% /codeblock %}}

#### Automated Directory Handling
To further improve file management, `ggsave()` offers the capability to create directories if they don't already exist. 
This function is especially useful for ensuring that your desired file structure is adhered to without requiring manual directory setup. Specify within `ggsave()`, `create.dir = TRUE`, to utilize this feature. 

{{% codeblock %}}
```R
# Automatically creating directories if they don't exist
ggsave(
  filename = paste0("scatterplot_gdp_vs_life_expectancy", format(Sys.Date(), "%Y-%m-%d"), ".pdf"), 
  plot = "your_plot_object",
  path = "my_project/analysis/figures/scatterplots" 
  width = 11, 
  height = 8,
  create.dir = TRUE)
```
{{% /codeblock %}}

{{% summary %}}
This article covers techniques for saving R plots using the `ggsave()` function from the `ggplot2` package, covering:
- Transitioning from base R's device-based plot saving to the more versatile `ggsave()`.
- Using dynamic file naming and conventions within `ggsave()` for clear, searchable plot filenames.
- Version control with `ggsave()`, utilizing timestamps and version numbers for unique plot identification.
- Directory management, specifying paths and auto-creating directories to keep projects organized.

The article includes practical examples at each step, ready-to-use code snippets, and best practices tips, aimed at improving  project's organization and efficiency in managing visual outputs.

{{% /summary %}}
