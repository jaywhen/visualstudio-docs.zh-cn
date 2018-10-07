---
title: CvIsEnabled 函数 | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cvmarkers/CvIsEnabledEx
- cvmarkers/CvIsEnabled
helpviewer_keywords:
- CvIsEnabled method
- CvIsEnabledEx method
ms.assetid: 2e4fea6d-758d-4150-8744-6102a1d58c1c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0919e8792743c7d1d953faad88ae6e8385b03993
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "47472453"
---
# <a name="cvisenabled-function"></a>CvIsEnabled 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题的最新版本，请参阅[CvIsEnabled 函数](https://docs.microsoft.com/visualstudio/profiling/cvisenabled-function)。  
  
确定是否有任何会话启用了指定的 ETW 提供程序。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CvIsEnabled(  
   _In_ PCV_PROVIDER pProvider  
);  
HRESULT CvIsEnabledEx(  
   _In_ PCV_PROVIDER pProvider,  
   _In_ CV_IMPORTANCE level,  
   _In_ int category  
);  
```  
  
#### <a name="parameters"></a>参数  
 `category`  
 类别。  
  
 `level`  
 重要性级别。  
  
 `pProvider`  
 有效的提供程序对象。 不能为 NULL。  
  
## <a name="return-value"></a>返回值  
 如果提供程序当前已启用，则返回 S_OK。 如果提供程序当前已禁用，则返回 S_FALSE。 出现任何错误时返回错误代码。 使用 FAILED 宏检查错误条件，然后检查 S_OK/S_FALSE。  
  
## <a name="requirements"></a>要求  
 **标头：** cvmarkers.h  
  
## <a name="see-also"></a>请参阅  
 [C++ 库参考](../profiling/cpp-library-reference.md)


