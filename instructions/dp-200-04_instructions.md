﻿---
lab:
    title: '使用 Cosmos DB 构建全局分布式数据库'
    module: '模块 4:使用 Cosmos DB 建立全局分布式数据库'
---

# DP 200 - 实施数据平台解决方案
# 实验4 - 使用 Cosmos DB 构建全球分布式数据库

**预计用时**：90 分钟

**先决条件**：假设已阅读了本实验室的案例研究。假设模块 1 的内容和实验室：“适用于数据工程师的 Azure”中的内容也已完成

**实验室文件**：本实验室的文件位于 _Allfiles\Labfiles\Starter\DP-200.4_ 文件夹。

## 实验室概述

学生将能够描述和演示 Azure Cosmos DB 可为组织提供的功能。他们将能够创建 Cosmos DB 实例，并展示如何通过门户网站和 .Net 应用程序上传和查询数据。然后，他们将能够演示如何启用 Cosmos DB 数据库的全局缩放。

## 实验室目标
  
完成本实验室课程后，你将能够：

1. 创建旨在扩展的 Azure Cosmos DB 数据库
1. 在 Azure Cosmos DB 数据库中插入和查询数据
1. 使用 Azure Cosmos DB 全局分布数据
1. （可选）在 Visual Studio Code 中为 Azure Cosmos DB 构建 .NET Core 应用

## 方案
  
AdventureWorks 的开发人员和信息服务部门注意到，最近在 Azure 上发布的一项名为 Cosmos DB 的新服务可以近乎实时地提供对数据的全球规模访问。他们希望了解该服务可以提供的功能，以及该服务如何以及在什么情况下可以为 AdventureWorks 带来价值。

信息服务部门希望了解如何设置服务以及如何上传数据。开发人员希望看到可用于将数据上传到 Cosmos 的应用程序示例。两者都想了解如何满足全球规模的要求。

本实验室结束后，你将可以：

1. 创建构建为可缩放的 Azure Cosmos DB 数据库
1. 在 Azure Cosmos DB 数据库中插入和查询的数据
1. 使用 Azure Cosmos DB 全球分布数据
1. （可选）在 Visual Studio Code 中为 Azure Cosmos DB 构建 .NET Core 应用

> **重要事项**：在完成本实验室后，请记下在任何预配或配置任务中遇到的任何问题，并将其记录在位于 \Labfiles\DP-200-Issues-Doc.docx__ 的文档的表格中。记录实验室编号和技术，说明问题以及解决方案的内容。保存此文档，以便在稍后模块中回头参阅。

## 练习 1：创建按比例构建的 Azure Cosmos DB 数据库

预计用时：10 分钟

个人练习
  
本练习的主要任务如下：

1. 创建 Azure Cosmos DB 实例

### 任务 1：创建 Azure Cosmos DB 实例

1. 在 Azure 门户中，如有必要，请单击 **“主页”** 超链接。

1. 导航到 **“+ 创建资源”** 图标。

1. 在新的屏幕中，导航到 **“搜索应用商店”** 文本框，然后输入 **Cosmos** 一词。在显示的列表中单击 **“Azure Cosmos DB”**。

1. 在 **“Azure Cosmos DB”** 屏幕中，单击 **“创建”**。

1. 在 **创建 Azure Cosmos DB 帐户** 屏幕中，使用以下设置创建 Azure Cosmos DB 帐户：

    - 在屏幕的“项目详细信息”中，输入以下信息
    
        - **订阅**：你在本实验室使用的订阅名称

        - **资源组**： **awrgstudxx**，其中 **xx** 是你的姓名缩写

    - 在屏幕的实例详细信息中，键入以下信息

        - **帐户名**： **awcdbstudxx**，其中 **xx** 是你的首字母缩写。

        - **API**：**Core(SQL)**

        - **Apache Spark**：**无**

        - **“位置”**：最靠近实验室位置的 Azure 区域名称，在其中你能预配 Azure VM。

        - 将其余选项保留为默认设置

            ![在 Azure 门户中创建 Azure Cosmos DB](Linked_Image_Files/M04-E01-T01-img01.png)

1. 在 **“创建 Azure Cosmos DB 帐户”** 边栏选项卡中，单击 **“查看+创建”**。

