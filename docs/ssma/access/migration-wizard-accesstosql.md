---
title: 마이그레이션 마법사 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 62ef99767be3f228702a06d89ba52f5c3a9821fb
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664822"
---
# <a name="migration-wizard-accesstosql"></a>마이그레이션 마법사 (AccessToSQL)
마이그레이션 마법사는 과정을 안내 하나 이상의 데이터베이스의 마이그레이션에 대 한 액세스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 마법사를 사용 하 여 있습니다는 프로젝트를 만들 데이터베이스 프로젝트를 추가, 연결 하 고, 마이그레이션하려는 개체를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 또한 변환, 로드 하 고 Access 스키마 및 데이터 마이그레이션. 필요에 따라 액세스 테이블을 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블입니다.  
  
마이그레이션 마법사 페이지의 대부분 기존 SSMA 대화 상자와 동일한 옵션을 포함 합니다. 따라서 마법사 페이지는 여기서 설명 하는 하 고 개별 옵션에 대 한 자세한 내용은 되도록 링크 제공 합니다. 고유 옵션 페이지가 있으면 여기 설명 되어 있습니다.  
  
## <a name="starting-the-migration-wizard"></a>마이그레이션 마법사를 시작합니다.  
마이그레이션 마법사에는 기본적으로 SSMA를 시작 하면 나타납니다. 마법사를 시작할 수도 있습니다는 **파일** 를 선택 하 여 메뉴 **마이그레이션 마법사**합니다.  
  
## <a name="welcome-page"></a>시작 페이지  
마이그레이션 마법사를 소개 하 고 마법사를 시작 하기 위한 다음 옵션을 제공 하는 시작 페이지입니다.  
  
**시작 시이 마법사를 시작 합니다.**  
기본적으로 SSMA SSMA를 시작 하는 경우 마이그레이션 마법사가 시작 됩니다. 마법사의 자동 시작을 방지 하려면이 확인란의 선택을 취소 합니다.  
  
## <a name="create-new-project-page"></a>새 프로젝트 페이지 만들기  
새 프로젝트 만들기 페이지가 프로젝트 파일 이름, 위치 및 마이그레이션 프로젝트 형식 (대상 마이그레이션에 사용 되는 SQL Server의 버전)를 입력 하는 위치입니다. 자세한 내용은 참조 하세요. [새 프로젝트 (SSMA)](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>액세스 데이터베이스 페이지를 추가 합니다.  
Access 데이터베이스 추가 페이지가 하나 이상의 Access 데이터베이스 프로젝트에 추가 되는 위치입니다. 클릭 하 여 개별 데이터베이스를 추가할 수 있습니다 **데이터베이스 추가**, 한 다음 데이터베이스를 선택 하는 **오픈** 창입니다. 사용 하 여 데이터베이스를 찾을 수 있습니다 또는 합니다 **찾을 데이터베이스** 단추. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [Access 데이터베이스 파일 추가 및 제거](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [데이터베이스 찾기 마법사 (위치 선택)](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [데이터베이스 찾기 마법사 (파일 선택)](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [데이터베이스 찾기 마법사(선택 확인)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>페이지의 마이그레이션할 개체를 선택 합니다.  
마이그레이션 페이지로 선택 개체를 변환 하는 개체를 선택 합니다. 모든 개체를 개체 또는 개별 개체의 그룹을 선택할 수 있습니다.  
  
**개체를 선택 합니다.**  
  
1.  확장 **액세스-메타 베이스**를 차례로 확장 하 고 **데이터베이스**합니다.  
  
2.  다음 중 하나 이상을 수행 합니다.  
  
    -   모든 데이터베이스를 변환 하려면 확인란을 선택 합니다 옆 **데이터베이스**합니다.  
  
    -   변환 또는 생략 개별 데이터베이스를 선택 하거나 데이터베이스 이름 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 쿼리를 생략 하려면 데이터베이스를 확장 하 고 다음 선택 하거나 선택을 취소 합니다 **쿼리** 확인란 합니다.  
  
    -   를 변환 하거나 개별 테이블을 생략 하려면 데이터베이스를 확장 **테이블**, 다음을 선택 하거나 표 옆의 확인란의 선택을 취소 합니다.  
  
사용 하려는 많은 개체가 있는 경우는 **고급 개체 선택** 액세스를 필터링 하려면 오른쪽 창에서 옵션 데이터베이스 개체입니다. 예를 들어 선택한 **테이블** 왼쪽된 창에서 필터링 할 수 있습니다 다음 테이블 목록에서 문자열을 입력 하 여 합니다 **필터** 상자입니다. 선택 하거나 창의 맨 위에 있는 단추를 사용 하 여 마이그레이션에 대 한 필터링 된 테이블을 지울 수 있습니다.  
  
필터링에 대 한 자세한 내용은의 옵션 섹션을 참조 하세요 [고급 개체 선택 영역 (SSMA 공통)](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c)합니다.  
  
## <a name="connect-to-sql-server-page"></a>SQL Server 페이지에 연결  
에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에서 연결 속성을 지정 하 고 다음 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 참조 하세요. [SQL Server에 연결](https://msdn.microsoft.com/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> 연결에 성공 하는 즉시 발생 **링크 테이블** 테이블을 연결 하는 옵션이 있는 페이지. 클릭 **다음** 마이그레이션을 시작 합니다.  
  
## <a name="connect-to-sql-azure-page"></a>SQL Azure에 연결 페이지  
SQL Azure 페이지로 연결에서 연결 속성을 지정 하 고 SQL Azure 연결 합니다. 새 azure 데이터베이스를 만들려면 있습니다 수 사용 하 여 그렇게 **Azure 데이터베이스 만들기** 를 클릭할 때 표시 되는 옵션 **찾아보기** 단추입니다. 자세한 내용은 참조 하세요. [SQL Azure 연결](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> 연결에 성공 하는 즉시 발생 **링크 테이블** 테이블을 연결 하는 옵션이 있는 페이지. 클릭 **다음** 마이그레이션을 시작 링크 페이지의 단추입니다.  
  
## <a name="link-tables-page"></a>링크 테이블 페이지  
테이블 연결 페이지를 사용 하면 원래 Access 테이블을 마이그레이션된 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블입니다. 테이블 연결을 수정 하 Access 데이터베이스에서 데이터를 사용 하는 쿼리, 폼, 보고서 및 데이터 액세스 페이지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Access 데이터베이스의 데이터 대신 SQL Azure 데이터베이스.  
  
**테이블 연결**  
선택 된 **테이블을 연결** 확인란을 마이그레이션된 테이블 액세스 링크 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블. 클릭 해야 하는 마이그레이션을 시작 하려면 **다음** 단추입니다.  
  
## <a name="migration-status-page"></a>마이그레이션 상태 페이지  
마이그레이션 상태 페이지에 대 한 액세스 스키마 변환 진행률을 보여 줍니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마, 변환 된 스키마를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 및 다음 데이터를 마이그레이션.  
  
이 페이지에 대 한 자세한 내용은 참조 하세요. [변환, 로드 및 마이그레이션](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>관련 항목  
[액세스에 대 한 SQL Server Migration Assistant를 사용 하 여 시작 &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[사용자 인터페이스 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
