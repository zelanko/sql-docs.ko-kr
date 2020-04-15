---
title: 삽입 - SQL 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce00005fb1aa0ca9732fc5e9cfeacd6faf6ef9e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300011"
---
# <a name="insert---sql-command"></a>INSERT - SQL 명령
지정된 필드 값을 포함하는 테이블의 끝에 레코드를 보합합니다.  
  
 Visual FoxPro ODBC 드라이버는 이 명령에 대한 기본 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 비고를 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>인수  
 *dbf_name* 삽입  
 새 레코드가 추가되는 테이블의 이름을 지정합니다. *dbf_name* 경로를 포함할 수 있으며 이름 식일 수 있습니다.  
  
 지정한 테이블이 열려 있지 않으면 새 작업 영역에서만 열리고 새 레코드가 테이블에 추가됩니다. 새 작업 영역이 선택되지 않았습니다. 현재 작업 영역은 선택된 상태로 유지됩니다.  
  
 지정한 테이블이 열려 있으면 INSERT는 새 레코드를 테이블에 적용합니다. 테이블이 현재 작업 영역이 아닌 작업 영역에서 열려 있으면 레코드가 추가된 후 선택되지 않습니다. 현재 작업 영역은 선택된 상태로 유지됩니다.  
  
 *[(fname1[,* fname2[,...]]]] *fname2*  
 새 레코드에서 값이 삽입되는 필드의 이름을 지정합니다.  
  
 값 *(eExpression1*[, *eExpression2*[, ...]] )  
 새 레코드에 삽입된 필드 값을 지정합니다. 필드 이름을 생략하는 경우 테이블 구조에 정의된 순서대로 필드 값을 지정해야 합니다.  
  
## <a name="remarks"></a>설명  
 새 레코드에는 VALUE 절에 나열된 데이터가 포함되어 있습니다.  
  
## <a name="driver-remarks"></a>운전자 발언  
 응용 프로그램이 ODBC SQL 문 INSERT를 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 변환 없이 명령을 Visual FoxProINSERT 명령으로 변환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 만들기 - SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)
