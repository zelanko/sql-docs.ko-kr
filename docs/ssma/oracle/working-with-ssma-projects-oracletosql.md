---
title: SSMA 프로젝트 작업 (OracleToSQL) | Microsoft Docs
description: 설정 및 연결 정보와 함께, SQL Server 마이그레이션할 Oracle 데이터베이스에 대 한 메타 데이터가 포함 된 SSMA 프로젝트를 만드는 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 1acf08369e0d6591c96e74defabe2a49d15e412d
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932694"
---
# <a name="working-with-ssma-projects-oracletosql"></a>SSMA 프로젝트 작업(OracleToSQL)
Oracle 데이터베이스를로 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 먼저 SSMA 프로젝트를 만듭니다. 프로젝트는 다음 정보를 포함 하는 파일입니다.  
  
-   마이그레이션하려는 Oracle 데이터베이스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다.  
  
-   마이그레이션된 개체와 데이터를 받을의 대상 인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 정보입니다.  
  
-   프로젝트 설정.  
  
프로젝트를 열면 Oracle 및에서 연결이 끊어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이를 통해 오프 라인으로 작업할 수 있습니다. 에 다시 연결 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server &#40;OracleToSQL&#41;에 연결 ](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)을 참조 하세요.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA에는 데이터베이스 개체를 변환 및 로드 하 고, 데이터를 마이그레이션하고, SSMA를 Oracle 및와 동기화 하기 위한 여러 설정이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 기본 설정은 대부분의 사용자에 게 적합 합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 설정을 검토 해야 합니다. 원하는 경우 모든 새 프로젝트에 사용 되는 기본 설정을 변경할 수 있습니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 클릭 합니다.  
  
2.  설정을 보거나 변경 해야 하는 **마이그레이션 대상 버전** 드롭다운에서 프로젝트 유형을 선택 하 고 **일반** 탭을 클릭 합니다.  
  
3.  왼쪽 창에서 **변환**을 클릭 합니다.  
  
4.  오른쪽 창에서 필요에 따라 설정을 검토 하 고 변경 합니다. 이러한 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)을 참조 하세요.  
  
5.  마이그레이션, 동기화, 시스템 개체, GUI 및 유형 매핑 페이지에 대해 1-3 단계를 반복 합니다.  
  
    -   마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;migration&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)를 참조 하세요.  
  
    -   시스템 개체 설정에 대 한 자세한 내용은 [프로젝트 설정&#40;시스템 개체 로드&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md)를 참조 하세요.  
  
    -   로의 동기화 설정에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [프로젝트 설정&#40;동기화&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)를 참조 하세요.  
  
    -   GUI 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)를 참조 하세요.  
  
    -   데이터 형식 매핑 설정에 대 한 자세한 내용은 [프로젝트 설정 &#40;형식 매핑&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)을 참조 하세요.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
Oracle 데이터베이스에서로 데이터를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 먼저 프로젝트를 만들어야 합니다.  
  
**프로젝트를 만들려면**  
  
1.  **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  **위치** 상자에서 프로젝트에 대 한 폴더를 입력 하거나 선택한 다음 **확인**을 클릭 합니다.  
  
4.  **마이그레이션** 드롭다운에서 마이그레이션에 사용 되는 대상 버전을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 제공되는 옵션은 다음과 같습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL Database  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
모든 새 SSMA 프로젝트에 적용 되는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [프로젝트 옵션 설정 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)을 참조 하세요.  
  
원본 데이터베이스와 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 자세한 내용은 [Oracle 및 SQL Server 데이터 형식 &#40;OracleToSQL&#41;매핑 ](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)을 참조 하세요.  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트를 저장 하면 SSMA는 프로젝트 설정 및 필요에 따라 데이터베이스 메타 데이터를 프로젝트 파일에 유지 합니다.  
  
**프로젝트를 저장하려면**  
  
-   **파일** 메뉴에서 **프로젝트 저장**을 클릭 합니다.  
  
    프로젝트의 스키마가 변경 되었거나 변환 되지 않은 경우 SSMA에서 메타 데이터를 로드 하 고 저장 하 라는 메시지를 표시 합니다. 메타 데이터를 로드 하 고 저장 하면 오프 라인으로 작업할 수 있습니다. 또한 기술 지원 담당자와 같은 다른 사람에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 표시 되 면 다음을 수행 합니다.  
  
    1.  **누락 된 메타 데이터**의 상태를 표시 하는 각 스키마에 대해 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하는 데 몇 분 정도 걸릴 수 있습니다. 메타 데이터를 아직 저장 하지 않으려면 확인란을 선택 하지 마십시오.  
  
    2.  **저장** 단추를 클릭합니다.  
  
        SSMA는 Oracle 스키마를 구문 분석 하 고 메타 데이터를 프로젝트 파일에 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열면 Oracle과의 연결이 끊어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이를 통해 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 데이터베이스 개체를에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 데이터를 마이그레이션하려면 Oracle 및에 다시 연결 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   **파일** 메뉴에서 **최근 프로젝트**를 가리킨 다음 열려는 프로젝트를 클릭 합니다.  
  
    -   **파일** 메뉴에서 **프로젝트 열기**를 선택 하 고 o2ssproj 프로젝트 파일을 찾은 다음 파일을 선택 하 고 **열기**를 클릭 합니다.  
  
2.  Oracle에 다시 연결 하려면 **파일** 메뉴에서 **Oracle에 다시 연결**을 클릭 합니다.  
  
3.  에 다시 연결 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **파일** 메뉴에서 **다시 연결**을 클릭 하 여 SQL Server 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [Oracle Database (OracleToSQL)에 연결](https://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Oracle Database &#40;OracleToSQL&#41;에 연결 하는 중](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[SQL Server &#40;OracleToSQL&#41;에 연결 하는 중](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
