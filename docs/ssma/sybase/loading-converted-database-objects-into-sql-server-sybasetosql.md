---
title: 변환 된 로드 된 데이터베이스 개체를 SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96e2bee47c97e85421b074e870c9dab1dd46220a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245893"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>변환된 데이터베이스 개체를 SQL Server로 로드(SybaseToSQL)
Sybase 적응형 Server Enterprise (ASE) 데이터베이스 개체를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 결과 데이터베이스 개체를 로드할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 개체를 만드는 SSMA를 포함할 수 있습니다 또는 개체를 스크립팅 합니다 하 고 직접 스크립트를 실행할 수 있습니다. SSMA의 실제 콘텐츠를 사용 하 여 대상 메타 데이터를 업데이트할 수 있습니다 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>동기화 및 스크립트 선택  
변환 된 데이터베이스 개체를 로드 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 수정 하지 않고 SQL Azure 직접 만들거나 데이터베이스 개체를 다시 만들고 SSMA 있을 수 있습니다. 이 메서드는 빠르고 쉬우며 하지만 사용자 지정을 허용 하지 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 정의 하는 코드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 저장된 프로시저 외의 SQL Azure 개체입니다.  
  
수정 하려는 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 개체를 만드는 데 사용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체에서 만들어진 시기와 방법을 더 제어 하려는 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure, SSMA를 만드는 데 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트입니다. 그런 다음 해당 스크립트를 수정, 각 개체를 개별적으로 만드는 고 사용할 수 있습니다도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 해당 개체 만들기를 예약 하려면 SQL Azure 에이전트입니다.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>SSMA를 사용 하 여 개체를 SQL Server 또는 SQL Azure 로드  
SSMA를 만드는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 개체의 개체를 선택 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기를 다음 사용 하 여 개체를 동기화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure, 다음 절차에 표시 된 대로 합니다. 기본적으로 개체에 이미 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure SSMA 메타 데이터에 일부 로컬 변경 내용 또는 매우 해당 개체의 정의에 대 한 업데이트 경우 SSMA에서 개체 정의 변경 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 편집 하 여 기본 동작을 변경할 수 있습니다 **프로젝트 설정**합니다.  
  
> [!NOTE]  
> 기존 선택할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 ASE 데이터베이스에서 변환 되지 않은 SQL Azure 데이터베이스 개체입니다. 그러나 개체만 하지 다시 만들어지거나 SSMA에 의해 변경 합니다.  
  
**SQL Server 또는 SQL Azure 사용 하 여 개체를 동기화 하려면**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기의 맨 위에 확장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 노드를 펼친 다음 **데이터베이스**합니다.  
  
2.  처리할 개체를 선택 합니다.  
  
    -   전체 데이터베이스를 동기화 하려면 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
    -   동기화 또는 개별 개체 또는 개체 범주의 생략을 선택 하거나 개체 또는 폴더 옆의 확인란의 선택을 취소 합니다.  
  
3.  개체의 처리를 선택한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 메타 데이터 탐색기를 마우스 오른쪽 단추로 클릭 **데이터베이스**를 클릭 하 고 **데이터베이스와 동기화**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 하 여 개별 개체 또는 개체 범주의 동기화 수도 **데이터베이스와 동기화**합니다.  
  
    그 후 SSMA 표시 됩니다는 **데이터베이스와 동기화** 대화 상자에서 항목의 두 그룹을 볼 수 있는 합니다. 왼쪽된에 있는 SSMA 트리에서 선택한 데이터베이스 개체가 표시 됩니다. 오른쪽에서 동일한 SSMA 메타 데이터 개체를 나타내는 트리를 볼 수 있습니다. 있습니다 수 왼쪽 또는 오른쪽 클릭 하 여 트리를 확장 합니다. ' +' 단추입니다. 동기화 방향은 두 트리 사이 배치 된 작업 열에 표시 됩니다.  
  
    동작 기호는 다음 세 가지 상태일에서 수 있습니다.  
  
    -   왼쪽된 화살표 (기본값) 데이터베이스의 메타 데이터의 콘텐츠를 저장할 것을 의미 합니다.  
  
    -   오른쪽 화살표 데이터베이스 내용을 SSMA 메타 데이터를 덮어씁니다를 의미 합니다.  
  
    -   교차 기호를 아무 작업도 수행할 것을 의미 합니다.  
  
