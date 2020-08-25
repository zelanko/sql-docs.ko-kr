---
description: put_OLEDBCommand 메서드
title: put_OLEDBCommand 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: rothja
ms.author: jroth
ms.openlocfilehash: e386485f5e430a1bda50aa0d2059aeca90525af2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772772"
---
# <a name="put_oledbcommand-method"></a>put_OLEDBCommand 메서드
이 메서드는 작업을 수행 하지 않으며 항상 S_OK을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pOLEDBCommand*  
 진행 OLE DB Command 개체에 대 한 포인터입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))