1. 验证 **“创建 Azure Cosmos DB 帐户”** 边栏选项卡后，单击 **“创建”**。

   > **备注**：预配大约需要 5 分钟。在这些实验室中，在 Azure 中预配任何服务时通常避免对其他选项卡进行说明。你可能会注意到，在预配屏幕中存在“网络”、“标记”或“高级”等其他标签页。这使你可以为服务定义任何自定义设置。例如，许多服务的网络标签页让你可以定义虚拟网络的配置，以便能够针对给定的数据服务控制和保护网络流量。“标记”选项是名称/值对，使你可以通过将相同标记应用于多个资源和资源组对资源进行分类并查看合并的账单。高级选项卡将根据具有高级选项卡的服务的不同而有所不同。但务必注意：你能够控制这些区域，并需要与网络管理员或财务部门协作，以了解应如何配置这些选项。

1. 预配完成后，将显示“你的部署已完成”屏幕，单击 **“转到资源”** 并进入下一个练习。 

>**结果** 在本练习中，你已配置 Azure Cosmos DB 帐户

## 练习 2：在 Azure Cosmos DB 数据库中插入和查询数据
  
预计用时：20 分钟

个人练习
  
本练习的主要任务如下：

1. 设置 Azure Cosmos DB 数据库和集合

1. 使用门户添加数据

1. 在 Azure 门户中运行查询

1. 对数据运行复杂的操作

### 任务 1：设置 Azure Cosmos DB 数据库和集合

1. 在 Azure 门户中，Cosmos DB 部署完成后，单击 **“转到资源”** 按钮。

1. 在 Cosmos DB 屏幕中，单击 **“视图”** 按钮。

1. 在 **“awcdbstudxx”** 屏幕中，单击 **“+ 添加容器”**。使用 **“添加容器”** 边栏选项卡，打开 **“awcdbstudxx 数据资源管理器”** 屏幕。

1. 在 **“添加容器”** 边栏选项卡中，创建一个产品数据库，其中容器名称为“Clothing”，并具有以下设置：

    - **数据库 ID**： **产品**
    
    - **吞吐量**：  **400**

    - **容器 ID**：  **服装业**

    - **分区键**： **/productId**

    - 将其余选项保留为默认值

        ![在 Azure 门户中的 Azure Cosmos DB 添加容器](Linked_Image_Files/M04-E02-T01-img01.png)

1. 在 **“添加容器”** 屏幕中，单击 **“确定”**

### 任务 2：使用门户添加数据

1. 在 **“awcdbstudcto - 数据资源管理器”** 屏幕中，在数据资源管理器工具栏上“新容器”按钮对面，单击 **“打开全屏”** 按钮。在“打开全屏”对话框中，单击 **“打开”**。在 Microsoft Edge 中打开一个新标签页。

1. 在 **SQL API** 窗格中，单击“刷新”图标，然后展开 **“产品”**， 其次是 **“服装”**，然后单击 **“项目”**。 

1. 在“文档”窗格中，单击 **“新建项目”** 图标。将出现包含现在将替换的示例 JSON 的新文档。

1. 复制以下代码并将其粘贴到 **“文档”** 选项卡：

    ```JSON
    {
       "id": "1",
       "productId": "33218896",
       "category": "Women's Clothing",
       "manufacturer": "Contoso Sport",
       "description": "Quick dry crew neck t-shirt",
       "price": "14.99",
       "shipping": {
           "weight": 1,
           "dimensions": {
           "width": 6.
           "height": 8.
           "depth": 1
          }
       }
    }
    ```

    ![使用 Azure 门户中的数据资源管理器将数据添加到 Cosmos DB 中](Linked_Image_Files/M04-E02-T02-img01.png)

1. 将 JSON 添加到“文档”选项卡后，单击 **“保存”**。

1. 在“文档”窗格中，单击 **“新建项目”** 图标。

1. 复制以下代码并将其粘贴到 **“项目”** 选项卡：

    ```JSON
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "price": "49.99",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8.
            "height": 11.
            "depth": 3
            }
        }
    }
    ```

    ![使用 Azure 门户中的数据资源管理器将数据添加到 Cosmos DB 中](Linked_Image_Files/M04-E02-T02-img02.png)

1. 将 JSON 添加到“文档”选项卡后，单击 **“保存”**。

