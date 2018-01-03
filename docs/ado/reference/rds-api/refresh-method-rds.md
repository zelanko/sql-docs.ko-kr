---
title: "Refresh 메서드 (RDS) | Microsoft Docs"
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords: Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5730f11f027cf6fb4492f8133f88ce80ac35aee3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="refresh-method-rds"></a>Refresh (RDS) 메서드
에 지정 된 데이터 원본 다시 쿼리는 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성 및 쿼리 결과 업데이트 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 개체 변수를 나타내는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>주의  
 설정 해야 합니다는 [연결](../../../ado/reference/rds-api/connect-property-rds.md), [서버](../../../ado/reference/rds-api/server-property-rds.md), 및 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성 사용 하기 전에 **새로 고침** 메서드. 와 연결 된 폼에 있는 모든 데이터 바인딩된 컨트롤은 **.rds입니다 DataControl** 개체에서 새 레코드 집합이 반영 됩니다. 기존의 모든 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 해제 되 고 저장 되지 않은 모든 변경 내용이 삭제 됩니다. **새로 고침** 메서드 자동으로 첫 번째 레코드를 현재 레코드로 만듭니다.  
  
 호출 하는 것이 좋습니다는 **새로 고침** 메서드 주기적으로 작업할 때 데이터를 사용 합니다. 데이터를 검색 하 고 잠시 동안 클라이언트 컴퓨터에 유지 하는 경우에 만료 될 수 있습니다. 수행한 모든 변경 내용을 실패 함을, 누군가가 레코드 변경 했을 수 하 고 제출 하기 전에 변경 내용을 때문에 불가능 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [메서드 예제를 (VB)를 새로 고칩니다.](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [메서드 (VBScript) 예제를 새로 고칩니다.](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 메서드 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


