---
title: "get_OLEDBCommand 메서드 | Microsoft Docs"
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
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c78a0b7bd79da2bc75c3bcccbcb2bc9acbde8e35
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getoledbcommand-method"></a>get_OLEDBCommand 메서드
기본 OLE DB 명령을 먼저 OLE DB 명령에 ADO 명령에 설정 하는 모든 매개 변수 정보를 전파를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ppOLEDBCommand*  
 [out] 기본 OLE DB 명령에 대 한 IUnknown 포인터를 쓸 포인터 위치에 대 한 포인터입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IADOCommandConstruction](http://msdn.microsoft.com/en-us/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)

