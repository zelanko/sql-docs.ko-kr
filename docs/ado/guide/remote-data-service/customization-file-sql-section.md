---
description: 사용자 지정 파일 SQL 섹션
title: 사용자 지정 파일 SQL 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: rothja
ms.author: jroth
ms.openlocfilehash: 210363a1a852aa3c059c7929af1c07a9fe32c6ae
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978234"
---
# <a name="customization-file-sql-section"></a>사용자 지정 파일 SQL 섹션
**Sql** 섹션에는 클라이언트 명령 문자열을 대체 하는 새 sql 문자열이 포함 될 수 있습니다. 섹션에 SQL 문자열이 없는 경우 섹션은 무시 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 새 SQL 문자열은 *매개 변수화*될 수 있습니다. 즉, **sql** 섹션 sql 문자열 ('? ' 문자에 의해 지정 됨)의 매개 변수는 클라이언트 명령 문자열 (괄호 안의 쉼표로 구분 된 목록으로 지정)의 *식별자* 에서 해당 인수로 바꿀 수 있습니다. 식별자 및 인수 목록은 함수 호출 처럼 동작 합니다.  
  
 예를 들어, 클라이언트 명령 문자열이이 고 `"CustomerByID(4)"` sql 섹션 헤더가 이며 `[SQL CustomerByID]` 새 SQL 섹션 문자열은 `"SELECT * FROM Customers WHERE CustomerID = ?".` 처리기가 해당 문자열을 생성 하 `"SELECT * FROM Customers WHERE CustomerID = 4"` 고 사용 하 여 데이터 소스를 쿼리 한다고 가정 합니다.  
  
 새 SQL 문이 null 문자열 ("") 인 경우이 섹션은 무시 됩니다.  
  
 새 SQL 문 문자열이 유효 하지 않으면 문 실행이 실패 합니다. 클라이언트 매개 변수는 효과적으로 무시 됩니다. 다음을 지정 하 여이 작업을 수행 하 여 모든 클라이언트 SQL 명령을 "해제" 할 수 있습니다.  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>구문  
 대체 SQL 문자열 항목의 형식은 다음과 같습니다.  
  
 **SQL =**   
 ***sqlString***  
  
|부분|설명|  
|----------|-----------------|  
|**SQL**|SQL 섹션 항목 임을 나타내는 리터럴 문자열입니다.|  
|***sqlString***|클라이언트 문자열을 대체 하는 SQL 문자열입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 파일 연결 섹션](./customization-file-connect-section.md)   
 [사용자 지정 파일 로그 섹션](./customization-file-logs-section.md)   
 [사용자 지정 파일 UserList 섹션](./customization-file-userlist-section.md)   
 [DataFactory 사용자 지정](./datafactory-customization.md)   
 [필수 클라이언트 설정](./required-client-settings.md)   
 [사용자 지정 파일 이해](./understanding-the-customization-file.md)   
 [고유한 사용자 지정된 처리기 작성](./writing-your-own-customized-handler.md)