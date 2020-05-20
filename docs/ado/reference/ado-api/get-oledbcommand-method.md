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
author: rothja
ms.author: jroth
ms.openlocfilehash: 043e432bfef39f90fbeb5b147487272c4d284bdb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760079"
---
# <a name="get_oledbcommand-method"></a>get_OLEDBCommand 메서드
먼저 ADO 명령에 설정 된 매개 변수 정보를 OLE DB 명령에 전파 하는 기본 OLE DB 명령을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ppOLEDBCommand*  
 제한이 기본 OLE DB 명령에 대 한 IUnknown 포인터가 작성 될 포인터 위치에 대 한 포인터입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IADOCommandConstruction](https://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
