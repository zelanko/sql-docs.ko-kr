---
title: 고유하게 컴파일된 저장 프로시저 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9525ef65973baa38ae19ba4681e4a93f949c004a
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531135"
---
# <a name="creating-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저 만들기
  고유하게 컴파일된 저장 프로시저는 전체 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍 기능 및 쿼리 노출 영역을 구현하지 않습니다. 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 고유하게 컴파일된 저장 프로시저 내에서 사용할 수 없습니다. 자세한 내용은 [Natively Compiled Stored Procedures에서 지원 되는 구문](../in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)합니다.  
  
 하지만 몇 가지 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능은 고유하게 컴파일된 저장 프로시저에서만 지원됩니다.  
  
-   ATOMIC 블록 자세한 내용은 [Atomic Blocks](atomic-blocks-in-native-procedures.md)을(를) 참조하십시오.  
  
-   고유하게 컴파일된 저장 프로시저에서 매개 변수와 변수에 대한 `NOT NULL` 제약 조건. `NULL` 값을 `NOT NULL`로 선언된 매개 변수 또는 변수에 할당할 수 없습니다. 자세한 내용은 [DECLARE @local_variable&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)을 참조하세요.  
  
-   고유하게 컴파일된 저장 프로시저의 스키마 바인딩  
  
 고유하게 컴파일된 저장 프로시저는 [CREATE PROCEDURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)를 사용하여 만듭니다. 다음 예에서는 메모리 최적화 테이블과 해당 테이블에 행을 삽입하는 데 사용되는 고유하게 컴파일된 저장 프로시저를 보여 줍니다.  
  