1. 你可以通过单击左侧菜单上的每个文档来查看已保存的每个文档。第一项（ID 为 1）的值为 **33218896**，以 productid 命名，第二项的值将是 **33218897**

### 任务 3：在 Azure 门户中运行查询。

1. 在 Azure 门户的 **“项目”** 屏幕中，单击位于 **SQL API** 边栏选项卡上方的 **“新建 SQL 查询”** 按钮。

    > **注意**：出现“查询 1” 屏幕选项卡，显示查询 **SELECT * FROM c**。

1. 替换返回 JSON 文件的查询，该文件显示 productId 1 的详细信息。

    ```SQL
    SELECT *
    FROM Products p
    WHERE p.id ="1"
    ```

1. 单击 **“执行查询”** 图标。返回以下结果

    ```JSON
    [
        {
            "id": "1",
            "productId": "33218896",
            "category": "Women's Clothing",
            "manufacturer": "Contoso Sport",
            "description": "Quick dry crew neck t-shirt",
            "price": "14.99",
            "shipping": {
                "weight": 1,
                "dimensions": {
                    "width": 6.
                    "height": 8.
                    "depth": 1
                }
            },
            "_rid": "I2YsALxG+-EBAAAAAAAAAA==",
            "_self": "dbs/I2YsAA==/colls/I2YsALxG+-E=/docs/I2YsALxG+-EBAAAAAAAAAA==/",
            "_etag": "\"0000844e-0000-1a00-0000-5ca79f840000\"",
            "_attachments": "attachments/",
            "_ts": 1554489220
        }
    ]
    ```

    ![使用 Azure 门户中的数据资源管理器查询 Cosmos DB 中的数据](Linked_Image_Files/M04-E03-T02-img01.png)

1. 在现有的查询窗口中。编写可在 productId 的 JSON 文件中返回 id、制造商和说明的查询 

    ```SQL
    SELECT
        p.id,
        p.manufacturer,
        p.description
    FROM Products p
    WHERE p.id ="1"
    ```

1. 单击 **“执行查询”** 图标。返回以下结果

    ```JSON
    [
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
    ]
    ```

    ![使用 Azure 门户中的数据资源管理器查询 Cosmos DB 中的数据](Linked_Image_Files/M04-E03-T02-img02.png)

1. 在现有查询窗口中，写入可返回按价格升序排列的所有产品的价格、说明和产品 ID 的查询。

    ```SQL
    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC
    ```

1. 单击 **“执行查询”** 图标。返回以下结果

    ```JSON
    [
        {
            "price": "14.99",
            "description": "Quick dry crew neck t-shirt",
            "productId": "33218896"
        },
        {
            "price": "49.99",
            "description": "Black wool pea-coat",
            "productId": "33218897"
        }
    ]
    ```

    ![使用 Azure 门户中的数据资源管理器查询 Cosmos DB 中的数据](Linked_Image_Files/M04-E03-T02-img03.png)

### 任务 4：对数据运行复杂的操作

1. 在 Azure 门户中，在 **“项目”** 屏幕中，单击 **“新建存储过程”** 按钮。

    > **注意**：将出现显示示例存储过程的新存储过程屏幕。

1. 在“新存储流程”屏幕中，在 **“存储流程 ID”** 文本框中键入 **“createMyDocument”**。

1. 使用以下代码在存储过程主体中创建存储过程。

    ```Javascript
    function createMyDocument() {
        var context = getContext();
        var collection = context.getCollection();

        var doc = {
            "id": "3",
            "productId": "33218898",
            "description": "Contoso microfleece zip-up jacket",
            "price": "44.99"
        };

        var accepted = collection.createDocument(collection.getSelfLink(),
            doc,
            function (err, documentCreated) {
                if (err) throw new Error('Error' + err.message);
                context.getResponse().setBody(documentCreated)
            });
        if (!accepted) return;
    }
    ```

1. 在“新存储过程”屏幕中，单击 **“保存”**。

1. 在“新存储流程”屏幕中，单击 **“执行”**。

1. 在输入参数屏幕中， **“类型”** 应该设置为 **“字符串”**，并且 **“数值”** 在 **“分区键值”** 文本框中设为 **“33218898”**，然后单击 **“执行”**。

