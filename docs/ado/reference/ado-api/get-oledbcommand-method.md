---
title: get_OLEDBCommand 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72e902c6eb27cadff5f49d5bc385b99917f977eb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850429"
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
 [out] 기본 OLE DB 명령에 대 한 IUnknown 포인터를 쓸 위치 포인터 위치에 대 한 포인터입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IADOCommandConstruction](http://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
