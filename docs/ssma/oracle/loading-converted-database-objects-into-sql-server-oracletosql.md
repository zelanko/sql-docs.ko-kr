---
title: 데이터베이스 개체를 SQL Server (OracleToSQL)로 변환 된 로드 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 26ac7029947dcf826c19851b5988b5e898783f7c
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777619"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>데이터베이스 개체를 SQL Server (OracleToSQL)로 변환 된 로드
SQL Server로 Oracle 스키마를 변환한 후 결과 데이터베이스 개체를 SQL Server로 로드할 수 있습니다. 개체를 만들 SSMA를 포함할 수 있고 개체를 스크립팅 합니다 스크립트를 실행할 수 있습니다. 또한 SSMA SQL Server 데이터베이스의 실제 내용과 대상 메타 데이터를 업데이트할 수 있습니다.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>동기화 및 스크립트 중에서 선택  
수정 하지 않고 SQL Server로 변환 된 데이터베이스 개체를 로드 하려면 SSMA를 직접 만들거나 데이터베이스 개체를 다시 만들 수도 있습니다. 메서드는 빠르고 쉬우며, 하지만의 사용자 지정이 가능 하지 않습니다는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 저장된 프로시저 외 SQL Server 개체를 정의 하는 코드입니다.  
  
수정 하려는 경우는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 개체를 만들거나 개체를 만드는 자세한 제어 하려면 SSMA를 사용 하 여 스크립트를 만드는 데 사용 되는 합니다. 그런 다음 해당 스크립트를 수정 하, 각 개체를 개별적으로 만들,도 SQL Server 에이전트를 사용 하 여 해당 개체를 만들고 예약할 수입니다.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA를 사용 하 여 SQL Server와 함께 개체를 동기화 하려면  
SQL Server 데이터베이스 개체를 만드는 SSMA를 사용 하려면 개체 SQL Server 메타 데이터 탐색기에서 선택한 다음 다음 절차에 나와 있는 것 처럼 SQL Server와 함께 개체를 동기화 합니다. 기본적으로 SQL Server에 개체가 이미 존재 하 고 SSMA 메타 데이터를 SQL Server에서 개체 보다 최신인 경우 SSMA 변경 SQL Server에 있는 개체 정의. 편집 하 여 기본 동작을 변경할 수 있습니다 **프로젝트 설정**합니다.  
  
> [!NOTE]  
> Oracle 데이터베이스에서 변환 되지 않은 기존 SQL Server 데이터베이스 개체를 선택할 수 있습니다. 그러나 이러한 개체는 다시 작성 또는 수 SSMA에 의해 변경.  
  
**SQL Server와 함께 개체를 동기화 하려면**  
  
1.  SQL Server 메타 데이터 탐색기에서 위쪽 SQL Server 노드를 확장 한 다음 확장 **데이터베이스**합니다.  
  
2.  처리할 개체를 선택 합니다.  
  
    -   전체 데이터베이스를 동기화 하려면 데이터베이스 이름 옆에 있는 확인란을 선택 합니다.  
  
    -   동기화 하거나 생략 개별 개체 또는 개체의 범주를 선택 하거나 개체 또는 폴더 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  SQL Server 메타 데이터 탐색기에서 처리할 개체를 선택한 후 마우스 오른쪽 단추로 클릭 **데이터베이스**, 클릭 하 고 **데이터베이스와 동기화**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 개별 개체 또는 개체 범주의 동기화도 **데이터베이스와 동기화**합니다.  
  
    그 후 SSMA 표시 됩니다는 **데이터베이스와 동기화** 대화 상자에서 두 개의 항목 그룹이 확인할 수 있습니다. 왼쪽에서 SSMA 트리에 표시 되는 선택한 데이터베이스 개체를 표시 합니다. 오른쪽에서 SSMA 메타 데이터에 동일한 개체를 나타내는 트리를 볼 수 있습니다. 있습니다 수 왼쪽 이나 오른쪽을 클릭 하 여 트리를 확장 합니다. ' +' 단추입니다. 동기화 방향 두 트리 사이 배치 작업 열에 표시 됩니다.  
  
    작업 기호는 세 가지 상태로 될 수 있습니다.  
  
    -   왼쪽된 화살표 메타 데이터의 내용을 (기본값) 데이터베이스에 저장할 것을 의미 합니다.  
  
    -   오른쪽 화살표 데이터베이스 내용 SSMA 메타 데이터를 덮어씁니다를 의미 합니다.  
  
    -   교차 기호 아무 작업도 수행 될 것을 의미 합니다.  
  
