---
title: 사용자 지정 파일 SQL 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba0d8c7ab1294400c19456abf164c6ad6be0dd2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704310"
---
# <a name="customization-file-sql-section"></a>사용자 지정 파일 SQL 섹션
합니다 **sql** 섹션 클라이언트 명령 문자열을 대체 하는 새 SQL 문자열을 포함할 수 있습니다. 섹션에서 SQL 문자열이 없을 경우 섹션 무시 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 새 SQL 문자열을 사용할 수 있습니다 *매개 변수가 있는*합니다. 매개 변수 즉,는 **sql** SQL 문자열 섹션 (지정 된는 '?' 문자) 해당 인수에 대체 될 수 있습니다는 *식별자* 클라이언트 명령 문자열에 (지정 된을 쉼표로 구분 된 목록을 괄호 안에 있음)입니다. 식별자와 인수 목록은 함수 호출 처럼 동작합니다.  
  
 예를 들어, 클라이언트 명령 문자열은 `"CustomerByID(4)"`, SQL 섹션 헤더를 `[SQL CustomerByID]`, 새 SQL 섹션 문자열이 `"SELECT * FROM Customers WHERE CustomerID = ?".` The 처리기 생성 됩니다 `"SELECT * FROM Customers WHERE CustomerID = 4"` 해당 문자열을 사용 하 여 데이터 원본을 쿼리 합니다.  
  
 새 SQL 문을 null 문자열인 경우 (""), 섹션 무시 됩니다.  
  
 새 SQL 문 문자열이 올바르지 않으면 문이 실행이 실패 합니다. 클라이언트 매개 변수는 실질적으로 무시 됩니다. 의도적으로 "기능을 해제 하려면" 모든 클라이언트 SQL 명령을 지정 하 여이 수행할 수 있습니다.  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>구문  
 SQL 문자열 항목을 대체 폼입니다.  
  
 **SQL=**    
 ***sqlString***  
  
|부분|설명|  
|----------|-----------------|  
|**SQL**|이 나타내는 리터럴 문자열에는 SQL 섹션 항목입니다.|  
|***sqlString***|클라이언트 문자열을 대체 하는 SQL 문자열입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 파일 연결 섹션](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [사용자 지정 파일 UserList 섹션](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [필수 클라이언트 설정](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [사용자 지정 파일 이해](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


