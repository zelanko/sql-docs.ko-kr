---
title: "고유하게 컴파일된 저장 프로시저 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f0ebadeaa959c6eb148cdd9a9d6e0a1019d858ab
ms.openlocfilehash: 413be658a429308744b303d2d3ef82892c964c5a
ms.contentlocale: ko-kr
ms.lasthandoff: 07/27/2017

---
# <a name="creating-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저 만들기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  고유하게 컴파일된 저장 프로시저는 전체 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍 기능 및 쿼리 노출 영역을 구현하지 않습니다. 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 고유하게 컴파일된 저장 프로시저 내에서 사용할 수 없습니다. 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.  
  
 하지만 몇 가지 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능은 고유하게 컴파일된 저장 프로시저에서만 지원됩니다.  
  
-   ATOMIC 블록 자세한 내용은 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)을 참조하세요.  
  
-   매개 변수 및 변수에 대한 **NOT NULL** 제약 조건입니다. **NULL** 값을 **NOT NULL**로 선언된 매개 변수 또는 변수에 할당할 수 없습니다. 자세한 내용은 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)을 참조하세요.  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"**; -- *(값으로 초기화해야 함)*  
  
    -   SET @myVarchar **= null**; -- *(컴파일되지만 런타임 중에 실패함)*  
  
-   고유하게 컴파일된 저장 프로시저의 스키마 바인딩  
  
 고유하게 컴파일된 저장 프로시저는 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 사용하여 만듭니다. 다음 예에서는 메모리 액세스에 최적화된 테이블과 해당 테이블에 행을 삽입하는 데 사용되는 고유하게 컴파일된 저장 프로시저를 보여 줍니다.  
  
```tsql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 코드 샘플에서 **NATIVE_COMPILATION** 은 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저가 고유하게 컴파일된 저장 프로시저임을 나타냅니다. 다음 옵션이 필요합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|**SCHEMABINDING**|고유하게 컴파일된 저장 프로시저는 참조하는 개체의 스키마에 바인딩되어야 합니다. 이는 프로시저에서 참조하는 테이블을 삭제할 수 없음을 의미합니다. 프로시저에서 참조되는 테이블에는 해당 스키마 이름을 포함해야 하며 쿼리에 와일드카드(\*)를 사용할 수 없습니다( `SELECT * from...`을 의미하지 않음). **SCHEMABINDING** 은 이 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 고유하게 컴파일된 저장 프로시저에 대해서만 지원됩니다.|  
|**BEGIN ATOMIC**|고유하게 컴파일된 저장 프로시저의 본문은 단 하나의 ATOMIC 블록으로 구성되어야 합니다. ATOMIC 블록은 저장 프로시저의 원자성 실행을 보장합니다. 프로시저가 활성 트랜잭션의 컨텍스트 외부에서 호출되면 새 트랜잭션을 시작하며 ATOMIC 블록의 끝에서 커밋합니다. 고유하게 컴파일된 저장 프로시저의 ATOMIC 블록에는 다음과 같은 두 가지 필수 옵션이 있습니다.<br /><br /> **TRANSACTION ISOLATION LEVEL**입니다. 지원되는 격리 수준은 [메모리 액세스에 최적화된 테이블에 대한 트랜잭션 격리 수준](http://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) 을 참조하세요.<br /><br /> **LANGUAGE**입니다. 저장 프로시저의 언어는 사용 가능한 언어 또는 언어 별칭 중 하나로 설정되어야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  