상태를 변경 하려면 작업 기호를 클릭 합니다. 클릭할 때 실제 동기화가 수행 **확인** 의 단추는 **데이터베이스와 동기화** 대화 상자.  
  
## <a name="scripting-objects"></a>스크립팅 개체  
저장 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 변환 된 데이터베이스 개체 또는 개체 정의 변경 하 고 스크립트를 실행 하려면 정의 저장할 수 있습니다 변환된 데이터베이스 개체 정의를 [!INCLUDE[tsql](../../includes/tsql_md.md)] 스크립트입니다.  
  
**스크립트 개체를 저장 하려면**  
  
1.  사용자가 스크립트에 저장 하는 개체를 선택한 후 마우스 오른쪽 단추로 클릭 **데이터베이스**, 클릭 하 고 **스크립트로 저장**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 개별 개체 또는 개체 범주의 스크립팅하여 수도 **스크립트로 저장**합니다.  
  
2.  에 **다른 이름으로 저장** 대화 상자에서에 파일 이름을 입력 하는 스크립트를 저장 하려는 폴더를 찾습니다는 **파일 이름** 상자를 선택한 다음 클릭 확인 SSMA.sql 파일 이름 확장명을 추가 합니다.  
  
### <a name="modifying-scripts"></a>스크립트 수정  
사용할 수 있는 SQL Server 개체 정의 하나 이상의 스크립트 저장 한 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 를 보고 하는 스크립트를 수정 합니다.  
  
**스크립트를 수정 하려면**  
  
1.  에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **파일** 메뉴에서 **열려**, 클릭 하 고 **파일**합니다.  
  
2.  에 **열려** 대화 상자에서 스크립트 파일을 선택 하 고 확인을 클릭 합니다.
  
3.  쿼리 편집기를 사용 하 여 스크립트 파일을 편집 합니다.  
  
    쿼리 편집기에 대 한 자세한 내용은 "편집기 편의 명령 및 기능" SQL Server 온라인 설명서의를 참조 하십시오.  
  
4.  파일 메뉴에서 스크립트를 저장 하려면 **저장**합니다.  
  
### <a name="running-scripts"></a>스크립트 실행  
스크립트 또는 개별 문을에서 실행할 수 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]합니다.  
  
**스크립트를 실행 하려면**  
  
1.  에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **파일** 메뉴에서 **열려**, 클릭 하 고 **파일**합니다.  
  
2.  에 **열려** 대화 상자에서 스크립트 파일을 선택한 다음 확인을 클릭  
  
3.  전체 스크립트를 실행 하려면는 **F5** 키입니다.  
  
4.  문 집합을 실행 하려면 쿼리 편집기 창에서 문을 선택 하 고 다음 키를 누릅니다는 **F5** 키입니다.  
  
스크립트를 실행 하려면 쿼리 편집기를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] 쿼리"에서 SQL Server 온라인 설명서.  
  
사용 하 여 명령줄에서 스크립트를 실행할 수도 있습니다는 **sqlcmd** 유틸리티 및 SQL Server 에이전트에서 합니다. 에 대 한 자세한 내용은 **sqlcmd**, SQL Server 온라인 설명서의 "sqlcmd 유틸리티"를 참조 하십시오. SQL Server 에이전트에 대 한 자세한 내용은 "자동화 Administrative Tasks (SQL Server Agent)" SQL Server 온라인 설명서의를 참조 하십시오.  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server 개체의에서 보안 설정  
SQL Server로 변환 된 데이터베이스 개체를 로드 하면 부여 하거나 해당 개체에 대 한 권한을 거부할 수 있습니다. 마이그레이션하기 전에이 작업을 수행 하는 것이 좋습니다 데이터를 SQL Server. SQL Server에서 개체를 보호 하는 방법에 대 한 내용은 "보안 고려 사항에 대 한 데이터베이스 및 데이터베이스 응용 프로그램"에서 SQL Server 온라인 설명서를 참조 하십시오.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 [데이터를 SQL Server로 마이그레이션](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server로 데이터베이스 마이그레이션 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
