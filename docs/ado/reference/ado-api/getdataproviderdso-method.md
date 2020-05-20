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
author: rothja
ms.author: jroth
ms.openlocfilehash: 55272fdbcd0aacfc8e98cb4e38ae19270b3b461a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760049"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO 메서드
셰이프 공급자에서 내부 OLE DB 데이터 소스 개체를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ppDataProviderDSOIUnknown*  
 제한이  내부 OLE DB 데이터 소스 개체의 IUnknown을 반환 하는 포인터에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 인터페이스 포인터를 addref 하지 않습니다. 호출자가 포인터를 보유 하도록 계획 하는 경우 호출자는 필수 addref 및 릴리스를 수행 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IDSOShapeExtensions 인터페이스](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