동작 기호 상태를 변경 하려면 클릭 합니다. 클릭 하면 실제 동기화가 수행 됩니다 **확인** 단추를 **데이터베이스와 동기화** 대화 합니다.  
  
## <a name="scripting-objects"></a>스크립팅 개체  
저장 하려는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변환 된 데이터베이스 개체의 정의 개체 정의 변경 하려면 직접 스크립트를 실행 하 고 변환된 된 데이터베이스의 개체 정의를 저장할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트입니다.  
  
**스크립트 개체를 저장 하려면**  
  
1.  사용자가 스크립트를 저장 하려면 개체를 선택한 후 마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **스크립트로 저장**합니다.  
  
    개체 또는 해당 포함 된 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체 또는 개체의 범주를 스크립팅할 수도 있습니다 **스크립트 저장**합니다.  
  
2.  에 **다른 이름으로 저장** 대화 상자에서 입력에서 파일 이름을 스크립트를 저장 하려는 폴더를 찾습니다는 **파일 이름** 상자를 선택한 다음 클릭 **확인**합니다.  
  
    SSMA는.sql 파일 이름 확장명을 추가 합니다.  
  
### <a name="modifying-scripts"></a>스크립트를 수정합니다.  
저장 한 후는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 사용할 수 있습니다 하나 이상의 스크립트와 SQL Azure 개체 정의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 보고 하는 스크립트를 수정 합니다.  
  
**스크립트를 수정 하려면**  
  
1.  에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **파일** 메뉴에서 **열기**를 클릭 하 고 **파일**합니다.  
  
2.  에 **엽니다** 대화 상자에서 스크립트 파일을 선택 및 클릭 한 다음 이동할 **확인**.  
  
3.  편집 및 쿼리 편집기를 사용 하 여 스크립트 파일입니다.  
  
    쿼리 편집기에 대 한 자세한 내용은의 "편집기 편의 명령 및 기능" 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
4.  파일 메뉴에서 스크립트를 저장 하려면 선택 **저장할**합니다.  
  
### <a name="running-scripts"></a>스크립트를 실행합니다.  
스크립트 또는 개별 문을에서 실행할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
**스크립트를 실행 하려면**  
  
1.  에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **파일** 메뉴에서 **열기**를 클릭 하 고 **파일**합니다.  
  
2.  에 **엽니다** 대화 상자에서 스크립트 파일을 선택 및 클릭 한 다음 이동할 **확인**.  
  
3.  키를 눌러 전체 스크립트를 실행 하는 **F5** 키입니다.  
  
4.  문 집합을 실행 하려면 쿼리 편집기 창에 문을 선택 하 고 다음 키를 누릅니다 합니다 **F5** 키입니다.  
  
쿼리 편집기를 사용 하 여 스크립트를 실행 하는 방법에 대 한 자세한 내용은 참조 하세요. " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리"에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
사용 하 여 명령줄에서 스크립트를 실행할 수도 있습니다는 **sqlcmd** 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트입니다. 에 대 한 자세한 내용은 **sqlcmd**에서 "sqlcmd 유틸리티"를 참조 하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 "관리 태스크 자동화 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트)"에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server의 보안 개체  
변환 된 데이터베이스 개체를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 부여 하거나 해당 개체에 대 한 권한을 거부할 수 있습니다. 마이그레이션하기 전에이 작업을 수행 하는 것이 좋습니다 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. 개체를 보호 하는 방법에 대 한 정보에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 "보안 고려 사항에 대 한 데이터베이스 및 데이터베이스 응용 프로그램"을 참조 하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스에서 다음 단계 [Sybase ASE 데이터를 SQL Server로 마이그레이션 / SQL Azure(SybaseToSQL)](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)합니다.  
  
## <a name="see-also"></a>관련 항목  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
