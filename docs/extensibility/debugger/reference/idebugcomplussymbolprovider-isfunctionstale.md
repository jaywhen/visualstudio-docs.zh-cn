---
title: IDebugComPlusSymbolProvider：： IsFunctionStale |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::IsFunctionStale
ms.assetid: dcffc090-4ed8-47b2-ba51-bce1a6b6428d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4e5b42e8bb89a84b5274669173c93db3e287755a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80733694"
---
# <a name="idebugcomplussymbolproviderisfunctionstale"></a>IDebugComPlusSymbolProvider::IsFunctionStale
确定指定的调试地址处的函数是否被视为过时。

## <a name="syntax"></a>语法

```cpp
HRESULT IsFunctionStale(
    IDebugAddress* pAddress
);
```

```csharp
int IsFunctionStale(
    IDebugAddress pAddress
);
```

## <a name="parameters"></a>参数
`pAddress`\
中由 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口表示的调试地址。 此地址必须是 METHOD_ADDRESS。

## <a name="return-value"></a>返回值
如果此函数被视为过时，则返回 `S_OK` 。 如果函数未过时，则返回 `S_FALSE` 。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的**CDebugSymbolProvider**对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::IsFunctionStale(
    IDebugAddress* pAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pAddress, IDebugAddress));

    METHOD_ENTRY( CDebugSymbolProvider::IsFunctionStale );

    IfFalseGo( pAddress, S_FALSE );
    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    if (!pModule->IsFunctionStale( address.addr.addr.addrMethod.tokMethod,
                                   address.addr.addr.addrMethod.dwVersion ))
    {

        // S_FALSE indicates the function is not stale

        hr = S_FALSE;
    }

Error:

    METHOD_EXIT( CDebugSymbolProvider::IsFunctionStale, hr );

    if (!SUCCEEDED(hr))
    {
        hr = S_FALSE;
    }

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