```sql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding, execute as owner  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 코드 샘플에서 `NATIVE_COMPILATION`은 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저가 고유하게 컴파일된 저장 프로시저임을 나타냅니다. 다음 옵션이 필요합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|`SCHEMABINDING`|고유하게 컴파일된 저장 프로시저는 참조하는 개체의 스키마에 바인딩되어야 합니다. 이는 프로시저에서 참조하는 테이블을 삭제할 수 없음을 의미합니다. 프로시저에서 참조 하는 테이블의 스키마 이름 및 와일드 카드를 포함 해야 합니다 (\*) 쿼리에서 허용 되지 않습니다. `SCHEMABINDING`은 이 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 고유하게 컴파일된 저장 프로시저에 대해서만 지원됩니다.|  
|`EXECUTE AS`|고유하게 컴파일된 저장 프로시저는 기본 실행 컨텍스트인 `EXECUTE AS CALLER`를 지원하지 않습니다. 따라서 실행 컨텍스트를 지정해야 합니다. 옵션 `EXECUTE AS OWNER`하십시오 `EXECUTE AS` *사용자*, 및 `EXECUTE AS SELF` 지원 됩니다.|  
|`BEGIN ATOMIC`|고유하게 컴파일된 저장 프로시저의 본문은 단 하나의 ATOMIC 블록으로 구성되어야 합니다. ATOMIC 블록은 저장 프로시저의 원자성 실행을 보장합니다. 프로시저가 활성 트랜잭션의 컨텍스트 외부에서 호출되면 새 트랜잭션을 시작하며 ATOMIC 블록의 끝에서 커밋합니다. 고유하게 컴파일된 저장 프로시저의 ATOMIC 블록에는 다음과 같은 두 가지 필수 옵션이 있습니다.<br /><br /> `TRANSACTION ISOLATION LEVEL`에서 분할된 테이블 또는 인덱스를 만들 수 있습니다. 참조 [트랜잭션 격리 수준](../../database-engine/transaction-isolation-levels.md) 격리 수준을 지원 합니다.<br /><br /> `LANGUAGE`에서 분할된 테이블 또는 인덱스를 만들 수 있습니다. 저장 프로시저의 언어는 사용 가능한 언어 또는 언어 별칭 중 하나로 설정되어야 합니다.|  
  
 `EXECUTE AS` 및 Windows 로그인과 관련하여 `EXECUTE AS`를 통해 수행된 가장 때문에 오류가 발생할 수 있습니다. 사용자 계정이 Windows 인증을 사용하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 사용되는 서비스 계정과 Windows 로그인의 도메인 간에는 완전 신뢰 관계가 있어야 합니다. 완전 신뢰 관계가 없는 경우 고유하게 컴파일된 저장 프로시저를 만들 때 메시지 15404, Windows NT 그룹/사용자 'username', 오류 코드 0x5에 대 한 정보를 가져올 수 없습니다.  
  
 이 오류를 해결하려면 다음 중 하나를 사용합니다.  
  
-   Windows 사용자와 동일한 도메인에 있는 계정을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스에 사용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 네트워크 서비스 또는 로컬 시스템과 같은 시스템 계정을 사용하는 경우 해당 컴퓨터가 Windows 사용자가 포함된 도메인에서 트러스트되어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용합니다.  
  
 고유하게 컴파일된 저장 프로시저를 만들 때 오류 15517이 나타날 수도 있습니다. 자세한 내용은 [MSSQLSERVER_15517](../errors-events/mssqlserver-15517-database-engine-error.md)합니다.  
  
## <a name="updating-a-natively-compiled-stored-procedure"></a>고유하게 컴파일된 저장 프로시저 업데이트  
 고유하게 컴파일된 저장 프로시저에 대한 변경 작업 수행은 지원되지 않습니다. 고유하게 컴파일된 저장 프로시저를 수정하는 한 가지 방법은 저장 프로시저를 삭제하고 다시 만드는 것입니다.  
  
1.  저장 프로시저 사용 권한에 대한 스크립트를 생성합니다.  
  
2.  선택적으로 저장 프로시저에 대한 스크립트를 생성하고 백업으로 저장합니다.  
  
3.  저장 프로시저를 삭제합니다.  
  
4.  변경된 저장 프로시저를 만듭니다.  
  
5.  스크립팅된 사용 권한을 저장 프로시저에 다시 적용합니다.  
  
 이 절차의 단점은 3단계 시작과 5단계 완료 사이에 오프라인 시간이 있다는 것입니다. 이 작업은 몇 초 정도 걸릴 수 있으며 응용 프로그램을 사용하는 클라이언트에 오류 메시지가 표시될 수 있습니다.  
  
 고유하게 컴파일된 저장 프로시저를 효과적으로 수정하는 다른 방법은 먼저 저장 프로시저의 새 버전을 만드는 것입니다. 여기서 고유하게 컴파일된 저장 프로시저에는 연결된 버전 번호가 있습니다. 기존 버전을 SP_Vold라고 하고 새 버전을 SP_Vnew라고 합니다.  
  
1.  SP_Vold의 사용 권한에 대한 스크립트를 생성합니다.  
  
2.  SP_Vnew를 만듭니다.  
  
3.  SP_Vold의 사용 권한을 SP_Vnew에 적용합니다.  
  
4.  SP_Vnew를 가리키도록 SP_Vold에 대한 참조를 업데이트합니다. 이 작업은 다음과 같은 다양한 방법으로 수행할 수 있습니다.  
  
     래퍼(디스크 기반) 저장 프로시저를 사용하고 SP_Vnew를 가리키도록 해당 프로시저를 변경합니다. 이 방법의 단점은 간접 참조가 성능에 미치는 영향입니다.  
  
    ```sql  
    ALTER PROCEDURE dbo.SP p1,...,pn  
    AS  
      EXEC dbo.SP_Vnew p1,...,pn  
    GO  
    ```  
  
5.  선택적으로 SP_Vold를 삭제합니다.  
  
 이 방법의 장점은 응용 프로그램이 오프라인으로 전환되지 않는다는 것입니다. 하지만 참조를 유지하고 참조가 항상 최신 버전의 저장 프로시저를 가리키는지 확인하는 데 더 많은 작업이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)  
  
  
