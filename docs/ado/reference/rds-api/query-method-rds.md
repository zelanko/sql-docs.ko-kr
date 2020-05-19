---
title: Query 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: rothja
ms.author: jroth
ms.openlocfilehash: b3025f37b47cd545e7e7cde127e96740077ab961
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751492"
---
# <a name="query-method-rds"></a>Query 메서드(RDS)
는 유효한 SQL 쿼리 문자열을 사용 하 여 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)을 반환 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *레코드 집합*  
 **레코드 집합** 개체를 나타내는 개체 변수입니다.  
  
 *DataFactory*  
 DataFactory 개체를 나타내는 개체 변수 [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *연결*  
 서버 연결 정보를 포함 하는 **문자열** 값입니다. 이는 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성과 유사 합니다.  
  
 *쿼리*  
 SQL 쿼리를 포함 하는 **문자열** 입니다.  
  
## <a name="remarks"></a>설명  
 이 쿼리는 데이터베이스 서버의 SQL 언어를 사용 해야 합니다. 실행 된 쿼리에 오류가 있으면 결과 상태가 반환 됩니다. 쿼리 **메서드에서는** **쿼리** 문자열에 대 한 구문 검사를 수행 하지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataFactory 개체, Query 메서드 및 CreateObject 메서드 예제(VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


