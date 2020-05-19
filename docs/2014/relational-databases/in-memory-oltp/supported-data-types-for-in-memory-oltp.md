---
title: 지원 되는 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b7ba8c40979873cc2c3f2358b57dc0e491a1795e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718832"
---
# <a name="supported-data-types"></a>지원되는 데이터 형식
  다음은 메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저에서 **지원되는** 데이터 형식입니다.  
  
 **숫자 데이터 형식**  
  
|데이터 형식|참조 항목|  
|---------------|--------------------------|  
|int|[int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|bigint|[int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|smallint|[int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|tinyint|[int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|decimal|[decimal 및 numeric&#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|numeric|[decimal 및 numeric&#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|float|[float 및 real &#40;Transact-SQL&#41;](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|real|[float 및 real &#40;Transact-SQL&#41;](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|money|[money 및 smallmoney&#40;Transact-SQL&#41;](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
|smallmoney|[money 및 smallmoney&#40;Transact-SQL&#41;](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
  
 **문자열 데이터 형식**  
  
|데이터 형식|참조 항목|  
|---------------|--------------------------|  
|char(n)|[char 및 varchar&#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|varchar (n) <sup>1</sup>|[char 및 varchar&#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|nchar(n)|[nchar 및 nvarchar&#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|nvarchar (n) <sup>1</sup>|[nchar 및 nvarchar&#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|sysname|[nchar 및 nvarchar&#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
  
 <sup>1</sup> 제한은 가변 길이 형식의 계산 (n)을 통해 8060 바이트의 행 합계입니다.  
  
 지원되는 데이터 정렬에 대한 자세한 내용은 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)를 참조하세요.  
  
 **날짜 및 시간 데이터 형식**  
  
|데이터 형식|참조 항목|  
|---------------|--------------------------|  
|date|[date&#40;Transact-SQL&#41;](/sql/t-sql/data-types/date-transact-sql)|  
|time|[time &#40;Transact-SQL&#41;](/sql/t-sql/data-types/time-transact-sql)|  
|Datetime|[datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)|  
|datetime2|[datetime2&#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime2-transact-sql)|  
|smalldatetime|[smalldatetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/smalldatetime-transact-sql)|  
  
 **이진 데이터 형식**  
  
|데이터 형식|참조 항목|  
|---------------|--------------------------|  
|bit|[bit &#40;Transact-SQL&#41;](/sql/t-sql/data-types/bit-transact-sql)|  
|binary(n)|[binary 및 varbinary&#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
|varbinary (n) <sup>1</sup>|[binary 및 varbinary&#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
  
 <sup>1</sup> 제한은 가변 길이 형식의 계산 (n)을 통해 8060 바이트의 행 합계입니다.  
  
 **기타 데이터 형식**  
  
|데이터 형식|참조 항목|  
|---------------|--------------------------|  
|uniqueidentifier|[uniqueidentifier&#40;Transact-SQL&#41;](/sql/t-sql/data-types/uniqueidentifier-transact-sql)|  
  
 **지원 되지 않는 데이터 형식**  
  
 다음 데이터 형식은 지원되지 않습니다.  
  
||||  
|-|-|-|  
|DATETIMEOFFSET|GEOGRAPHY|GEOMETRY|  
|HIERARCHYID|LOB(Large Object). 예: varchar(max), nvarchar(max), varbinary(max), image, xml, text 및 ntext|ROWVERSION|  
|sql_variant|CLR 함수|UDT(사용자 정의 형식)|  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP에 대 한 transact-sql 지원](transact-sql-support-for-in-memory-oltp.md)   
 [메모리 액세스에 최적화 된 테이블에서 LOB 열 구현](../../database-engine/implementing-lob-columns-in-a-memory-optimized-table.md)   
 [메모리 액세스에 최적화된 테이블에서 SQL_VARIANT 구현](implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  
