---
title: SSMA 프로젝트 작업 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: eb6f035b4d597e2b648134c195b698554dc78e12
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68072473"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>SSMA 프로젝트 작업(SybaseToSQL)
Sybase ASE (적응 서버 엔터프라이즈) 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하려면 먼저 ssma 프로젝트를 만듭니다. 프로젝트는 SQL Azure 마이그레이션하려 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 ASE 데이터베이스에 대 한 메타 데이터를 포함 하는 파일입니다 .이 파일의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 인스턴스에 대 한 메타 데이터, 마이그레이션된 개체 및 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 받는 SQL Azure 또는 연결 정보 SQL Azure, 프로젝트 설정에 대 한 메타 데이터를 포함 하는 파일입니다.  
  
프로젝트를 열면 또는 SQL Azure에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결이 끊어집니다. 이렇게 하면 오프 라인으로 작업할 수 있습니다. 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다시 연결 하거나 SQL Azure 수 있습니다. 자세한 내용은 [SQL Server에 연결 &#40;sybasetosql&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  /  [Azure SQL DB에 연결 &#40;sybasetosql&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)을 참조 하세요.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA에는 데이터베이스 개체를 변환 및 로드 하 고, 데이터를 마이그레이션하고, ASE 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure와 ssma를 동기화 하기 위한 몇 가지 옵션이 포함 되어 있습니다. 이러한 옵션에 대 한 기본 설정은 대부분의 사용자에 게 적합 합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 옵션을 검토 하 고 원하는 경우 모든 새 프로젝트에 사용 되는 기본값을 변경 해야 합니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 합니다.  
  
2.  설정을 보거나 변경 해야 하는 **마이그레이션 대상 버전** 드롭다운에서 프로젝트 유형을 선택 하 고 **일반** 탭을 클릭 합니다.  
  
3.  왼쪽 창에서 **변환**을 클릭 합니다.  
  
4.  오른쪽 창에서 옵션을 검토 하 고 필요에 따라 옵션을 변경 합니다. 이러한 옵션에 대 한 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)을 참조 하세요.  
  
5.  마이그레이션, SQL Azure, 개체 로드, GUI 및 형식 매핑 페이지에 대해 1-3 단계를 반복 합니다.  
  
    -   마이그레이션 옵션에 대 한 자세한 내용은 [프로젝트 설정 &#40;마이그레이션&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)을 참조 하세요.  
  
    -   로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]개체를 로드 하는 옵션에 대 한 자세한 내용은 [프로젝트 설정 &#40;동기화&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)를 참조 하세요.  
  
    -   GUI 옵션에 대 한 자세한 내용은 [프로젝트 설정 &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)를 참조 하세요.  
  
    -   데이터 형식 매핑 설정에 대 한 자세한 내용을 보려면 [프로젝트 설정 &#40;형식 매핑&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)을 클릭 합니다.  
  
    -   SQL Azure 옵션에 대 한 자세한 내용은 [프로젝트 설정 &#40;AZURE SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)를 참조 하세요.  
  
    > [!NOTE]  
    > SQL Azure 설정은 프로젝트를 만드는 동안 **SQL Azure로 마이그레이션을** 선택한 경우에만 표시 됩니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
ASE 데이터베이스에서 또는 SQL Azure로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 마이그레이션하려면 먼저 프로젝트를 만들어야 합니다.  
  
**프로젝트를 만들려면**  
  
1.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  **위치** 상자에서 프로젝트에 대 한 폴더를 입력 하거나 선택 합니다.  
  
4.  **마이그레이션** 드롭다운에서 마이그레이션에 사용 되는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 선택 합니다. 제공되는 옵션은 다음과 같습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
그런 다음 **확인**을 클릭 합니다.  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
모든 새 SSMA 프로젝트에 적용 되는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [프로젝트 옵션 설정 &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)을 참조 하세요.  
  
원본 데이터베이스와 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 형식 매핑에 대 한 자세한 내용은 [SYBASE ASE 및 SQL Server 데이터 형식 매핑 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)을 참조 하세요.  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트를 저장 하면 SSMA는 프로젝트 설정 및 필요에 따라 데이터베이스 메타 데이터를 프로젝트 파일에 유지 합니다.  
  
**프로젝트를 저장하려면**  
  
-   **파일** 메뉴에서 **프로젝트 저장**을 선택 합니다.  
  
    프로젝트 내의 데이터베이스가 변경 되었거나 변환 되지 않은 경우 SSMA는 메타 데이터를 프로젝트에 저장 하 라는 메시지를 표시 합니다. 메타 데이터를 저장 하면 오프 라인으로 작업 하 고 기술 지원 담당자를 비롯 한 전체 프로젝트 파일을 다른 사용자에 게 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 표시 되 면 다음을 수행 합니다.  
  
    1.  **누락 된 메타 데이터**의 상태를 표시 하는 각 데이터베이스에 대해 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하는 데 몇 분 정도 걸릴 수 있습니다. 이때 메타 데이터를 저장 하지 않으려면 확인란을 선택 하지 마십시오.  
  
    2.  **저장** 단추를 클릭합니다.  
  
        SSMA는 Sybase ASE 스키마를 구문 분석 하 고 메타 데이터를 프로젝트 파일에 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열 때 ASE와에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에서 연결이 끊어집니다. 이렇게 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure으로 로드 합니다. 데이터를 마이그레이션하려면 ASE 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에 다시 연결 해야 합니다.  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   **파일** 메뉴에서 **최근 프로젝트**를 가리킨 다음 열려는 프로젝트를 선택 합니다.  
  
    -   **파일** 메뉴에서 **프로젝트 열기**를 선택 하 고 s2ssproj 프로젝트 파일을 찾은 다음 파일을 선택 하 고 **열기**를 클릭 합니다.  
  
2.  ASE에 다시 연결 하려면 **파일** 메뉴에서 **Sybase에 다시 연결**을 선택 합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure에 다시 연결 하려면 **파일** 메뉴에서 **다시 연결** / 을 선택 하 여**SQL Azure에 다시 연결**SQL Server 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SYBASE ASE에 연결](connecting-to-sybase-ase-sybasetosql.md)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Sybase ASE &#40;SybaseToSQL&#41;에 연결](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[SQL Server &#40;SybaseToSQL&#41;에 연결](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Azure SQL DB &#40;SybaseToSQL&#41;에 연결](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
