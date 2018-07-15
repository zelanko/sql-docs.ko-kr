---
title: 메모리 내 OLTP에 대한 SQL Server Management Studio 지원 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ee847b5f-6a1a-448e-a746-d61a023881ff
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 85dd4c829a05bd051fcf57f1ea299916080251a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313775"
---
# <a name="sql-server-management-studio-support-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 SQL Server Management Studio 지원
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라를 관리하기 위한 통합 환경입니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. 자세한 내용은 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md)를 참조하세요.  
  
 이 항목의 태스크에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 메모리 최적화 테이블, 메모리 최적화 테이블의 인덱스, 고유하게 컴파일된 저장 프로시저, 사용자 정의 메모리 최적화 테이블 형식을 관리하는 방법을 설명합니다.  
  
 프로그래밍 방식으로 메모리 최적화 테이블을 만드는 방법은 [메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)를 참조하세요.  
  
### <a name="to-create-a-database-with-a-memory-optimized-data-filegroup"></a>메모리 최적화 데이터 파일 그룹이 포함된 데이터베이스를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 클릭합니다.  
  
3.  새 메모리 최적화 데이터 파일 그룹을 추가하려면 **파일 그룹** 페이지를 클릭합니다. 
            **MEMORY OPTIMIZED DATA**아래에서 **파일 그룹 추가** 를 클릭한 다음 메모리 최적화 데이터 파일 그룹의 이름을 입력합니다.  **FILESTREAM 파일** 이라는 열에는 파일 그룹에 있는 컨테이너 수가 표시됩니다. 컨테이너는 **일반** 페이지에서 추가됩니다.  
  
4.  파일(컨테이너)를 파일 그룹에 추가하려면 **일반** 페이지를 클릭합니다. **데이터베이스 파일**아래에서 **추가**를 클릭합니다. 
            **파일 형식** 을 **FILESTREAM 데이터**로 선택하고 컨테이너의 논리적 이름을 지정한 다음 메모리 최적화 파일 그룹을 선택하고 **자동 증가/최대 크기** 가 **제한 없음**으로 설정되어 있는지 확인합니다.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 새 데이터베이스를 만드는 방법은 [데이터베이스 만들기](../databases/create-a-database.md)를 참조하세요.  
  
### <a name="to-create-a-memory-optimized-table"></a>메모리 최적화 테이블을 만들려면  
  
1.  **개체 탐색기**에서 데이터베이스의 **테이블** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **메모리 액세스에 최적화된 테이블**을 클릭합니다.  
  
     메모리 최적화 테이블을 만들기 위한 템플릿이 표시됩니다.  
  
2.  템플릿 매개 변수를 바꾸려면 **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정** 을 클릭합니다.  
  
     템플릿을 사용하는 방법은 [Template Explorer](../../ssms/template/template-explorer.md)를 참조하십시오.  
  
3.  
            **개체 탐색기**에서 테이블은 먼저 디스크 기반 테이블에 따라 정렬된 다음, 메모리 최적화 테이블에 따라 정렬됩니다. **개체 탐색기 정보** 를 사용하여 모든 테이블을 이름순으로 정렬합니다.  
  
### <a name="to-create-a-natively-compiled-stored-procedure"></a>고유하게 컴파일된 저장 프로시저를 만들려면  
  
1.  **개체 탐색기**에서 데이터베이스의 **저장 프로시저** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **고유하게 컴파일된 저장 프로시저**를 클릭합니다.  
  
     고유하게 컴파일된 저장 프로시저를 만들기 위한 템플릿이 표시됩니다.  
  
2.  템플릿 매개 변수를 바꾸려면 **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 클릭합니다.  
  
     새 저장 프로시저를 만드는 방법은 [Create a Stored Procedure](../stored-procedures/create-a-stored-procedure.md)를 참조하십시오.  
  
### <a name="to-create-a-user-defined-memory-optimized-table-type"></a>사용자 정의 메모리 최적화 테이블 형식을 만들려면  
  
1.  **개체 탐색기**에서 데이터베이스의 **형식** 노드를 확장하고 **사용자 정의 테이블 형식** 노드를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 클릭하고 **사용자 정의 메모리 액세스에 최적화된 테이블 형식**을 클릭합니다.  
  
     사용자 정의 메모리 최적화 테이블 형식을 만들기 위한 템플릿이 표시됩니다.  
  
