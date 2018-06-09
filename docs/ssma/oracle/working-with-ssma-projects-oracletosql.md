---
title: SSMA 프로젝트 (OracleToSQL) 사용 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: b1b28a2a9b6bf9210aa23d0f7914693f938bbf53
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778059"
---
# <a name="working-with-ssma-projects-oracletosql"></a>SSMA 프로젝트 (OracleToSQL) 작업
Oracle 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 프로젝트를 만들어야 합니다. 프로젝트는 다음 정보를 포함 하는 파일입니다.  
  
-   로 마이그레이션하려는 Oracle 데이터베이스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   대상 인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션된 개체 및 데이터를 받습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 연결 정보입니다.  
  
-   프로젝트 설정 합니다.  
  
프로젝트를 열 때 Oracle에서 연결이 끊어지도록 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. 에 다시 연결 하는 방법에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 참조 [SQL Server에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)합니다.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA 변환 및 마이그레이션 데이터를 데이터베이스 개체를 로드 및 Oracle과 SSMA를 동기화에 대 한 몇 가지 설정을 포함 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기본 설정은 많은 사용자에 대 한 적절 한입니다. 그러나 새 SSMA 프로젝트를 만들기 전에 설정을 검토 해야 합니다. 원하는 경우에 모든 새 프로젝트에 사용할 기본 설정을 변경할 수 있습니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  에 **도구** 메뉴를 클릭 하 여 **기본 프로젝트 설정**합니다.  
  
2.  프로젝트 형식을 선택 **마이그레이션 대상 버전** 어떤 설정이 보거나 변경 하는 데 필요 하 고 클릭 한 다음에 대 한 드롭다운 **일반** 탭 합니다.  
  
3.  왼쪽된 창에서 클릭 **변환**합니다.  
  
4.  오른쪽 창에서 검토 하 고 필요에 따라 설정을 변경 합니다. 이러한 설정에 대 한 자세한 내용은 참조 [프로젝트 설정 &#40;변환&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)합니다.  
  
5.  마이그레이션, 동기화, 시스템 개체를 로드, GUI 및 유형 매핑 페이지에 대 한 1-3 단계를 반복 합니다.  
  
    -   마이그레이션 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40;마이그레이션&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)합니다.  
  
    -   시스템 개체 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정&#40;로드 시스템 개체&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md)합니다.  
  
    -   동기화에 대 한 설정에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 참조 [프로젝트 설정&#40;동기화&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)합니다.  
  
    -   GUI 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)합니다.  
  
    -   데이터 형식 매핑 설정에 대 한 정보를 참조 하십시오. [프로젝트 설정 &#40;형식 매핑&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)합니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
Oracle 데이터베이스에서 데이터를 마이그레이션하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 프로젝트를 먼저 만들어야 합니다.  
  
**프로젝트를 만들려면**  
  
1.  에 **파일** 메뉴를 클릭 하 여 **새 프로젝트**합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  에 **위치** 상자 입력 하거나 프로젝트에 대 한 폴더를 선택 하 고 클릭 **확인**합니다.  
  
4.  에 **마이그레이션에** 대상 버전을 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션에 사용 합니다. 사용할 수 있는 옵션이 있습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
에 모든 새 SSMA 프로젝트에 적용 되는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [프로젝트 옵션 설정 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)합니다.  
  
원본 및 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 프로젝트, 데이터베이스 또는 개체 수준에서 매핑 정의할 수 있습니다. 자세한 내용은 참조 [매핑 Oracle 및 SQL Server 데이터 형식 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)합니다.  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트를 저장 하면 SSMA 프로젝트 설정 및 필요에 따라 프로젝트 파일에는 데이터베이스 메타 데이터를 유지 합니다.  
  
**프로젝트를 저장 하려면**  
  
-   에 **파일** 메뉴를 클릭 하 여 **프로젝트 저장**합니다.  
  
    프로젝트의 스키마 변경 변환 하지 않은 경우 SSMA 하 라는 메시지가 나타납니다 로드 하 고 메타 데이터를 저장 합니다. 로드 및 메타 데이터를 저장 하면 오프 라인으로 작업 합니다. 또한 기술 지원 담당자와 같은 다른 사람에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하는 메시지가 다음을 수행 합니다.  
  
    1.  상태를 보여 주는 각 스키마에 대해 **메타 데이터 누락**, 데이터베이스 이름 옆에 있는 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하면 몇 분 정도 걸릴 수 있습니다. 메타 데이터를 아직 저장 하지 않을 경우 모든 확인란을 선택 하지 마십시오.  
  
    2.  클릭는 **저장** 단추입니다.  
  
        SSMA는 Oracle 스키마를 구문 분석 하 고 프로젝트 파일에 메타 데이터를 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열 때 연결이 끊어지도록 및 Oracle에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 데이터베이스 개체에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. Oracle에 연결 해야 데이터를 마이그레이션하려면 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   에 **파일** 메뉴에서 **최근에 사용한 프로젝트**, 한 다음 열려는 프로젝트를 클릭 합니다.  
  
    -   에 **파일** 메뉴 선택 **프로젝트 열기**,.o2ssproj 프로젝트 파일, 파일을 찾은 다음 클릭 **열려**합니다.  
  
2.  Oracle에 다시 연결할는 **파일** 메뉴를 클릭 하 여 **Oracle에 다시 연결**합니다.  
  
3.  에 다시 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]의 **파일** 메뉴를 클릭 하 여 **SQL Server에 다시 연결**합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 [Oracle 데이터베이스 (OracleToSQL)에 연결](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server로 데이터베이스 마이그레이션 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Oracle 데이터베이스에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[SQL Server에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
