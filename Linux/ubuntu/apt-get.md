# apt-get

### 什么是apt-get？

Ubuntu源自[Debian Linux](https://www.debian.org/)。Debian使用[dpkg打包系统](https://wiki.debian.org/DebianPackageManagement)。包装系统是一种为安装提供程序和应用程序的方法。这样，您就不必从源代码构建程序。

[APT](https://wiki.debian.org/Apt)（高级软件包工具）是与此打包系统交互的命令行工具。已经有[dpkg](http://man.linuxde.net/dpkg)命令来管理它。但apt更适合处理包装。您可以使用它来查找和安装新软件包，升级软件包，清理软件包等。

它有两个主要工具：apt-get和apt-cache。apt-get用于安装，升级和清理包，而apt-cache用于查找新包。我们将在本指南后面的示例中看到所有这些命令。

我在本教程中使用Linux Mint 18，但您可以使用任何其他基于Ubuntu的Linux发行版，例如基本操作系统，Linux Lite等。

建议阅读 apt和apt-get之间的差异解释

## 使用apt-get命令

让我们首先从apt-get命令开始。你无法逃避这个命令。最好了解这些命令，以便以更好的方式处理Linux系统。

### 使用apt-get更新包数据库

apt-get基本上适用于可用包的数据库。如果不更新此数据库，系统将不知道是否有更新的软件包可用。实际上，这是在全新安装后需要在任何Linux系统中运行的第一个命令。

更新包数据库需要超级用户权限，因此您需要使用[sudo](http://man.linuxde.net/sudo)。

```
sudo apt-get update
```

运行此命令时，您将看到从各种服务器检索的信息。

[![apt-get update命令](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-01.jpg?resize=799%2C396&ssl=1)](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-01.jpg?ssl=1)

你会在这里看到三种类型的线，hit，get和ign。让我向你解释一下：

- - 点击：包版本没有变化

- - ign：包被忽略了。可能有各种原因。这个包太新了以至于它甚至都懒得检查，或者检索文件时出错，但错误是微不足道的，因此它被忽略了。这不是错误。没有必要担心。

- get：有一个新版本可用。它将下载信息（而不是包本身）。您可以在上面的屏幕截图中看到有“get”行的下载信息。

### 使用apt-get升级已安装的软件包

更新软件包数据库后，可以升级已安装的软件包。最方便的方法是升级所有可用更新的软件包。您可以使用以下命令来实现此目的：

```
sudo apt-get upgrade
```

[![apt-get upgrade命令](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-12.jpg?resize=799%2C396&ssl=1)](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-12.jpg?ssl=1)

要仅升级特定程序，请使用以下命令：

```
sudo apt-get upgrade <package_name>
```

还有另一种方法可以使用以下命令提供完整的升级：

```
sudo apt-get dist-upgrade
```

这实际上是查找新版本的依赖项并尝试安装它。但你应该避免使用它。我将在下一节中解释它。

#### 升级和dist-upgrade之间的区别

命令apt-get upgrade非常听话。它永远不会尝试删除任何包或尝试自己安装新包。

另一方面，命令apt-get dist-upgrade是主动的。它会查找正在安装的较新版本软件包的依赖项，并尝试安装新软件包或自行删除现有软件包。

听起来像dist-upgrade更强大，更聪明，不是吗？但它存在风险。

看，它有一个“智能”冲突解决系统。有了它，它将尝试升级最重要的包，而不是那些不太重要的包。这可能会导致您删除一些您可能不想要的包。这是在生产机器上应该避免dist-upgrade的主要原因。

#### apt-get update和apt-get升级有什么区别？

这是一个非常普遍的混乱。您不是唯一一个被术语更新和升级混淆的人。

虽然听起来像是在进行apt-get更新时，但它会更新软件包。但事实并非如此。apt-get update仅更新包的数据库。例如，如果安装了XYX软件包版本1.3，则在apt-get update之后，数据库将知道有更新的版本1.4可用。

当您在apt-get update之后进行apt-get升级时，它会将已安装的软件包升级（或更新，无论您喜欢哪个术语）到新版本。

这就是为什么更新Ubuntu的最快和最方便的方法是使用此命令：

```
sudo apt-get update && sudo apt-get upgrade -y
```

建议阅读 在Ubuntu和其他Linux发行版中使用Snap包的完整指南

### 使用apt-cache命令搜索包

我会跟你说实话。这不是我搜索包的首选方式。但是当你在寻找一些特定的lib时，这非常方便。

您需要做的就是使用以下命令。你甚至不需要sudo。

```
apt-cache search <search term>
```

[![在Linux的命令行中使用容易搜索包](https://i2.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-05.jpg?resize=658%2C413&ssl=1)](https://i2.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-05.jpg?ssl=1)

您无需知道包的确切名称。它会搜索包名称及其简短描述，并根据该结果显示结果。

如果您只想搜索具有特定包名称的包，可以使用以下命令：

```
apt-cache pkgnames <search_term>
```

这将为您提供以搜索词开头的所有包的列表。

[![Linux的命令行中的可用包详细信息](https://i2.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-03.jpg?resize=658%2C222&ssl=1)](https://i2.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-03.jpg?ssl=1)

一旦知道确切的包名，就可以使用以下命令获取有关它的更多信息，例如版本，依赖关系等：

```
apt-cache showpkg <package_name>
```

[![apt-get的命令安装包](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-02.jpg?resize=658%2C413&ssl=1)](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-02.jpg?ssl=1)

### 如何使用apt-get安装新软件包

如果您知道包的名称，可以使用以下命令轻松安装它：

```
sudo apt-get install <package_name>
```

只需将<package_name>替换为所需的包。假设我想安装Pinta图像编辑器，我需要做的就是使用以下命令：

```
sudo apt-get install pinta
```

这个命令的好处是它有自动完成功能。因此，如果您不确定确切的包名称，可以键入几个字母并按Tab键，它会建议所有包含这些字母的包。例如：

[![在命令行的Linux中安装包](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-10.jpg?resize=799%2C220&ssl=1)](https://i0.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-10.jpg?ssl=1)

#### 如何安装多个包

您不限于一次只安装一个包。您可以通过提供名称一次安装多个包：

```
sudo apt-get install <package_1> <package_2> <package_3>
```

#### 

#### [![在Linux的中安装软件包](https://i1.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-11.jpg?resize=799%2C396&ssl=1)](https://i1.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-11.jpg?ssl=1)

#### 如果在已安装的软件包上运行install，该怎么办？

假设您已经安装了一个软件包，但是您已经为已安装的软件包使用了install命令。这实际上会查看数据库，如果找到更新的版本，它会将已安装的软件包升级到更新的软件包。因此，除非您不希望升级，否则使用此命令不会造成任何损害。

#### 如何在不升级的情况下安装包

假设由于某种原因你想要安装一个软件包但是如果已经安装了它就不想升级它。听起来很奇怪，但你可能有理由这样做。

对于这种情况，您可以按以下方式使用sub -no-upgrade：

```
sudo apt-get install <package_name> --no-upgrade
```

#### [![没有升级包的Linux](https://i1.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-09.jpg?resize=799%2C206&ssl=1)](https://i1.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-09.jpg?ssl=1)

#### 如何只升级包，而不是安装它

如果您只想升级包但不想安装它（如果尚未安装），则可以使用以下命令执行此操作：

```
sudo apt-get install <package_name> --only-upgrade
```

#### [![仅使用apt-get Linux升级软件包](https://i1.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-07.jpg?resize=658%2C237&ssl=1)](https://i1.wp.com/itsfoss.com/wp-content/uploads/2016/08/Using-apt-get-commands-linux-07.jpg?ssl=1)

#### 如何安装特定版本的应用程序

默认情况下，将为任何应用程序安装存储库中可用的最新版本。但由于某些原因，如果您不想安装最新版本，则可以指定版本号（您需要知道要安装的确切版本号）。

您需要做的就是添加带有包名称的= version。

```
sudo apt-get install <package_name>=<version_number>
```

### 如何使用apt-get删除已安装的软件包

这不是你只能用apt-get安装软件包。您也可以使用它删除包。您需要做的就是以这种方式使用命令：

```
sudo apt-get remove <package_name>
```

自动完成也适用于此处。所以你只需要开始输入包名称并按Tab键，它将建议所有已安装的包以这些字母开头。

卸载软件包的另一种方法是使用清除。该命令以下列方式使用：

```
sudo apt-get purge <package_name>
```

#### apt-get remove和apt-get purge有什么区别？

- apt-get remove只删除包的二进制文件。它不会触及配置文件
- apt-get purge删除与包相关的所有内容，包括配置文件

因此，如果您“删除”特定软件并再次安装，您的系统将具有相同的配置文件。当然，再次安装时，系统会要求您覆盖现有的配置文件。

当你搞砸了程序的配置时，清除特别有用。您希望从系统中完全擦除其痕迹，并且可能重新开始。

大多数情况下，简单删除对于卸载软件包来说已经足够了。

### 如何使用apt-get清理系统

哦，是的！您还可以使用apt-get清理系统并释放一些磁盘空间。

您可以使用以下命令清除检索到的包文件的本地存储库：

```
sudo apt-get clean
```

另一种方法是使用autoclean。与上面的clean命令不同，autoclean只删除那些现在有更新版本的检索包文件，它们将不再使用。

```
sudo apt-get autoclean
```

另一种释放磁盘空间的方法是使用autoremove。它会删除自动安装的lib和软件包，以满足已安装软件包的依赖关系。如果删除了包，则这些自动安装的包在系统中是无用的。此命令删除此类包。

```
sudo apt-get autoremove
```

这是清理Linux系统的命令行方式。如果您更喜欢GUI，这里有一些[Linux的CCleaner替代品](https://itsfoss.com/ccleaner-alternatives-ubuntu-linux/)，您可以在基于Ubuntu和Ubuntu的Linux发行版上使用它们。

 