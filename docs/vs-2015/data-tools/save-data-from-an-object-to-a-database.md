---
title: 将数据从对象保存到数据库 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b122285b653b75691a78367d12344c4720792f97
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47472181"
---
# <a name="save-data-from-an-object-to-a-database"></a>将数据从对象保存到数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[将数据从对象保存到数据库](https://docs.microsoft.com/visualstudio/data-tools/save-data-from-an-object-to-a-database)。  
  
  
可以在将值从您的对象传递到 TableAdapter 的 DBDirect 方法之一将数据保存到数据库的对象中 (例如， `TableAdapter.Insert`)。 有关详细信息，请参阅[TableAdapter 概述](../data-tools/tableadapter-overview.md)。  
  
 若要保存数据的对象的集合，请循环访问对象 （例如下, 一步的循环） 的集合，并使用 TableAdapter 的 DBDirect 方法之一将每个对象的值发送到数据库。  
  
 默认情况下，可以直接对数据库运行的 TableAdapter 上创建 DBDirect 方法。 这些方法可以直接调用，并且不需要<xref:System.Data.DataSet>或<xref:System.Data.DataTable>对象来协调更改即可将更新发送到数据库。  
  
> [!NOTE]
>  在配置 TableAdapter 时，主查询必须提供足够的信息供 DBDirect 方法创建。 例如，如果 TableAdapter 查询的数据配置不具有定义的主键列的表中，它不生成 DBDirect 方法。  
  
|TableAdapter DBDirect 方法|描述|  
|----------------------------------|-----------------|  
|`TableAdapter.Insert`|将新记录添加到数据库并使您能够在各列的值作为方法参数中传递。|  
|`TableAdapter.Update`|更新现有数据库中的记录。 `Update`方法采用原始的和新列作为方法参数的值。 用于查找的原始记录的原始值和新值用于更新该记录。<br /><br /> `TableAdapter.Update`方法还用于协调回数据库的数据集的更改，通过采用<xref:System.Data.DataSet>， <xref:System.Data.DataTable>， <xref:System.Data.DataRow>，或数组<xref:System.Data.DataRow>的方法参数。|  
|`TableAdapter.Delete`|删除现有的基于原始列值作为方法参数传入数据库中的记录。|  
  
### <a name="to-save-new-records-from-an-object-to-a-database"></a>若要将新记录从对象保存到数据库  
  
-   将值传递给创建的记录`TableAdapter.Insert`方法。  
  
     下面的示例创建新的客户记录中`Customers`表中的值传递`currentCustomer`对象传递给`TableAdapter.Insert`方法。  
  
     [!code-csharp[VbRaddataSaving#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#23)]
     [!code-vb[VbRaddataSaving#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#23)]  
  
### <a name="to-update-existing-records-from-an-object-to-a-database"></a>若要更新现有记录从对象到数据库  
  
-   通过调用修改记录`TableAdapter.Update`方法，传入新值更新记录，并传入要找到的记录的原始值。  
  
    > [!NOTE]
    >  您的对象需要维护的原始值，以便将它们传递给`Update`方法。 此示例使用属性与`orig`前缀来存储原始值。  
  
     下面的示例更新中的现有记录`Customers`表中的新的和原始值传递`Customer`对象传递给`TableAdapter.Update`方法。  
  
     [!code-csharp[VbRaddataSaving#24](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#24)]
     [!code-vb[VbRaddataSaving#24](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#24)]  
  
### <a name="to-delete-existing-records-from-a-database"></a>若要从数据库中删除现有记录  
  
-   通过调用删除记录`TableAdapter.Delete`方法并传入要找到的记录的原始值。  
  
    > [!NOTE]
    >  您的对象需要维护的原始值，以便将它们传递给`Delete`方法。 此示例使用属性与`orig`前缀来存储原始值。  
  
     以下示例将删除来自`Customers`表中的原始值表示通过`Customer`对象传递给`TableAdapter.Delete`方法。  
  
     [!code-csharp[VbRaddataSaving#25](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#25)]
     [!code-vb[VbRaddataSaving#25](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#25)]  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 您必须有权执行所选的插入、 更新或删除对数据库中的表。  
  
## <a name="see-also"></a>请参阅  
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
