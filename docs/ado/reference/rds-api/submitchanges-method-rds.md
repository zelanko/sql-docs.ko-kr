---
title: SubmitChanges 메서드 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c4f2b3a0cf70d068e1f6a7124e7152c8329ebd1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="submitchanges-method-rds"></a>SubmitChanges 메서드 (RDS)
보류 중인 변경 내용을 로컬로 캐시 된 및 업데이트할 수 있는 전송 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에 지정 된 데이터 원본에는 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성 또는 [URL](../../../ado/reference/rds-api/url-property-rds.md) 속성입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 개체 변수를 나타내는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *DataFactory*  
 개체 변수를 나타내는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다.  
  
 *연결*  
 A **문자열** 사용 하 여 만든 연결을 나타내는 값의 **.rds입니다 DataControl** 개체의 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성입니다.  
  
 *레코드 집합*  
 개체 변수를 나타내는 **레코드 집합** 개체입니다.  
  
## <a name="remarks"></a>주의  
 [연결](../../../ado/reference/rds-api/connect-property-rds.md), [서버](../../../ado/reference/rds-api/server-property-rds.md), 및 [SQL](../../../ado/reference/rds-api/sql-property.md) 사용 하기 전에 속성을 설정 해야 합니다는 **SubmitChanges** 메서드는  **.RDS DataControl** 개체입니다.  
  
 호출 하는 경우는 [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) 메서드를 호출한 후 **SubmitChanges** 동일한 컴퓨터에 대해 **레코드 집합** 개체는 **CancelUpdate** 변경 내용을 이미 커밋 되었는지 호출이 실패 합니다.  
  
 변경 된 레코드만 성공 하거나 모든 변경 내용을 함께 실패, 수정 하 고 변경 내용을 모두 전송 됩니다.  
  
 사용할 수 있습니다 **SubmitChanges** 기본과만 **업데이트할** 개체입니다. 사용자 지정 비즈니스 개체는이 메서드를 사용할 수 없습니다.  
  
 경우는 **URL** 속성이 설정 되어 **SubmitChanges** 변경 내용을 URL에서 지정한 위치에 전송 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [SubmitChanges 메서드 예제 (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 메서드(RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



