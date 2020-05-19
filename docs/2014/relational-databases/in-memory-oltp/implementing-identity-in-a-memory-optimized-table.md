---
title: 메모리 액세스에 최적화된 테이블에서 IDENTITY 구현 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a3fe549e5a49dcc7c0c0417199206a6fd34079ac
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706492"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>메모리 액세스에 최적화된 테이블에서 IDENTITY 구현
  IDENTITY(1, 1)는 메모리 최적화 테이블에서 지원됩니다. 그러나 x != 1 또는 y != 1인 IDENTITY(x, y) 정의를 사용하는 ID 열은 메모리 최적화 테이블에서 지원되지 않습니다. IDENTITY 값에 대한 해결 방법은 SEQUENCE 개체를 사용합니다([Sequence Numbers](../sequence-numbers/sequence-numbers.md)).  
  
 먼저 메모리 내 OLTP로 변환 중인 테이블에서 IDENTITY 속성을 제거합니다. 그런 다음 테이블의 행에 대해 새 SEQUENCE 개체를 정의합니다. ID 열인 SEQUENCE 개체는 NEXT VALUE FOR 구문을 사용하여 새 ID 값을 얻기 위해 열의 DEFAULT 값을 만드는 기능에 의존합니다. 메모리 내 OLTP에서는 DEFAULT가 지원되지 않으므로 새로 생성된 SEQUENCE 값을 INSERT 문 또는 삽입을 수행하는 고유하게 컴파일된 저장 프로시저로 전달해야 합니다. 다음 예에서는 이러한 패턴을 보여 줍니다.  
  
```sql  
-- Create a new In-Memory OLTP table to simulate IDENTITY insert  
-- Here the column C1 was the identity column in the original table  
--  
create table T1  
(  
  
[c1] integer not null primary key T1_c1 nonclustered,  
[c2] varchar(32) not null,  
[c3] datetime not null  
  
) with (memory_optimized = on)  
go  
  
-- This is a sequence provider that will give us values for column [c1]  
--  
create sequence usq_SequenceForT1 as integer start with 2 increment by 1  
go  
  
--   insert a sample row using the sequence  
--   note that a new value needs to be retrieved form   
--   the sequence object for every insert  
--  
declare @c1 integer = next value for [dbo].[usq_SequenceForT1]  
insert into T1 values (@c1, 'test', getdate())  
```  
  
 삽입을 여러 번 수행하면 [c1] 열에 단순하게 증가하는 유효한 값이 나타납니다. 이 결과 집합은 `ORDER BY` 없이 테이블 검색과 해시 인덱스를 사용하여 생성되므로 행은 정렬되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
