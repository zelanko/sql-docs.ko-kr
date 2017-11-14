---
title: "GetDataProviderDSO 메서드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 40b23b500c50100b5a50f06566eeadd44e7f519c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 메서드
Shape 공급자에서 기본 OLE DB 데이터 원본 개체를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ppDataProviderDSOIUnknown*  
 [out]  내부 OLE DB 데이터 원본 개체의 IUnknown을 반환 하는 포인터에 대 한 포인터입니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 인터페이스 포인터를 addref 하지 않습니다. 호출자에 게 포인터를 계획, 호출자에 게 필요한 addref를 수행 해야 하 고 해제 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IDSOShapeExtensions 인터페이스](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)

