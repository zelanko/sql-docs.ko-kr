---
title: Refresh 메서드 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9992b0f7e7281ec318f978ff487107fc832c961f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697527"
---
# <a name="refresh-method-rds"></a>Refresh 메서드(RDS)
에 지정 된 데이터 원본 다시 쿼리 합니다 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성 및 쿼리 결과 업데이트 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 나타내는 개체 변수는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 설정 해야 합니다는 [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [서버](../../../ado/reference/rds-api/server-property-rds.md), 및 [SQL](../../../ado/reference/rds-api/sql-property.md) 사용 하기 전에 속성을 **새로 고침** 메서드. 모든 데이터 바인딩된 컨트롤이 연결 된 양식에 **rds. DataControl** 개체는 새 레코드 집합을 반영 합니다. 모든 기존 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 해제 되 고 저장 되지 않은 모든 변경 내용이 삭제 됩니다. 합니다 **새로 고침** 메서드 자동으로 첫 번째 레코드를 현재 레코드로 만듭니다.  
  
 호출 하는 것이 좋습니다 합니다 **새로 고침** 메서드 주기적으로 작업할 때 데이터를 사용 하 여 합니다. 데이터를 검색 하는 동안 클라이언트 컴퓨터에서 유지 하는 경우에 만료 될 수 있습니다. 수행한 모든 변경 내용을 실패 하므로 다른 사용자가 레코드를 변경 했을 수와 제출 하기 전에 변경 내용을 가능성이 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [Refresh 메서드 예제 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 메서드 예제 (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 메서드 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