返回以下结果

    ```JSON
    {
        "id": "3",
        "productId": "33218898",
        "description": "Contoso microfleece zip-up jacket",
        "price": "44.99",
        "_rid": "I2YsALxG+-EDAAAAAAAAAA==",
        "_self": "dbs/I2YsAA==/colls/I2YsALxG+-E=/docs/I2YsALxG+-EDAAAAAAAAAA==/",
        "_etag": "\"0000874e-0000-1a00-0000-5ca7a7050000\"",
        "_attachments": "attachments/"
    }
    ```

1. 在 Azure 门户的数据资源管理器全屏中，单击下拉按钮，找到 **“新建存储过程”**，单击 **“新建 UDF”**。

    > **注意**：将出现显示 **function userDefinedFunction(){}** 的“新建 UDF 1”屏幕

1. 在 **“新定义函数”屏幕的“用户定义函数 ID”** 文本框中输入 **“producttax”**。

1. 使用以下代码在用户定义函数主体中创建用户定义函数。

    ```Javascript
    function producttax(price) {
        if (price == undefined) 
            throw 'no input';

        var amount = parseFloat(price);

        if (amount < 1000) 
            return amount * 0.1;
        else if (amount < 10000) 
            return amount * 0.2;
        else
            return amount * 0.4;
    }
    ```

1. 在“新 UDF 1”屏幕中，点击 **“保存”**。

1. 单击“查询 1”选项卡，然后使用以下查询替换现有查询：

    ```SQL
    SELECT c.id, c.productId, c.price, udf.producttax(c.price) AS producttax FROM c
    ```

1. 在“查询 1”屏幕中，单击 **“执行查询”**。

返回以下结果

    ```JSON
    [
        {
            "id": "1",
            "productId": "33218896",
            "price": "14.99",
            "producttax": 1.499
        },
        {
            "id": "2",
            "productId": "33218897",
            "price": "49.99",
            "producttax": 4.9990000000000005
        },
        {
            "id": "3",
            "productId": "33218898",
            "price": "44.99",
            "producttax": 4.4990000000000005
        }
    ]
    ```

## 练习 3：使用 Azure Cosmos DB 全局分发数据

预计用时：15 分钟

个人练习

本练习的主要任务如下：

1. 将数据复制到多个区域

1. 管理故障转移

### 任务 1：将数据复制到多个区域

1. 在 Microsoft Edge 中，单击显示有 **“awcdbstudxx - 数据资源管理器”** 的标签页。

1. 如果出现指示“连接错误”的消息，请单击 **“刷新”** 按钮。

1. 在 **“awcdbstudxx - 数据资源管理器”** 窗口的边栏选项卡中，单击 **“全局复制数据”**。

    ![在 Azure 门户中全局复制 Cosmos DB](Linked_Image_Files/M04-E03-T01-img01.png)

1. 在世界地图上，单击你所在大洲内的数据中心位置，然后单击 **“保存”**。

> **注** 预配额外的数据中心大约需要 7 分钟

### 任务 2：管理故障转移。

1. 在 **“awcdbstudxx - 全局复制数据”** 窗口中，单击 **“手动故障转移”**。

1. 点击 **“读取区域”** 数据中心位置，然后单击“我理解并同意在当前的写入区域上触发故障转移”旁边的复选框，然后单击 **“确认”**。

> **注** 手动故障转移大约需要 3 分钟。屏幕如下所示。注意图标颜色已改变

![Azure 门户中 Cosmos DB 的手动故障转移](Linked_Image_Files/M04-E03-T02-img1.png)

1. 在 **“awcdbstudxx - 全局复制数据”** 窗口中，点击 **“自动故障转移”**

1. 在“自动故障转移”屏幕中，点击 **“开启”** 按钮，然后点击 **“确认”**。

>**注**  自动故障转移的预配大约需要 3 分钟。

## 如果时间允许

> **注意**：如果你到目前为止已经完成了各实验并且还有时间，请询问讲师是否可以进行练习 4。这是针对 Cosmos DB 构建应用程序的示例。这不是 DP200 的考试要求，并且此实验室展示了可能的操作

## 练习 4：在 Visual Studio Code 中为 Azure Cosmos DB 构建 .NET Core 应用

预计用时：45 分钟

个人练习

本练习的主要任务如下：

1. 在 Visual Studio Code 中启用 Azure Cosmos DB 资源

