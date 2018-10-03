---
title: DML 트리거 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], about triggers
- DML triggers, about DML triggers
- triggers [SQL Server]
ms.assetid: 298eafca-e01f-4707-8c29-c75546fcd6b0
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 979866917514cb10689f60bf5114d02dbe889fd9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826711"
---
# <a name="dml-triggers"></a>DML 트리거
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  DML 트리거는 트리거에 정의된 테이블 또는 뷰에 영향을 주는 DML(데이터 조작 언어) 이벤트가 실행될 때 자동으로 적용되는 특별한 유형의 저장 프로시저입니다. DML 이벤트에는 INSERT, UPDATE 또는 DELETE 문이 포함됩니다. DML 트리거를 사용하여 비즈니스 규칙과 데이터 무결성을 적용하고, 다른 테이블을 쿼리하고, 복잡한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함할 수 있습니다. 트리거 및 트리거를 시작하는 문은 트리거 내에서 롤백할 수 있는 단일 트랜잭션으로 처리됩니다. 디스크 공간 부족 등의 심각한 오류가 발견되면 전체 트랜잭션이 자동으로 롤백됩니다.  
  
## <a name="dml-trigger-benefits"></a>DML 트리거의 이점  
 DML 트리거는 엔터티 무결성 또는 도메인 무결성을 적용할 수 있다는 점에서 제약 조건과 비슷합니다. 일반적으로 PRIMARY KEY 및 UNIQUE 제약 조건의 일부가 되거나 제약 조건과 상관없이 생성되는 인덱스는 가장 낮은 수준에서 항상 엔터티 무결성이 강제 적용되어야 합니다. 도메인 무결성은 CHECK 제약 조건을 통해 강제 적용되어야 하고, 참조 무결성(RI)은 FOREIGN KEY 제약 조건을 통해 강제 적용되어야 합니다. DML 트리거는 제약 조건에서 지원하는 기능이 응용 프로그램에서 필요한 기능을 수행하지 못할 때 가장 유용합니다.  
  
 다음 목록에서는 DML 트리거를 제약 조건과 비교하고 DML 트리거의 이점을 식별합니다.  
  
-   DML 트리거는 데이터베이스의 관련 테이블을 통해 변경 내용을 연계할 수 있습니다. 그러나 연계 참조 무결성 제약 조건을 사용하면 더 효율적으로 변경할 수 있습니다. REFERENCES 절이 연계 참조 동작을 정의하지 않으면 FOREIGN KEY 제약 조건은 다른 열의 값과 정확히 일치하는 열 값에 대해서만 유효성을 검사할 수 있습니다.  
  
-   DML 트리거는 악의적이거나 잘못된 INSERT, UPDATE 및 DELETE 작업으로부터 보호하며 CHECK 제약 조건으로 정의하는 것보다 복잡한 다른 제약 조건을 적용합니다.  
  
     CHECK 제약 조건과 달리 DML 트리거는 다른 테이블의 열을 참조할 수 있습니다. 예를 들어 트리거는 다른 테이블에서 SELECT 문을 사용하여 삽입되거나 업데이트된 데이터와 비교하고 데이터 수정 또는 사용자 정의 오류 메시지 표시 등의 추가 동작을 수행할 수 있습니다.  
  
-   데이터 수정 전후의 테이블 상태를 평가하고 이 차이점에 따라 동작을 수행할 수도 있습니다.  
  
-   테이블에 같은 유형(INSERT, UPDATE 또는 DELETE)의 DML 트리거를 여러 개 만들면 같은 수정 문이 실행될 때 여러 다른 동작을 실행할 수 있습니다.  
  
-   제약 조건은 표준화된 시스템 오류 메시지를 통해서만 오류를 알립니다. 응용 프로그램에서 사용자 지정 메시지와 더 복잡한 오류 처리가 필요하면 트리거를 사용해야 합니다.  
  
-   DML 트리거는 참조 무결성을 위반하는 변경 내용을 적용하지 않거나 롤백하여 데이터 수정을 취소할 수 있습니다. 이 트리거는 외래 키를 변경했는데 새 값이 기본 키와 일치하지 않을 때 적용됩니다. 그러나 이 작업에는 일반적으로 FOREIGN KEY 제약 조건을 사용합니다.  
  
-   트리거 테이블에 제약 조건이 있으면 INSTEAD OF 트리거가 실행된 후 AFTER 트리거가 실행되기 전에 제약 조건이 확인됩니다. 제약 조건을 위반하면 INSTEAD OF 트리거 동작이 롤백되고 AFTER 트리거가 실행되지 않습니다.  
  
