---
title: "SET NULL 명령을 | Microsoft Docs"
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
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14cade223de7014dd4a0c27295d3ff742d18af17
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="set-null-command"></a>SET NULL 명령
결정 null 값은 및 지원 되는 ALTER TABLE-SQL, CREATE TABLE-SQL INSERT-방법을 SQL 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 (드라이버에 대 한 기본, Visual FoxPro에 대 한 기본값은 OFF) ALTER TABLE과 CREATE TABLE을 사용 하 여 만든 테이블의 모든 열에 null 값을 사용할 수 있음을 지정 합니다. 열 정의에 NOT NULL 절을 포함 하 여 테이블의 열에 대 한 지원 null 값을 재정의할 수 있습니다.  
  
 삽입-SQL는 삽입할 수 있는 null 값 삽입-SQL VALUE 절에에서 포함 되지 않은 모든 열도 지정 합니다. 삽입-SQL null 값을 허용 하는 열에만 null 값을 삽입 합니다.  
  
 OFF  
 ALTER TABLE과 CREATE TABLE을 사용 하 여 만든 테이블의 모든 열은 null 값 없도록 지정 합니다. 열 정의에 NULL 절을 포함 하 여 ALTER TABLE과 CREATE TABLE의 열에 대 한 지원 null 값을 지정할 수 있습니다.  
  
 또한 삽입 하도록 지정 합니다 삽입-SQL는 빈 값 삽입-SQL VALUE 절에에서 포함 되지 않은 모든 열에 있습니다.  
  
## <a name="remarks"></a>주의  
 NULL 설정에 영향을 줍니다만 어떻게 null 값은 ALTER TABLE, CREATE TABLE 및 INSERT-SQL에서 지원 됩니다. 다른 명령을 SET NULL 영향을 받지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [테이블-SQL 명령을 만들려면](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)

