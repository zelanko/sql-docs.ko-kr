---
title: SET NULL 명령 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6f0e23abd31661210282967fa35080376eaaaf3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765637"
---
# <a name="set-null-command"></a>SET NULL 명령
결정 방법 null 값은 및 지원 되는 ALTER TABLE-SQL, CREATE TABLE-SQL INSERT-SQL 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 (드라이버에 대 한 기본; Visual FoxPro에 대 한 기본값은 OFF입니다.) ALTER TABLE 및 CREATE TABLE을 사용 하 여 만든 테이블의 모든 열에 null 값을 사용할 수 있음을 지정 합니다. 열 정의에 NOT NULL 절을 포함 하 여 테이블의 열에 대 한 지원을 null 값을 재정의할 수 있습니다.  
  
 또한는 INSERT-SQL는 null 값에 삽입 INSERT-SQL VALUE 절에에서 포함 되지 않은 모든 열을 지정 합니다. INSERT-SQL null을 허용 하는 열에만 null 값을 삽입 됩니다.  
  
 OFF  
 ALTER TABLE 및 CREATE TABLE을 사용 하 여 만든 테이블의 모든 열 null 값을 사용할 수 있음을 지정 합니다. 열 정의에 NULL 절을 포함 하 여 ALTER TABLE 및 CREATE TABLE의 열에 대해 null 값 처리 지원을 지정할 수 있습니다.  
  
 또한는 INSERT-SQL는 빈 값에 삽입 INSERT-SQL VALUE 절에에서 포함 되지 않은 모든 열을 지정 합니다.  
  
## <a name="remarks"></a>Remarks  
 NULL 설정에 영향을 줍니다만 어떻게 null 값은 ALTER TABLE, CREATE TABLE 및 INSERT-SQL에서 지원 됩니다. 다른 명령을 SET NULL 영향을 받지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE-SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
