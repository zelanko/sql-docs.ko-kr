---
title: GetDataProviderDSO 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2b5fbe59ab58b31cd0b796cbe46963683aa890b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932484"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 메서드
셰이프 공급자에서 기본 OLE DB 데이터 원본 개체를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ppDataProviderDSOIUnknown*  
 [out]  기본 OLE DB 데이터 원본 개체의 IUnknown을 반환 하는 포인터에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 인터페이스 포인터를 addref 하지를 않습니다. 호출자에 게 포인터를 저장 하는 계획을 호출자에 게 작업을 수행 해야 필요한 addref 및 릴리스 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IDSOShapeExtensions 인터페이스](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