2.  템플릿 매개 변수를 바꾸려면 **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정** 을 클릭합니다.  
  
     새 저장 프로시저를 만드는 방법은 [CREATE TYPE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)을 참조하세요.  
  
## <a name="memory-monitoring"></a>메모리 모니터링  
  
#### <a name="view-memory-usage-by-memory-optimized-objects-report"></a>메모리 액세스에 최적화된 개체별 메모리 사용량 보고서 보기  
  
-   **개체 탐색기**에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **보고서**, **표준 보고서**, **메모리 액세스에 최적화된 개체별 메모리 사용량**을 차례로 클릭합니다.  
  
     이 보고서는 데이터베이스에 있는 메모리 최적화 개체의 메모리 공간 사용률에 대한 자세한 데이터를 제공합니다.  
  
#### <a name="view-properties-for-allocated-and-used-memory-for-a-table-database"></a>테이블 또는 데이터베이스에 대해 할당되고 사용된 메모리에 대한 속성 보기  
  
1.  메모리 내 사용량에 대한 정보를 가져오려면 다음과 같이 하십시오.  
  
    -   
            **개체 탐색기**에서 메모리 최적화 테이블을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **저장소** 페이지를 클릭합니다. **데이터 공간** 속성에 대한 값은 테이블에 있는 데이터가 사용하는 메모리를 나타냅니다. **인덱스 공간** 속성에 대한 값은 테이블의 인덱스가 사용하는 메모리를 나타냅니다.  
  
    -   **개체 탐색기**에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **일반** 페이지를 클릭합니다. 
            **메모리 최적화 개체에 할당된 메모리** 속성에 대한 값은 데이터베이스에 있는 메모리 최적화 개체에 할당된 메모리를 나타냅니다. 
            **메모리 최적화 개체가 사용하는 메모리** 속성에 대한 값은 데이터베이스에 있는 메모리 최적화 개체가 사용하는 메모리를 나타냅니다.  
  
