---
description: 프로젝트 만들기 및 관리 (AccessToSQL)
title: 프로젝트 만들기 및 관리 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: ee6cf3bea905b169503851efe375fd614c4589e9
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988199"
---
# <a name="creating-and-managing-projects-accesstosql"></a>프로젝트 만들기 및 관리 (AccessToSQL)
Access 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하려면 먼저 SSMA 프로젝트를 만들어야 합니다. 프로젝트는 SQL Azure 마이그레이션하려는 액세스 데이터베이스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 개체 및 데이터, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보 및 프로젝트 설정을 받는 SQL Azure의 대상 인스턴스에 대 한 메타 데이터를 포함 하는 파일입니다.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정 검토  
SSMA에는 데이터베이스 개체를 변환 및 동기화 하 고 데이터를 변환 하기 위한 몇 가지 옵션이 포함 되어 있습니다. 이러한 옵션에 대 한 기본 설정은 대부분의 사용자에 게 적합 합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 옵션을 검토 하 고 원하는 경우 모든 새 프로젝트에 사용 되는 기본 설정을 변경 해야 합니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  **도구** 메뉴에서 **기본 프로젝트 설정**을 선택 합니다.  
  
2.  설정을 보거나 변경할 **마이그레이션 대상 버전** 드롭다운에서 프로젝트 유형을 선택 하 고 **일반** 탭을 클릭 합니다.  
  
3.  왼쪽 창에서 **변환**을 클릭 합니다.  
  
4.  오른쪽 창에서 옵션을 검토 합니다. 이러한 옵션에 대 한 자세한 내용은 [프로젝트 설정 (변환)](./project-settings-conversion-accesstosql.md)을 참조 하세요.  
  
5.  필요에 따라 옵션을 변경 합니다.  
  
6.  **마이그레이션**, **GUI**및 **형식 매핑** 페이지에 대해 이전 단계를 반복 합니다.  
  
    -   마이그레이션 옵션에 대 한 자세한 내용은 [프로젝트 설정 (마이그레이션)](./project-settings-migration-accesstosql.md)을 참조 하세요.  
  
    -   사용자 인터페이스 옵션에 대 한 자세한 내용은 [프로젝트 설정 (GUI)](../sybase/project-settings-gui-sybasetosql.md)을 참조 하세요.  
  
    -   데이터 형식 매핑 설정에 대 한 자세한 내용은 [프로젝트 설정 (형식 매핑)](./project-settings-type-mapping-accesstosql.md)을 참조 하세요.  
  
    -   SQL Azure 설정에 대 한 자세한 내용은 [프로젝트 설정 (SQL Azure)](./project-settings-azure-sql-db-accesstosql.md)을 참조 하세요.  
  
**참고** SQL Azure 설정은 프로젝트를 만드는 동안 SQL Azure로 마이그레이션을 선택한 경우에만 사용할 수 있습니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
기본 프로젝트를 로드 하지 않고 SSMA가 시작 됩니다. Access 데이터베이스에서 또는 SQL Azure로 데이터를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 만들어야 합니다.  
  
**새 프로젝트를 만들려면**  
  
1.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  **위치** 상자에서 프로젝트에 대 한 폴더를 입력 하거나 선택 합니다.  
  
4.  마이그레이션 드롭다운에서 SQL Server 2005/SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016/Azure SQL Database 중 하나를 선택 하 고 **확인**을 클릭 합니다.  
  
SSMA에서 프로젝트 파일을 만듭니다. 이제 [하나 이상의 Access 데이터베이스를 추가](adding-and-removing-access-database-files-accesstosql.md)하는 다음 단계를 수행할 수 있습니다.  
  
## <a name="customizing-project-settings"></a>프로젝트 설정 사용자 지정  
모든 새 SSMA 프로젝트에 적용 되는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [변환 및 마이그레이션 옵션 설정](setting-conversion-and-migration-options-accesstosql.md)을 참조 하세요.  
  
원본 데이터베이스와 대상 데이터베이스 간에 데이터 형식 매핑을 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 형식 매핑에 대 한 자세한 내용은 [원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md)을 참조 하세요.  
  
## <a name="saving-projects"></a>프로젝트 저장  
프로젝트를 저장 하면 SSMA는 프로젝트 설정 및 필요에 따라 데이터베이스 메타 데이터를 프로젝트 파일에 유지 합니다.  
  
**프로젝트를 저장하려면**  
  
-   **파일** 메뉴에서 **프로젝트 저장**을 선택 합니다.  
  
    프로젝트 내의 데이터베이스가 변경 되었거나 변환 되지 않은 경우 SSMA는 메타 데이터를 프로젝트에 저장 하 라는 메시지를 표시 합니다. 메타 데이터를 저장 하면 오프 라인으로 작업할 수 있습니다. 또한 기술 지원 담당자를 비롯 한 다른 사용자에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 표시 되 면 다음을 수행 합니다.  
  
    1.  **누락 된 메타 데이터**의 상태를 표시 하는 각 데이터베이스에 대해 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하는 데 몇 분 정도 걸릴 수 있습니다. 이때 메타 데이터를 저장 하지 않으려면 확인란을 선택 하지 마십시오.  
  
    2.  **Save**을 클릭합니다.  
  
        SSMA는 액세스 스키마를 구문 분석 하 고 메타 데이터를 프로젝트 파일에 저장 합니다.  
  
## <a name="opening-projects"></a>프로젝트 열기  
프로젝트를 열면 또는 SQL Azure에서 연결이 끊어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이렇게 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터를 업데이트 하려면 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure으로 로드 합니다. 데이터를 마이그레이션하려면 또는 SQL Azure에 다시 연결 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   **파일** 메뉴에서 **최근 프로젝트**를 가리킨 다음 열려는 프로젝트를 선택 합니다.  
  
    -   **파일** 메뉴에서 **프로젝트 열기**를 선택 하 고 a2ssproj 프로젝트 파일을 찾은 다음 파일을 선택 하 고 **열기**를 클릭 합니다.  
  
2.  에 다시 연결 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **파일** 메뉴에서 **SQL Server에 다시 연결**을 선택 합니다.  
  
3.  SQL Azure에 다시 연결 하려면 **파일** 메뉴에서 **SQL Azure에 다시 연결을 선택 합니다.**  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [하나 이상의 Access 데이터베이스를 추가](adding-and-removing-access-database-files-accesstosql.md)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Access 데이터베이스 파일 추가 및 제거](adding-and-removing-access-database-files-accesstosql.md)  
