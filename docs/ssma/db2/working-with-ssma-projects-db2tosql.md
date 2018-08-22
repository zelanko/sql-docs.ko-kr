---
title: SSMA 프로젝트 (DB2ToSQL) 작업 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7f10a1fa9faf04e8f819acd7966f6ca6d03c57b5
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40395540"
---
# <a name="working-with-ssma-projects-db2tosql"></a>SSMA 프로젝트 (DB2ToSQL) 작업
DB2 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA 프로젝트를 만들어야 합니다. 프로젝트는 다음 정보를 포함 하는 파일:  
  
-   메타 데이터를 마이그레이션하려는 DB2 데이터베이스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
-   대상 인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 개체 및 데이터를 수신 하는 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보입니다.  
  
-   프로젝트 설정입니다.  
  
프로젝트를 열 때 DB2에서 연결이 끊어지도록 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. 에 다시 연결 하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server에 연결 &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)합니다.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정을 검토합니다.  
SSMA 변환 및 데이터베이스 개체를 로드, 데이터 마이그레이션 및 DB2와 함께 SSMA를 동기화에 대 한 몇 가지 설정을 포함 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. 기본 설정은 많은 사용자에 게 적합 합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 설정을 검토 해야 합니다. 를 하려는 경우에 모든 새 프로젝트에 사용할 기본 설정을 변경할 수 있습니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  에 **도구** 메뉴에서 클릭 **기본 프로젝트 설정**합니다.  
  
2.  라는 프로젝트 형식을 선택 **마이그레이션 대상 버전** 설정을 보거나 변경 하는 데 필요한 되며 클릭에 대 한 드롭다운 **일반** 탭 합니다.  
  
3.  왼쪽된 창에서 클릭 **변환**합니다.  
  
4.  오른쪽 창에서 검토 하 고 필요에 따라 설정을 변경 합니다. 이러한 설정에 대 한 자세한 내용은 참조 하세요. [프로젝트 설정 &#40;변환&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)합니다.  
  
5.  마이그레이션, 동기화, 시스템 개체 로드, GUI 및 형식 매핑 페이지에 대해 1-3 단계를 반복 합니다.  
  
    -   마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;마이그레이션&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)합니다.  
  
    -   시스템 개체 설정에 대 한 정보를 참조 하세요 [프로젝트 설정&#40;시스템 개체 로드&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)합니다.  
  
    -   동기화에 대 한 설정에 대 한 자세한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [프로젝트 설정&#40;동기화&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
    -   GUI 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)합니다.  
  
    -   데이터 형식 매핑 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;형식 매핑&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)합니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
DB2 데이터베이스에서 데이터를 마이그레이션하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 프로젝트를 먼저 만들어야 합니다.  
  
**프로젝트를 만들려면**  
  
1.  에 **파일** 메뉴에서 클릭 **새 프로젝트**합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  에 **위치** 상자, 입력 또는 프로젝트에 대 한 폴더를 선택 하 고 클릭 **확인**합니다.  
  
4.  에 **마이그레이션에** 드롭다운, 대상의 버전을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션에 사용 합니다. 사용 가능한 옵션은 다음과 같습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>사용자 지정 프로젝트 설정  
에 모든 새 SSMA 프로젝트에 적용 되는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [프로젝트 옵션 설정 &#40;OracleToSQL&#41; ](../../ssma/oracle/setting-project-options-oracletosql.md) 및 관련 섹션입니다.  
  
원본 및 대상 데이터베이스 간의 데이터 형식 매핑 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 자세한 내용은 [매핑 DB2 및 SQL Server 데이터 형식 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)합니다.  
  
## <a name="saving-projects"></a>프로젝트를 저장합니다.  
프로젝트를 저장 하면 SSMA 프로젝트 설정 및 선택적으로 프로젝트 파일에는 데이터베이스 메타 데이터를 유지 합니다.  
  
**프로젝트를 저장 하려면**  
  
-   에 **파일** 메뉴에서 클릭 **프로젝트 저장**합니다.  
  
    프로젝트의 스키마 변경, 변환 되지 않은 경우 로드 하 고 메타 데이터를 저장 하면 SSMA 메시지가 나타납니다. 메타 데이터를 저장 및 로드 오프 라인으로 작업할 수 있습니다. 또한 기술 지원 담당자와 같은 다른 사용자에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 나타나면 다음을 수행 합니다.  
  
    1.  상태를 보여 주는 각 스키마에 대해 **메타 데이터 누락**, 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하면 몇 분 정도 걸릴 수 있습니다. 메타 데이터를 아직 저장 하지 않을 경우 모든 확인란을 선택 하지 마십시오.  
  
    2.  클릭 합니다 **저장할** 단추입니다.  
  
        SSMA는 DB2 스키마를 구문 분석 하 고 프로젝트 파일에 메타 데이터를 저장 합니다.  
  
## <a name="opening-projects"></a>열린 프로젝트  
DB2에서 끊어진 프로젝트를 열면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 데이터베이스 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 데이터를 마이그레이션하려면 DB2에 연결 해야 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다.  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   에 **파일** 메뉴에서 **최근에 사용한 프로젝트**를 누른 다음 열려는 프로젝트 및 합니다.  
  
    -   에 **파일** 메뉴에서 **프로젝트 열기**.o2ssproj 프로젝트 파일 찾기, 파일을 선택 및 클릭 **열기**.  
  
2.  DB2로 다시 연결 합니다 **파일** 메뉴에서 클릭 **DB2에 다시 연결**합니다.  
  
3.  에 다시 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 **파일** 메뉴에서 클릭 **SQL Server에 다시 연결**합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스에서 다음 단계 [DB2 데이터베이스에 연결할](http://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server로 데이터베이스 마이그레이션 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[DB2 데이터베이스에 연결 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[SQL Server에 연결 &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
