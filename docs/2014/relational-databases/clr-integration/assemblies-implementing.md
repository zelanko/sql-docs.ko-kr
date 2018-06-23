---
title: 어셈블리 구현 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: efd00348db3f4c92ad90f79e4e87094a542f1f95
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080018"
---
# <a name="implementing-assemblies"></a>어셈블리 구현
  이 항목에서는 사용자가 데이터베이스에서 어셈블리를 구현하고 사용하는 데 도움이 되는 다음 영역에 대해 설명합니다.  
  
-   어셈블리 만들기  
  
-   어셈블리 수정  
  
-   어셈블리 삭제, 해제 및 설정  
  
-   어셈블리 버전 관리  
  
## <a name="creating-assemblies"></a>어셈블리 만들기  
 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 문을 사용하여 만들고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 Assembly Assisted Editor를 사용하여 만듭니다. SQL Server 프로젝트를 배포 하는 또한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 프로젝트에 대해 지정 된 데이터베이스에 어셈블리를 등록 합니다. 자세한 내용은 [Deploying CLR Database Objects](deploying-clr-database-objects.md)을(를) 참조하세요.  
  
 **TRANSACT-SQL을 사용 하 여 어셈블리를 만들려면**  
  
-   [CREATE ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
 **SQL Server Management Studio를 사용 하 여 어셈블리를 만들려면**  
  
-   [어셈블리 속성 &#40;일반 페이지&#41;](assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>어셈블리 수정  
 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 문을 사용하여 수정하고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 Assembly Assisted Editor를 사용하여 수정합니다. 다음을 수행할 때 어셈블리를 수정할 수 있습니다.  
  
-   새로운 버전의 어셈블리 바이너리를 업로드하여 어셈블리 구현을 변경합니다. 자세한 내용은 참조 [어셈블리 버전 관리](#_managing) 이 항목의 뒷부분에 나오는 합니다.  
  
-   어셈블리의 권한 집합을 변경합니다. 자세한 내용은 [Designing Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)을 참조하세요.  
  
-   어셈블리의 표시 여부를 변경합니다. 표시되는 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 참조할 때 사용할 수 있습니다. 표시되지 않는 어셈블리는 데이터베이스에 업로드했더라도 사용할 수 없습니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 업로드된 어셈블리가 표시됩니다.  
  
-   해당 어셈블리와 관련된 디버그 또는 원본 파일을 추가하거나 삭제합니다.  
  
 **TRANSACT-SQL을 사용 하 여 어셈블리를 수정 하려면**  
  
-   [ALTER ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
 **SQL Server Management Studio를 사용 하 여 어셈블리를 수정 하려면**  
  
-   [어셈블리 속성 &#40;일반 페이지&#41;](assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>어셈블리 삭제, 해제 및 설정  
 어셈블리는 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY 문이나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 삭제합니다.  
  
 **TRANSACT-SQL을 사용 하 여 어셈블리를 삭제 하려면**  
  
-   [DROP ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **SQL Server Management Studio를 사용 하 여 어셈블리를 삭제 하려면**  
  
-   [개체 삭제](../../ssms/object/delete-objects.md)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성된 어셈블리는 모두 기본적으로 실행할 수 없습니다. 사용할 수는 **사용 하도록 설정 하는 clr** 옵션의는 **sp_configure** 시스템 저장 프로시저를 사용 하지 않도록 설정 하거나에 업로드 된 모든 어셈블리를 실행할 수 있게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 어셈블리 실행을 해제하면 CLR(공용 언어 런타임) 함수, 저장 프로시저, 트리거, 집계 및 사용자 정의 유형이 실행되지 않고 현재 실행 중인 경우 중지됩니다. 어셈블리 실행을 해제하더라도 어셈블리를 만들거나, 변경하거나, 삭제하는 기능은 해제되지 않습니다. 자세한 내용은 참조 [clr enabled 서버 구성 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)합니다.  
  
 **어셈블리 실행을 사용 하지 않도록 설정 하려면**  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
##  <a name="_managing"></a> 어셈블리 버전 관리  
 어셈블리가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 업로드되면 데이터베이스 시스템 카탈로그에 저장되어 이 카탈로그에서 관리됩니다. 에 있는 어셈블리의 정의에 대 한 변경 내용을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터베이스 카탈로그에 저장 되어 있는 어셈블리로 전파 되어야 합니다.  
  
 어셈블리를 수정해야 할 경우 ALTER ASSEMBLY 문을 실행하여 데이터베이스의 어셈블리를 업데이트해야 합니다. 이렇게 하면 어셈블리가 해당 구현을 보유하고 있는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 모듈의 최신 복사본으로 업데이트됩니다.  
  
 ALTER ASSEMBLY 문의 WITH UNCHECKED DATA 절은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 데이터베이스의 지속형 데이터가 종속되어 있는 어셈블리도 새로 고치도록 지시합니다. 특히 다음 중 하나가 존재하는 경우 WITH UNCHECKED DATA를 지정해야 합니다.  
  
-   어셈블리에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 메서드를 통해 직접 또는 간접적으로 메서드를 참조하는 지속형 계산 열  
  
-   어셈블리에 종속된 CLR 사용자 정의 유형의 열 - 이 유형은 **UserDefined**(비**네이티브**) 직렬화 형식을 구현합니다.  
  
> [!CAUTION]  
>  WITH UNCHECKED DATA를 지정하지 않으면 새 어셈블리 버전이 테이블, 인덱스 또는 다른 영구 사이트의 기존 데이터에 영향을 주는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ALTER ASSEMBLY를 실행하지 못하도록 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 업데이트할 때 계산 열, 인덱스, 인덱싱된 뷰 또는 식이 기본 루틴 및 유형과 일치하도록 보장하지는 않습니다. ALTER ASSEMBLY를 실행할 때는 어셈블리에 저장된 이 식을 기반으로 하는 값과 식의 결과가 일치하는지 주의해서 확인하십시오.  
  
 구성원만는 **db_owner** 및 **db_ddlowner** 고정된 데이터베이스 역할 WITH UNCHECKED DATA 절을 사용 하 여 ALTER ASSEMBLY를 실행할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 어셈블리가 테이블의 검사하지 않은 데이터로 수정되었다는 메시지를 Windows 응용 프로그램 이벤트 로그에 게시합니다. 그러면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 해당 어셈블리에 종속된 데이터가 들어 있는 테이블에 검사하지 않은 데이터가 있다고 표시합니다. **has_unchecked_assembly_data** 의 열은 **sys.tables** 카탈로그 뷰에 선택 되지 않은 데이터 및 검사 하지 않은 데이터가 없는 테이블에 대해 0이 포함 된 테이블에 대 한 값 1을 포함 합니다.  
  
 검사하지 않은 데이터의 무결성을 확인하려면 검사하지 않은 데이터가 있는 각 테이블에 대해 DBCC CHECKTABLE을 실행합니다. DBCC CHECKTABLE이 실패하면 잘못된 테이블 행을 삭제하거나 어셈블리 코드를 수정하여 문제를 해결한 다음 추가 ALTER ASSEMBLY 문을 실행해야 합니다.  
  
 ALTER ASSEMBLY는 어셈블리 버전을 변경합니다. 어셈블리의 문화권과 공개 키 토큰은 그대로 유지됩니다 .SQL Server는 동일한 이름, 문화권 및 공개 키를 사용하여 다른 버전의 어셈블리를 등록하는 것을 허용하지 않습니다.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>버전 바인딩을 위해 컴퓨터 차원의 정책과 상호 작용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장되어 있는 어셈블리에 대한 참조가 게시자 정책 또는 컴퓨터 차원의 관리자 정책을 사용하여 특정 버전으로 리디렉션된 경우에는 다음 중 하나를 수행해야 합니다.  
  
-   이렇게 리디렉션된 새 버전이 데이터베이스에 있는지 확인합니다.  
  
-   컴퓨터 또는 게시자 정책의 외부 정책 파일로 문을 수정하여 이러한 파일이 데이터베이스에 있는 특정 버전을 참조하는지 확인합니다.  
  
 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 새 어셈블리 버전을 로드할 수 없습니다.  
  
 **어셈블리의 버전을 업데이트 하려면**  
  
-   [ALTER ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [어셈블리 &#40;데이터베이스 엔진&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [어셈블리에 대한 정보 가져오기](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
