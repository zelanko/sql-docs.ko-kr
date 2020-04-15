---
title: NULL 명령 설정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300813"
---
# <a name="set-null-command"></a>SET NULL 명령
ALTER TABLE - SQL, CREATE TABLE - SQL 및 INSERT - SQL 명령에서 null 값을 지원하는 방법을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 (드라이버에 대 한 기본값; Visual FoxPro에 대 한 기본값은 꺼져 있습니다.) ALTER TABLE 및 CREATE TABLE으로 만든 테이블의 모든 열이 null 값을 허용하도록 지정합니다. 열의 정의에 NOT NULL 절을 포함하 여 테이블에 있는 열에 대 한 null 값 지원을 재정의할 수 있습니다.  
  
 또한 INSERT - SQL이 INSERT - SQL VALUE 절에 포함되지 않은 열에 null 값을 삽입할 것을 지정합니다. INSERT - SQL은 null 값을 허용하는 열에만 null 값을 삽입합니다.  
  
 OFF  
 ALTER TABLE 및 CREATE TABLE으로 만든 테이블의 모든 열이 null 값을 허용하지 않도록 지정합니다. ALTER TABLE 및 CREATE TABLE의 열에 대한 null 값 지원을 열의 정의에 NULL 절을 포함시켜 지정할 수 있습니다.  
  
 또한 INSERT - SQL은 INSERT - SQL VALUE 절에 포함되지 않은 열에 빈 값을 삽입할 것을 지정합니다.  
  
## <a name="remarks"></a>설명  
 SET NULL은 ALTER TABLE, CREATE TABLE 및 INSERT - SQL에서 null 값을 지원하는 방법에만 영향을 줍니다. 다른 명령은 SET NULL의 영향을 받지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 변경 - SQL 명령](../../odbc/microsoft/alter-table-sql-command.md)   
 [테이블 만들기 - SQL 명령](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
