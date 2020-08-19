---
description: INSERT - SQL 명령
title: SQL 명령 삽입 | Microsoft Docs
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
ms.openlocfilehash: 92c4b2068149164716d52fd3693e56164ab788ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449505"
---
# <a name="insert---sql-command"></a>INSERT - SQL 명령
지정 된 필드 값을 포함 하는 테이블의 끝에 레코드를 추가 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다. 드라이버 관련 정보는 설명 부분을 참조 하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>인수  
 *DBF_NAME* 에 삽입  
 새 레코드가 추가 되는 테이블의 이름을 지정 합니다. *dbf_name* 는 경로를 포함할 수 있으며 이름 식일 수 있습니다.  
  
 지정한 테이블이 열려 있지 않으면 새 작업 영역에서 단독으로 열리고 새 레코드가 테이블에 추가 됩니다. 새 작업 영역이 선택 되지 않았습니다. 현재 작업 영역은 선택 된 상태로 유지 됩니다.  
  
 지정한 테이블이 열려 있으면 INSERT는 테이블에 새 레코드를 추가 합니다. 테이블이 현재 작업 영역 이외의 작업 영역에 열려 있는 경우 레코드가 추가 된 후에도 선택 되지 않습니다. 현재 작업 영역은 선택 된 상태로 유지 됩니다.  
  
 [( *fname1*[, *fname2*[, ...]])]  
 새 레코드에서 값이 삽입 되는 필드의 이름을 지정 합니다.  
  
 VALUES ( *eExpression1*[, *eExpression2*[, ...]])  
 새 레코드에 삽입 되는 필드 값을 지정 합니다. 필드 이름을 생략 하는 경우 테이블 구조에 정의 된 순서 대로 필드 값을 지정 해야 합니다.  
  
## <a name="remarks"></a>설명  
 새 레코드에는 VALUES 절에 나열 된 데이터가 포함 됩니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문을 데이터 원본에 전송할 때 Visual FoxPro ODBC 드라이버는 변환 하지 않고 명령을 Visual FoxProINSERT 명령으로 변환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 명령](../../odbc/microsoft/select-sql-command.md)
