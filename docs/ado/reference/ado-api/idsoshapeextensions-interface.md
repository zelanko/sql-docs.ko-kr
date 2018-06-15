---
title: IDSOShapeExtensions 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbffd2f45ada95c455bb1cc44165a4c9455cfe3e
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278922"
---
# <a name="idsoshapeextensions-interface"></a>IDSOShapeExtensions 인터페이스
SHAPE 공급자에 대 한 기본 OLE DB 데이터 원본 개체를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>메서드  
  
|||  
|-|-|  
|[GetDataProviderDSO 메서드](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Shape 공급자에서 기본 OLE DB 데이터 원본 개체를 검색합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
