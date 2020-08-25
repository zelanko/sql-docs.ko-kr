---
description: Cancel 메서드(RDS)
title: Cancel 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f4e902888285f758975ffce0381a08b813152ba
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768812"
---
# <a name="cancel-method-rds"></a>Cancel 메서드(RDS)
보류 중인 비동기 메서드 호출의 실행을 취소 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>설명  
 **Cancel**을 호출 하면 [ReadyState](./readystate-property-rds.md) 가 자동으로 **Adcreadystateloaded**로 설정 되 고 [레코드 집합](../ado-api/recordset-object-ado.md) 은 비어 있게 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [Cancel 메서드 예제 (VBScript)](./cancel-method-example-vbscript.md)   
 [Cancel 메서드 (ADO)](../ado-api/cancel-method-ado.md)   
 [CancelBatch 메서드 (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](./cancelupdate-method-rds.md)   
 [ExecuteOptions 속성(RDS)](./executeoptions-property-rds.md)