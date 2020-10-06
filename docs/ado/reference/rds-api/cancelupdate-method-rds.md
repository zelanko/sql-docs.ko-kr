---
description: CancelUpdate 메서드(RDS)
title: CancelUpdate 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CancelUpdate method [RDS]
ms.assetid: 76d8a6e9-bc6c-4ea0-8e7a-2bae5ed06650
author: rothja
ms.author: jroth
ms.openlocfilehash: 8cb9bcb9e0bf18cc2b6ab8d654eaccdc92ff7563
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722624"
---
# <a name="cancelupdate-method-rds"></a>CancelUpdate 메서드(RDS)
[레코드 집합](../ado-api/recordset-object-ado.md) 개체의 현재 또는 새 행에 대 한 변경 내용을 취소 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.CancelUpdate  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>설명  
 OLE DB에 대 한 커서 서비스는 원래 값의 복사본과 변경 내용의 캐시를 모두 유지 합니다. **CancelUpdate**를 호출 하면 변경 내용의 캐시가 비어 있는 것으로 다시 설정 되 고 바인딩된 모든 컨트롤이 원래 데이터로 새로 고쳐집니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [CancelUpdate 메서드 예제 (VBScript)](./cancelupdate-method-example-vbscript.md)   
 [주소록 명령 단추](../../guide/remote-data-service/address-book-command-buttons.md)   
 [Cancel 메서드 (ADO)](../ado-api/cancel-method-ado.md)   
 [Cancel 메서드 (RDS)](./cancel-method-rds.md)   
 [CancelBatch 메서드 (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [Refresh 메서드 (RDS)](./refresh-method-rds.md)   
 [SubmitChanges 메서드(RDS)](./submitchanges-method-rds.md)