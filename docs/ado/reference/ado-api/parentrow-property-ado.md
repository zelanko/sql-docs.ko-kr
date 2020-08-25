---
description: ParentRow 속성(ADO)
title: ParentRow 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: rothja
ms.author: jroth
ms.openlocfilehash: d7924a27a8b04e430eb1d9d68d5de6e4d19c51a8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773272"
---
# <a name="parentrow-property-ado"></a>ParentRow 속성(ADO)
**ADORecordConstruction** 개체에 대 한 OLE DB **row** 개체의 컨테이너를 설정 하 여 행의 부모를 ADO **Record** 개체로 설정 합니다.  
  
 쓰기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>매개 변수  
 *pParent*  
 행의 컨테이너입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK 및 E_FAIL를 포함 하 여 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordConstruction 인터페이스](./adorecordconstruction-interface.md)