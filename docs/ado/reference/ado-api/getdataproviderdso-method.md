---
title: GetDataProviderDSO 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fca773c6db137999da36daf0151a51a1becf79c6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
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