## <a name="supported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>다음에서 지원되는 기능 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 
            [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 메모리 최적화 데이터 파일 그룹, 메모리 최적화 테이블, 인덱스 및 고유하게 컴파일된 저장 프로시저가 포함된 데이터베이스에서 데이터베이스 엔진이 지원하는 기능과 작업을 지원합니다.  
  
 데이터베이스, 테이블, 저장 프로시저, 사용자 정의 테이블 형식 또는 인덱스 개체에 대해 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 기능이 메모리 내 OLTP를 지원하도록 업데이트되었거나 확장되었습니다.  
  
-   개체 탐색기  
  
    -   상황에 맞는 메뉴  
  
    -   필터 설정  
  
    -   스크립팅  
  
    -   태스크  
  
    -   보고서  
  
    -   속성  
  
    -   데이터베이스 태스크:  
  
        -   메모리 최적화 테이블이 포함된 데이터베이스 연결 및 분리  
  
             
            **데이터베이스 연결** 사용자 인터페이스는 메모리 최적화 데이터 파일 그룹을 표시하지 않습니다. 그러나 데이터베이스 연결은 계속 진행할 수 있으며 데이터베이스는 올바르게 연결됩니다.  
  
            > [!NOTE]  
            >  
            [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 메모리 최적화 데이터 파일 그룹 컨테이너가 있는 데이터베이스를 연결하려고 하는데 데이터베이스의 메모리 최적화 데이터 파일 그룹 컨테이너가 다른 컴퓨터에서 만든 것이라면 메모리 최적화 데이터 파일 그룹 컨테이너의 위치가 두 컴퓨터에서 동일해야 합니다. 데이터베이스의 메모리 최적화 데이터 파일 그룹 컨테이너 위치를 새 컴퓨터에서 다르게 지정하려는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스를 연결할 수 있습니다. 다음 예에서 새 컴퓨터의 메모리 최적화 데이터 파일 그룹 컨테이너 위치는 C:\Folder2입니다. 그러나 첫 번째 컴퓨터에서 메모리 최적화 데이터 파일 그룹 컨테이너가 생성된 위치는 C:\Folder1입니다.  
            >   
            >  `CREATE DATABASE[imoltp] ON`  
            >   
            >  `(NAME =N'imoltp',FILENAME=N'C:\Folder2\imoltp.mdf'),`  
            >   
            >  `(NAME =N'imoltp_mod1',FILENAME=N'C:\Folder2\imoltp_mod1'),`  
            >   
            >  `(NAME =N'imoltp_log',FILENAME=N'C:\Folder2\imoltp_log.ldf')`  
            >   
            >  `FOR ATTACH`  
            >   
            >  `GO`  
  
        -   스크립트 생성  
  
             **스크립트 생성 및 게시 마법사**에서 **개체의 존재 여부 확인** 스크립팅 옵션의 기본값은 FALSE입니다. **개체의 존재 여부 확인** 스크립팅 옵션의 값을 마법사의 **스크립팅 옵션 설정** 화면에서 TRUE로 설정하면 생성되는 스크립트에는 "CREATE PROCEDURE <procedure_name> AS" 및 "ALTER PROCEDURE <procedure_name> <procedure_definition>"이 포함됩니다. 고유하게 컴파일된 저장 프로시저에서는 ALTER PROCEDURE가 지원되지 않으므로 생성된 스크립트를 실행하면 오류가 반환됩니다.  
  
             각각의 고유하게 컴파일된 저장 프로시저에 대해 생성되는 스크립트를 변경하려면 다음을 수행합니다.  
  
            1.  "CREATE PROCEDURE <procedure_name> AS"에서 "AS"를 "<procedure_definition>"으로 바꿉니다.  
  
            2.  "ALTER PROCEDURE <procedure_name> <procedure_definition>"을 삭제합니다.  
  
        -   데이터베이스 복사. 메모리 최적화 개체가 포함된 데이터베이스의 경우 대상 서버에서 데이터베이스 만들기 및 데이터 전송이 트랜잭션 내에서 실행되지 않습니다.  
  
        -   데이터 가져오기 및 내보내기. **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사 하나 이상의 테이블 또는 뷰에서 데이터 복사** 옵션을 사용합니다. 대상 테이블이 대상 데이터베이스에 존재하지 않는 메모리 최적화 테이블인 경우:  
  
            1.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사**의 **테이블 복사 또는 쿼리 지정** 화면에서 **하나 이상의 테이블 또는 뷰에서 데이터 복사**를 선택합니다. 그런 후 **다음**을 클릭합니다.  
  
            2.  **매핑 편집**을 클릭합니다. 그런 다음 **대상 테이블 만들기** 를 선택하고 **SQL 편집**을 클릭합니다. 대상 데이터베이스에서 메모리 최적화 테이블을 만드는 CREATE TABLE 구문을 입력합니다. **확인** 을 클릭하고 마법사의 나머지 단계를 완료합니다.  
  
        -   유지 관리 계획. 유지 관리 태스크인 인덱스 다시 구성 및 인덱스 다시 작성은 메모리 최적화 테이블과 해당 인덱스에서 지원되지 않습니다. 따라서 인덱스 다시 작성 및 인덱스 다시 구성에 대한 유지 관리 계획을 실행하면 선택한 데이터베이스에서 메모리 최적화 테이블과 해당 인덱스가 생략됩니다.  
  
             유지 관리 태스크 업데이트 통계는 메모리 최적화 테이블과 해당 인덱스에 대한 예제 검사에서 지원되지 않습니다. 따라서 통계 업데이트에 대한 유지 관리 계획을 실행하면 메모리 최적화 테이블과 해당 인덱스에 대한 통계는 항상 `WITH FULLSCAN, NORECOMPUTE`로 업데이트됩니다.  
  
-   개체 탐색기 정보 창  
  
-   Template Explorer  
  
## <a name="unsupported-features-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>다음에서 지원되지 않는 기능 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 메모리 내 OLTP 개체의 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 데이터베이스 엔진이 지원하지 않는 기능과 작업을 지원하지 않습니다.  
  
 지원 되지 않는 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 참조 하세요 [지원 되는 SQL Server 기능](unsupported-sql-server-features-for-in-memory-oltp.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP에 대한 SQL Server 지원](sql-server-support-for-in-memory-oltp.md)  
  
  