1. 在 Visual Studio Code 中设置应用程序

1. 以编程方式创建、读取、更新和删除 NoSQL 数据

1. 使用 Azure Cosmos DB .NET Core SDK 进行查询

1. 从应用程序创建和运行存储过程

### 任务 1：在 Visual Studio Code 中启用 Azure Cosmos DB 资源

1. 打开 Visual Studio Code。

1. 在左侧菜单中，单击“扩展”按钮。

1. 在“市场”文本框的搜索扩展中，键入 **Cosmos DB** 并单击 **“Azure Cosmos DB”**。Visual Studio Code 中出现一个文档，然后单击 **“安装”**

    > **备注**：安装扩展时会出现移动条。完成后，已安装的项旁边将出现一个勾号。

1. 安装完成后，单击 **“重新加载”**。

1. 在“应用商店中搜索扩展”文本框中，输入 **“Azure 帐户”** 并单击 **“Azure 帐户扩展”**。Visual Studio Code 中出现文档，然后单击 **“安装”**

    > **注意**：安装扩展时会出现移动条。然后，一旦完成安装，即出现勾号。

1. 安装完成后，单击 **“重新加载”**。

1. 在 Visual Studio Code 中，通过单击 **“视图”**、 **“命令板”** 并输入 **“Azure：登录”** 来登录 Azure。

    > **注意**：按照 web 浏览器中的提示选择对 Visual Studio Code 会话进行身份验证的帐户。浏览器中的消息将确认你已登录。你可以关闭此标签页。

1. 在 Visual Studio Code 中，单击 Cosmos DB 下左侧菜单中的 **“Azure 图标”**，右键单击你的“订阅”，然后单击 **“创建账户”**。

1. 在 Visual Studio Code 中，会显示 **“打开文件夹”** 对话框。

1. 在你选择的位置创建名为 **learning-module** 的新文件夹，然后单击 **“选择文件夹”**。

    > **注意**：此时，Visual Studio Code 可能会在你设置工作文件夹时重新启动。因此，你必须重新打开实验文档。

1. 在 Visual Studio Code 中，单击 **“Cosmos DB”** 下左侧菜单中的 **“Azure 图标”**，右键单击你的 **“订阅”**，然后单击 **“创建帐号”**。

1. 在屏幕顶部名为 **“创建新的 Cosmos DB 帐户”** 的文本框中输入你的 Azure Cosmos DB 帐户的唯一名称 **xxcosmos**，其中 xx 是你的姓名缩写，然后按下键盘上的 **Enter**。

1. 下一步，选择 **“SQL（DocumentDB）”**，然后选择 **“awrgstudxx”** 资源组，然后选择离你最近的 **“位置”**。

    > **备注**：Visual Studio Code 底部将显示一栏，指出“正在创建 Cosmos DB 帐户…”，大约需要 5 分钟。该栏将更改为创建已成功状态。

1. 创建帐户后，在 Azure 中展开 Azure 订阅：Cosmos DB 窗格和扩展显示新的 Azure Cosmos DB 帐户。

1. 右键单击新帐户，然后单击 **“创建数据库”**。

1. 在屏幕顶部的输入板中，输入 **“用户” **作为数据库名称，然后按 **Enter**。

1. 为输入 **“WebCustomers”** 作为集合名称，然后按 **Enter**。

1. 输入分区键的 **userId**，然后按 **Enter** 键。

1. 最后，确认初始吞吐量是否为 **1000**，然后按 Enter **键**。

1. 在 Azure 中展开帐户：将显示 Cosmos DB 窗格、新的用户数据库和 WebCustomers 集合。

### 任务 2：在 Visual Studio Code 中设置应用程序

1. 单击 **“文件”** 菜单并选中 **“自动保存”** （如果未选中的话），以确保启用文件自动保存。你将复制几个代码块，这将确保你始终对文件的最新编辑进行操作。

1. 从主菜单选择 **“视图”**、 **“终端”**，然后从 Visual Studio Code 打开集成终端。

1. 单击终端窗口，按下键盘上的 **“Enter”**，然后复制并粘贴以下命令。

    ```bash
    dotnet new console
    ```

    > **注意**：此命令在你的 **“学习模块”** 文件夹中创建了“Program.cs”文件，其中已写入基本的“Hello World” 程序以及名为“learning-module.csproj”的 C# 项目文件。

