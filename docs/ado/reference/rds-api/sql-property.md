---
title: SQL 속성 | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba032adaa8b6412b9390de644504cae6c55c74f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697711"
---
# <a name="sql-property"></a>SQL 속성
검색에 사용 되는 쿼리 문자열을 나타내고 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 설정할 수 있습니다 합니다 **SQL** 에서 디자인 타임에 속성을 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 OBJECT 태그 또는 런타임에 코드를 스크립팅 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *QueryString*  
 A **문자열** 유효한 SQL 데이터 요청을 포함 하는 값입니다.  
  
 *DataControl*  
 나타내는 개체 변수는 **rds. DataControl** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 일반적으로이 SQL 문 (데이터베이스 서버의 언어 사용)와 같은 `"Select * from NewTitles"`합니다. 레코드 일치 하 고 정확 하 게 업데이트 하도록 쿼리를 업데이트할 수 있는 긴 이진 필드 또는 계산된 된 필드 이외의 필드를 포함 해야 합니다.  
  
 합니다 **SQL** 속성은 사용자 지정 서버 쪽 비즈니스 개체를 클라이언트에 대 한 데이터를 검색 하는 경우 선택 사항입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL 속성 예제 (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Connect 속성 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Query 메서드 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 메서드 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