## <a name="types-of-dml-triggers"></a>DML 트리거 유형  
 AFTER 트리거  
 INSERT, UPDATE, MERGE 또는 DELETE 문의 동작을 수행한 후에 AFTER 트리거를 실행합니다. 제약 조건을 위반하면 AFTER 트리거가 절대로 실행되지 않습니다. 따라서 제약 조건 위반이 발생할 수 있는 처리에 대해서는 이 트리거를 사용할 수 없습니다. MERGE 문에 지정된 INSERT, UPDATE 또는 DELETE 동작이 발생할 때마다 각 DML 동작에 대해 해당 트리거가 실행됩니다.  
  
 INSTEAD OF 트리거  
 INSTEAD OF 트리거는 트리거 문의 표준 동작을 무시합니다. 따라서 이 트리거를 사용하여 하나 이상의 열에서 오류나 값을 확인하고 행을 삽입, 업데이트 또는 삭제하기 전에 추가 동작을 수행할 수 있습니다. 예를 들어 임금 대장 테이블의 시간별 임금 열에서 업데이트되는 값이 지정된 값을 초과할 때 오류 메시지를 생성하거나 트랜잭션을 롤백하도록 트리거를 정의할 수 있습니다. 또는 임금 대장 테이블에 레코드를 삽입하기 전에 감사 내역에 새 레코드를 삽입하도록 트리거를 정의할 수 있습니다. INSTEAD OF 트리거의 주된 이점은 업데이트할 수 없는 뷰에 대해 업데이트를 지원한다는 것입니다. 예를 들어 여러 개의 기본 테이블로 구성된 뷰는 INSTEAD OF 트리거를 사용하여 여러 테이블의 데이터를 참조하는 삽입, 업데이트 및 삭제를 지원해야 합니다. INSTEAD OF 트리거의 또 다른 이점은 일괄 처리의 일부는 계속 처리하고 다른 일부는 처리하지 않도록 하는 논리를 코드화할 수 있게 한다는 것입니다.  
  
 이 표에서는 AFTER 트리거와 INSTEAD OF 트리거의 기능을 비교합니다.  
  
|함수|AFTER 트리거|INSTEAD OF 트리거|  
|--------------|-------------------|------------------------|  
|적용 대상|테이블|테이블 및 뷰|  
|각 테이블이나 뷰에서 가능한 트리거 수|각 트리거 동작(UPDATE, DELETE 및 INSERT)에 대해 여러 개 사용 가능|각 트리거 동작(UPDATE, DELETE 및 INSERT)에 대해 한 개만 사용 가능|  
|연계 참조|적용되는 제한 없음|연계 참조 무결성 제약 조건이 적용되는 테이블에는 INSTEAD OF UPDATE 트리거와 DELETE 트리거가 허용되지 않습니다.|  
|실행|이후:<br /><br /> 제약 조건 처리<br /><br /> 선언적 참조 동작<br /><br /> **inserted** 및 **deleted** 테이블 만들기<br /><br /> 트리거 동작|이전: 제약 조건 처리<br /><br /> 대신: 트리거 동작<br /><br /> 이후:  **inserted** 및 **deleted** 테이블 만들기|  
|실행 순서|첫 실행과 마지막 실행을 지정할 수 있음|해당 사항 없음|  
|**inserted**및 **deleted**테이블의 **varchar(max)** , **nvarchar(max)** 미 **varbinary(max)** 열 참조|허용함|허용함|  
|**inserted**및 **deleted**테이블의 **text** , **ntext** 및 **image** 열 참조|허용 안 됨|허용함|  
  
 CLR 트리거  
 CLR 트리거는 AFTER 또는 INSTEAD OF 트리거일 수 있습니다. 또한 CLR 트리거는 DDL 트리거일 수 있습니다. CLR 트리거는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 실행하는 대신 .NET Framework에서 생성되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업로드되는 어셈블리 멤버인 관리 코드로 작성된 하나 이상의 메서드를 실행합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크|항목|  
|----------|-----------|  
|DML 트리거를 만드는 방법에 대해 설명합니다.|[DML 트리거 만들기](../../relational-databases/triggers/create-dml-triggers.md)|  
|CLR 트리거를 만드는 방법에 대해 설명합니다.|[CLR 트리거 만들기](../../relational-databases/triggers/create-clr-triggers.md)|  
|단일 행 데이터 수정과 다중 행 데이터 수정을 모두 처리하는 DML 트리거를 만드는 방법에 대해 설명합니다.|[여러 행의 데이터를 처리하기 위한 DML 트리거 만들기](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)|  
|트리거를 중첩하는 방법에 대해 설명합니다.|[중첩 트리거 만들기](../../relational-databases/triggers/create-nested-triggers.md)|  
|AFTER 트리거가 발생되는 순서를 지정하는 방법에 대해 설명합니다.|[첫 번째 및 마지막 트리거 지정](../../relational-databases/triggers/specify-first-and-last-triggers.md)|  
|트리거 코드에서 특수 inserted 및 delete 테이블을 사용하는 방법에 대해 설명합니다.|[inserted 및 deleted 테이블 사용](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)|  
|DML 트리거를 수정하거나 이름을 변경하는 방법에 대해 설명합니다.|[DML 트리거 수정 또는 이름 바꾸기](../../relational-databases/triggers/modify-or-rename-dml-triggers.md)|  
|DML 트리거에 대한 정보를 보는 방법에 대해 설명합니다.|[DML 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-dml-triggers.md)|  
|DML 트리거 삭제하거나 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[DML 트리거 삭제 또는 해제](../../relational-databases/triggers/delete-or-disable-dml-triggers.md)|  
|트리거 보안을 관리하는 방법에 대해 설명합니다.|[트리거 보안 관리](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [트리거 함수&#40;Transact-SQL&#41;](../../t-sql/functions/trigger-functions-transact-sql.md)  
  
  
