---
title: "SQL 명령-삽입 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6862ff2ec4d95ce6a2149bbcd7647cdf8ea6819f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="insert---sql-command"></a>SQL 명령-삽입
지정된 된 필드 값이 포함 된 테이블의 끝에 레코드를 추가 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 주의 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>인수  
 INSERT INTO *dbf_name*  
 새 레코드가 추가 테이블의 이름을 지정 합니다. *dbf_name* 경로 포함할 수 있으며 이름 식이 될 수 있습니다.  
  
 지정한 테이블 열려 있지 않으면 새 작업 영역에서 단독으로 열려 있는 및 테이블에 새 레코드가 추가 됩니다. 새 작업 영역을 선택 하지 않으면; 현재 작업 영역 선택 되어 있습니다.  
  
 지정한 테이블 열려 있으면 INSERT 테이블에 새 레코드를 추가 합니다. 현재 작업 영역 아닌 다른 테이블이 작업 영역에서 열려 있는 경우는 레코드가 추가 된; 후 선택 되지 않은 현재 작업 영역 선택 되어 있습니다.  
  
 [( *fname1*[, *fname2*[,...]])]  
 새 레코드의 필드의 이름을 지정에 값 삽입 됩니다.  
  
 값 ( *eExpression1*[, *eExpression2*[,...]])  
 새 레코드에 삽입 된 필드 값을 지정 합니다. 필드 이름을 생략 하면 테이블 구조에 정의 된 순서로 필드 값을 지정 해야 합니다.  
  
## <a name="remarks"></a>주의  
 새 레코드는 VALUES 절에 나열 된 데이터를 포함 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램의 데이터 원본에는 ODBC SQL 문을 삽입 보내면 Visual FoxPro ODBC 드라이버를 변환 하지 않아도 Visual FoxProINSERT 명령으로 스크립팅 명령으로 변환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블-SQL 명령을 만들려면](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)

