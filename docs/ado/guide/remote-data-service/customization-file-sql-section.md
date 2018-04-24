---
title: 사용자 지정 파일 SQL 섹션 | Microsoft Docs
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
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6294ab601f527527cf69ca017e3643dfe98a1336
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="customization-file-sql-section"></a>사용자 지정 파일 SQL 섹션
**sql** 섹션에는 클라이언트 명령 문자열을 대체 하는 새로운 SQL 문자열 포함 될 수 있습니다. 섹션에서 SQL 문자열이 없는 섹션 무시 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 새 SQL 문자열 수 *매개 변수가 있는*합니다. 즉, 매개 변수에서는 **sql** SQL 문자열 섹션 (로 지정 된는 '?' 문자)에 해당 하는 인수에 대체 될 수 있습니다는 *식별자* 클라이언트 명령 문자열에서 (로 지정 된는 쉼표로 구분 된 목록을 괄호 안에 있음)입니다. 식별자와 인수 목록은 함수 호출 처럼 동작합니다.  
  
 예를 들어, 클라이언트 명령 문자열은 `"CustomerByID(4)"`, SQL 섹션 헤더는 `[SQL CustomerByID]`, 새 SQL 섹션 문자열이 `"SELECT * FROM Customers WHERE CustomerID = ?".` 처리기를 생성 합니다 `"SELECT * FROM Customers WHERE CustomerID = 4"` 해당 문자열을 사용 하 여 데이터 원본을 쿼리할 수 있습니다.  
  
 새 SQL 문을 null 문자열인 경우 (""), 섹션은 무시 됩니다.  
  
 새 SQL 문 문자열이 유효 하지 않을 경우 문 실행이 실패 합니다. 클라이언트 매개 변수는 효과적으로 무시 됩니다. 의도적으로 "사용 하지 않으려면" 모든 클라이언트 SQL 명령을 지정 하 여이 수행할 수 있습니다.  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>구문  
 대체 SQL 문자열 항목 형식입니다.  
  
 **SQL=**   
 ***sqlString***  
  
|부분|Description|  
|----------|-----------------|  
|**SQL**|이 설정에 리터럴 문자열은 SQL 섹션 항목입니다.|  
|***sqlString***|클라이언트 문자열을 대체 하는 SQL 문자열입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필요한 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


