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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c83c9ef9f8a0ce143308b73d8df09b05fb2cdea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300813"
---
# <a name="set-null-command"></a>SET NULL 명령
ALTER TABLE-SQL, CREATE TABLE, sql 삽입 명령에서 null 값이 지원 되는 방식을 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 (드라이버의 기본값입니다. Visual FoxPro의 기본값은 OFF입니다.) ALTER TABLE 및 CREATE TABLE를 사용 하 여 만든 테이블의 모든 열이 null 값을 허용 하도록 지정 합니다. 열 정의에 NOT NULL 절을 포함 하 여 테이블의 열에 대해 null 값 지원을 재정의할 수 있습니다.  
  
 또한 insert-SQL은 INSERT-SQL VALUE 절에 포함 되지 않은 모든 열에 null 값을 삽입 하도록 지정 합니다. INSERT-SQL은 null 값을 허용 하는 열에만 null 값을 삽입 합니다.  
  
 OFF  
 ALTER TABLE 및 CREATE TABLE를 사용 하 여 만든 테이블의 모든 열이 null 값을 허용 하지 않도록 지정 합니다. 열 정의에 NULL 절을 포함 하 여 ALTER TABLE 및 CREATE TABLE의 열에 대해 null 값을 지원 하도록 지정할 수 있습니다.  
  
 또한 insert-SQL은 INSERT-SQL VALUE 절에 포함 되지 않은 열에 빈 값을 삽입 하도록 지정 합니다.  
  
## <a name="remarks"></a>설명  
 SET NULL은 ALTER TABLE, CREATE TABLE 및 INSERT SQL에서 null 값이 지원 되는 방식에만 영향을 줍니다. 다른 명령은 SET NULL의 영향을 받지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE-SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