1. 在终端窗口中，复制并粘贴以下命令，以运行 **“Hello World!”** 程序。

    ```bash
    dotnet run
    ```

1. 在终端提示符下，复制并粘贴以下命令块以安装所需的 NuGet 包。

    ```bash
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package System.Configuration.ConfigurationManager
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet restore
    ```

1. 终端屏幕将加载包并在 **dotnet restore** 结束时显示命令，在终端窗口按下 **Enter**。

1. 在 EXplorer 窗格的顶部，单击 **Program.cs** 打开文件。在 **使用系统** 之后添加以下使用语句。

    ```C#
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

> **重要事项**：收到有关添加所需缺失资产的消息后，单击 **“是”**，大约需要 15 秒。

1. 在 learning-module 文件夹中创建名为 **App.config** 的新文件，并添加以下代码：

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<替换为你的终结点 URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. 复制连接字符串，方法是单击左侧的 **“Azure 图标”**，展开订阅，右键单击 **“你的新 Azure Cosmos DB 帐户”**，然后单击 **“复制连接字符串”**。

1. 将连接字符串粘贴到 App.config 文件的末尾，然后从连接字符串中将 **AccountEndpoint** 部分复制到 App.config 中的 **accountEndpoint** 值。

1. 现在从连接字符串中将 **AccountKey** 值复制到 **accountKey** 值，然后 **删除你复制的原始连接字符串**。

1. 最终 App.config 文件与此类似。

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="https://my-account.documents.azure.com:443/" />
            <add key="accountKey" value="6e7sRxunccGEeO7IVlMdeFt5BdsllfSGLYc28KyjzkESiCu7tfWbTaZXAErt2v88gOcMbOYgwp1q4NYDifD7ew==" />
          </appSettings>
    </configuration>
    ```

1. 在终端提示符下，复制并粘贴以下命令以运行该程序。

    ```bash
    dotnet run
    ```

    > **注意**：该程序在终端显示 Hello World!。

1. 在 Explorer 窗格中，单击 Program.cs 以打开该文件。将以下内容添加到程序类的开始。

    ```C#
    private DocumentClient client;
    ```

1. 添加新的异步任务以创建新客户端，并通过在 Main 方法后添加以下方法来检查 Users 数据库是否存在。

    ```C#
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. 在集成终端中，再次复制并粘贴以下命令以运行程序，从而确保代码运行。“Hello World!”在控制台中返回。

    ```bash
    dotnet run
    ```

1. 将以下代码复制并粘贴至主要方法中，覆盖当前的 **Console.WriteLine("Hello World!");** 代码：

    ```C#
    try
    {
        Program p = new Program();
        p.BasicOperations().Wait();
    }
    catch (DocumentClientException de)
    {
        Exception baseException = de.GetBaseException();
        Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
    }
    catch (Exception e)
    {
        Exception baseException = e.GetBaseException();
        Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
    }
    最终
    {
        Console.WriteLine("End of demo, press any key to exit.");
        Console.ReadKey();
    }
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```bash
    数据库和集合验证完成
    演示结束，按任意键退出。
    ```

> **结果** 在本练习中，你已创建可连接到 Azure Cosmos DB 的客户端应用程序

### 任务 3：以编程方式创建、读取、更新和删除 NoSQL 数据

#### 创建文档

1. 创建一个 **“User”** 类，其表示待存储在 Azure Cosmos DB 中的对象。我们也将创建在 **“User”** 中使用的 **“OrderHistory”** 类和 **“ShippingPreference”** 类。注：文档必须具有在 JSON 中被序列化为 id 的 Id 属性。

