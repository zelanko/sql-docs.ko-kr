---
title: Query 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1088a06456152ad9845361e733acfc250591a7d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="query-method-rds"></a>Query 메서드 (RDS)
유효한 SQL 쿼리 문자열을 사용 하 여 반환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *레코드 집합*  
 개체 변수를 나타내는 **레코드 집합** 개체입니다.  
  
 *DataFactory*  
 개체 변수를 나타내는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체입니다.  
  
 *연결*  
 A **문자열** 서버 연결 정보를 포함 하는 값입니다. 이 비슷합니다는 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성입니다.  
  
 *데이터 집합 속성*  
 A **문자열** SQL 쿼리 포함 합니다.  
  
## <a name="remarks"></a>주의  
 쿼리는 데이터베이스 서버의 SQL 언어를 사용 해야 합니다. 실행 된 쿼리에 동안 오류가 발생 하는 경우 결과 상태가 반환 됩니다. **쿼리** 메서드 모든 구문 검사를 수행 하지 않습니다는 **쿼리** 문자열입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>관련 항목:  
 [DataFactory 개체, Query 메서드 및 CreateObject 메서드 예제(VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


