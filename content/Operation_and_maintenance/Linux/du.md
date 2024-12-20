---
title: Linux_cmd_du
draft: true
---

# linux 查看当前目录下每个文件夹的占用空间

在Linux中，你可以使用几个不同的命令来查看当前目录下每个文件夹的占用空间。以下是一些常用的方法：

1. **使用`du`命令**：
   `du`（disk usage）命令用于查看文件和目录占用的磁盘空间。使用`-h`选项可以以易读的格式显示结果，`--max-depth=1`限制输出到当前目录的直接子目录。

   ```sh
   du -h --max-depth=1
   ```

2. **使用`ncdu`命令**：
   `ncdu`（NCurses Disk Usage）是一个基于文本的用户界面工具，用于查看磁盘空间使用情况。它提供了一个交互式界面来浏览文件和目录。

   ```sh
   ncdu .
   ```

3. **使用`tree`命令**：
   `tree`命令以树状图的形式显示目录的内容。使用`-a`选项显示所有文件和目录，包括隐藏文件。

   ```sh
   tree -a
   ```

4. **使用`find`命令**：
   `find`命令可以用来查找并显示当前目录下所有目录的名称和大小。

   ```sh
   find . -type d -exec du -sh {} +
   ```

5. **使用`ls`命令**：
   `ls`命令列出目录内容，与`-l`和`-s`选项结合使用，可以显示每个文件和目录的大小。

   ```sh
   ls -lS
   ```

6. **使用`gdu`命令**：
   `gdu`（图形化磁盘使用情况）是一个图形化工具，类似于`ncdu`，但它使用图形界面。

   ```sh
   gdu .
   ```

请注意，某些命令可能需要安装额外的软件包。例如，`ncdu`和`gdu`可能不在基础Linux发行版中预装，你可以使用包管理器安装它们。

在使用这些命令时，确保你有足够的权限来访问你想要检查的目录。如果你遇到权限问题，可能需要使用`sudo`来运行命令。此外，这些命令可能需要一些时间来计算大型目录的大小，具体取决于磁盘的大小和文件数量。






# linux 查看当前目录下每个文件夹的文件数量

在Linux中，要查看当前目录下每个子文件夹的文件数量，你可以使用`find`命令结合管道和`wc`（word count）命令。以下是一些方法来实现这个目的：

1. **使用`find`和`wc`命令**：
   这个命令组合会列出当前目录下每个文件夹的文件数量。

   ```sh
   find . -type f | wc -l
   ```

   这里`find . -type f`会找到当前目录及子目录下的所有文件（不包括目录），然后通过管道传递给`wc -l`来计数行数，即文件数量。

2. **使用`for`循环和`find`命令**：
   如果你想要分别查看每个子目录的文件数量，可以使用以下命令：

   ```sh
   for dir in */; do
     if [ -d "$dir" ]; then
       echo "$dir has $( find "$dir" -type f | wc -l ) files."
     fi
   done
   ```

   这个脚本片段会遍历当前目录下每个以`/`结尾的项（即每个文件夹），然后使用`find`命令计算每个文件夹中的文件数量。

3. **使用`du`和`sort`命令**：
   虽然`du`主要用于显示磁盘空间使用情况，但你可以通过以下方式使用它来查看每个文件夹中的文件数量：

   ```sh
   du --inodes -S | sort -rh
   ```

   这个命令会显示每个文件和目录的inode使用情况，`-S`选项表示不包括子目录的统计。然后通过`sort -rh`按人类可读格式（如KB、MB）降序排序。

4. **使用`tree`命令**：
   `tree`命令以树状图的形式显示目录内容，包括文件数量。

   ```sh
   tree -a
   ```

   `-a`选项表示显示所有文件和目录，包括隐藏文件。

请注意，某些命令可能需要安装额外的软件包。例如，`tree`和`ncdu`可能不在基础Linux发行版中预装。你可以使用包管理器安装它们。

在使用这些命令时，确保你有足够的权限来访问你想要检查的目录。如果你遇到权限问题，可能需要使用`sudo`来运行命令。此外，这些命令可能需要一些时间来计算大型目录的文件数量，具体取决于磁盘的大小和文件数量。