1. 为了创建这些类，请将以下 **“User”**、 **“OrderHistory”**、 **“ShippingPreference”** 和 **“CouponsUsed”** 类复制并粘贴到 **“BasicOperations”** 方法下。

    ```C#
    public class User
    {
        [JsonProperty("id")]
        public string Id { get; set; }
        [JsonProperty("userId")]
        public string UserId { get; set; }
        [JsonProperty("lastName")]
        public string LastName { get; set; }
        [JsonProperty("firstName")]
        public string FirstName { get; set; }
        [JsonProperty("email")]
        public string Email { get; set; }
        [JsonProperty("dividend")]
        public string Dividend { get; set; }
        [JsonProperty("OrderHistory")]
        public OrderHistory[] OrderHistory { get; set; }
        [JsonProperty("ShippingPreference")]
        public ShippingPreference[] ShippingPreference { get; set; }
        [JsonProperty("CouponsUsed")]
        public CouponsUsed[] Coupons { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class OrderHistory
    {
        public string OrderId { get; set; }
        public string DateShipped { get; set; }
        public string Total { get; set; }
    }

    public class ShippingPreference
    {
        public int Priority { get; set; }
        public string AddressLine1 { get; set; }
        public string AddressLine2 { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string ZipCode { get; set; }
        public string Country { get; set; }
    }

    public class CouponsUsed
    {
        public string CouponCode { get; set; }

    }

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```text
    数据库和集合验证完成
    演示结束，按任意键退出。
    ```

1. 现在复制并粘贴 **“CreateUserDocumentIfNotExists”** 任务到 Program.cs 文件末尾的 **“WriteToConsoleAndPromptToContinue”** 方法下。

    ```C#
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("User {0} already exists in the database", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            其它
            {
                throw;
            }
        }
    }
    ```

1. 然后，返回 **BasicOperations** 方法并将以下内容添加到该方法的末尾。

    ```C#
    User yanhe = new User
    {
        Id = "1",
        UserId = "yanhe",
        LastName = "He",
        FirstName = "Yan",
        Email = "yanhe@contoso.com",
        OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
            ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);

    User nelapin = new User
    {
        Id = "2",
        UserId = "nelapin",
        LastName = "Pindakova",
        FirstName = "Nela",
        Email = "nelapin@contoso.com",
        Dividend = "8.50",
        OrderHistory = new OrderHistory[]
        {
            new OrderHistory {
                OrderId = "1001",
                DateShipped = "08/17/2018",
                Total = "105.89"
            }
        },
            ShippingPreference = new ShippingPreference[]
        {
            new ShippingPreference {
                    Priority = 1,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            },
            new ShippingPreference {
                    Priority = 2,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            }
        },
        Coupons = new CouponsUsed[]
        {
            new CouponsUsed{
                CouponCode = "Fall2018"
            }
        }
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```text
    数据库和集合验证完成
    已创建用户 1
    按任意键继续...
    已创建用户 2
    按任意键继续...
    演示结束，按任意键退出。
    ```

#### 读取文档

1. 为了从数据库中读取文档，请复制以下代码并置于 Program.cs 文件中的 **WriteToConsoleAndPromptToContinue** 方法之后。

    ```C#
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("Read user {0}", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not read", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 将以下代码复制粘贴到 BasicOperations 方法末尾的 **await this.CreateUserDocumentIfNotExists(“Users”, “WebCustomers”, nelapin);** 行后面：

    ```C#
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```text
    数据库和集合验证完成
    用户 1 已存在于数据库中
    按任意键继续...
    用户 2 已存在于数据库中
    按任意键继续...
    读取用户 1
    按任意键继续...
    演示结束，按任意键退出。
    ```

#### 更换文档

1. 将 **ReplaceUserDocument** 方法复制并粘贴到 Program.cs 文件的 **ReadUserDocument** 方法后。

    ```C#
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) });
            this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser.LastName);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for replacement", updatedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 将以下代码复制并粘贴到 **BasicOperations** 方法末尾，在 **await this.CreateUserDocumentIfNotExists(”Users”, “WebCustomers”, nelapin);** 行后面。

    ```C#
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```text
        数据库和集合验证完成
        用户 1 已存在于数据库中
        按任意键继续......
         用户 2 已存在于数据库中
        按任意键继续...
         替换 Suh 的姓氏
        按任意键继续...
         读取用户 1
        按任意键继续...
         演示结束，按任意键退出
    ```

#### 删除文档

1. 将 **“DeleteUserDocument”** 方法复制并粘贴到 **“ReplaceUserDocument”** 方法下。

    ```C#
    private async Task DeleteUserDocument(string databaseName, string collectionName, User deletedUser)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, deletedUser.Id), new RequestOptions { PartitionKey = new PartitionKey(deletedUser.UserId) });
            Console.WriteLine("Deleted user {0}", deletedUser.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for deletion", deletedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 将以下代码复制并粘贴到 **BasicOperations** 方法末尾。

    ```C#
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```text
    数据库和集合验证完成
    用户 1 已存在于数据库中
    按任意键继续…
        用户 2 已存在于数据库中
    按任意键继续......
        已替换 Suh 的姓氏
    按任意键继续...
        读取用户 1
    按任意键继续...
        已删除用户 1
    演示结束，按任意键退出。
    ```

### 任务 4：使用 Azure Cosmos DB .NET Core SDK 进行查询

1. 以下示例显示如何使用 .NET 代码在 SQL、LINQ 或 LINQ lambda 中执行查询。复制代码并将其添加到 Program.cs 文件末尾的 **private async Task CreateUserDocumentIfNotExists** 之后。

    ```C#
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // 设置一些常见的查询选项
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1, EnableCrossPartitionQuery = true };

        // 在这里通过 LastName 查找 nelapin
        IQueryable<User> userQuery = this.client.CreateDocumentQuery<User>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(u => u.LastName == "Pindakova");

        // 此处查询是同步执行，但也可以通过 IDocumentQuery<T> 接口异步执行
        Console.WriteLine("Running LINQ query...");
        foreach (User user in userQuery)
        {
            Console.WriteLine("\tRead {0}", user);
        }

        // 现在，通过直接 SQL 执行相同的查询
        IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM User WHERE User.lastName = 'Pindakova'", queryOptions );

        Console.WriteLine("Running direct SQL query...");
        foreach (User user in userQueryInSql)
        {
                Console.WriteLine("\tRead {0}", user);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. 将以下代码复制并粘贴到 BasicOperations 方法的 **await this.DeleteUserDocument(“Users”, “WebCustomers”, yanhe);** 行前面。

    ```C#
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 会显示以下结果

    ```text
    数据库和集合验证完成
    创建用户 1
    按任意键继续...
     用户 2 已存在于数据库中
    按任意键继续...
     Suh 的姓氏已替换
    按任意键继续...
     读取用户 1
    按任意键继续...
     运行 LINQ 查询...
            读取 {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    运行直接 SQL 查询...
            读取 {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    按任意键继续...
     已删除的用户 1
    演示结束，按任意键退出。
    ```

### 任务 5：从你的应用程序创建和运行存储的流程

1. 在 Visual Studio Code 中，在 **“Azure 中： Cosmos DB”** 选项卡中，先后展开 **“Azure Cosmos 数据库帐户”**、 **用户**、 **WebCustomers**，然后右键单击 **“存储过程”**，然后单击 **“创建存储过程”**。

1. 在屏幕顶部的文本框中，输入 **UpdateOrderTotal**，然后按 Enter，为存储过程命名。

    > **注**：默认情况下，提供检索第一项的存储过程。如果未提供，则执行以下步骤：

1. 在 **“Azure: Cosmos DB”** 选项卡中，展开 **“存储过程”** 并单击 **UpdateOrderTotal**。

1. 为了从应用程序运行此默认存储过程，请将以下代码添加到 **Program.cs** 文件中，作为 **“类程序”** 后的第一个条目。

    ```C#
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
        Console.WriteLine("Stored procedure complete");
    }
    ```

1. 将以下代码复制粘贴到 BasicOperations 方法中的 await this.DeleteUserDocument("Users", "WebCustomers", yanhe); 行之前。

    ```C#
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. 在集成终端中，再次复制粘贴以下命令来运行程序，以确保其运行。

    ```bash
    dotnet run
    ```

1. 应显示以下结果

    ```text
    数据库和集合验证完成
    创建用户 1
    按任意键继续...
     用户 2 已存在于数据库中
    按任意键继续...
     替换 Suh 的姓氏
    按任意键继续...
     读取用户 1
    按任意键继续...
     Running LINQ query...
            Read {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    正在运行直接 SQL 查询...
            Read {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    按任意键继续…
     存储过程完成
    已删除的用户 1
    演示结束，按任意键退出。
   ```

> **结果** 在本练习中，你通过将 Visual Studio Code 设置为连接到 Azure Cosmos DB，从头开始构建了控制台应用程序。然后，你创建了 .Net 代码，以编程方式创建、读取、更新和删除 NoSQL 数据。然后，你添加了用于查询 Cosmos DB 的代码，并学习了如何创建编程对象（如存储过程）来处理 Cosmos DB。

