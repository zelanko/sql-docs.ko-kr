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
ms.openlocfilehash: 658487186924fe5547edee70425524b2b4e3be6c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083588"
---
# <a name="migration-wizard-accesstosql"></a>마이그레이션 마법사 (AccessToSQL)
마이그레이션 마법사는 하나 이상의 데이터베이스를에 대 한 액세스에서 또는 SQL Azure로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션하는 과정을 안내 합니다. 마법사를 사용 하 여 프로젝트를 만들고, 프로젝트에 데이터베이스를 추가 하 고, 마이그레이션할 개체를 선택 하 고, SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 합니다. 또한 액세스 스키마와 데이터를 변환, 로드 및 마이그레이션합니다. 필요에 따라 액세스 테이블을 또는 SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 연결할 수 있습니다.  
  
대부분의 마이그레이션 마법사 페이지에는 기존 SSMA 대화 상자와 같은 옵션이 포함 되어 있습니다. 따라서 마법사 페이지는 여기에 설명 되어 있으며, 개별 옵션에 대 한 자세한 내용을 확인할 수 있도록 링크가 제공 됩니다. 페이지에 고유한 옵션이 포함 되어 있으면 여기에 설명 되어 있습니다.  
  
## <a name="starting-the-migration-wizard"></a>마이그레이션 마법사 시작  
기본적으로 SSMA를 시작 하면 마이그레이션 마법사가 나타납니다. **마이그레이션 마법사**를 선택 하 여 **파일** 메뉴에서 마법사를 시작할 수도 있습니다.  
  
## <a name="welcome-page"></a>시작 페이지  
시작 페이지에서는 마이그레이션 마법사를 소개 하 고 마법사를 시작 하는 다음과 같은 옵션을 제공 합니다.  
  
**시작할 때이 마법사를 시작 합니다.**  
Ssma를 시작 하면 기본적으로 마이그레이션 마법사가 시작 됩니다. 마법사가 자동으로 시작 되는 것을 방지 하려면이 확인란의 선택을 취소 합니다.  
  
## <a name="create-new-project-page"></a>새 프로젝트 만들기 페이지  
새 프로젝트 만들기 페이지에서 프로젝트 파일 이름, 위치 및 마이그레이션 프로젝트 형식 (마이그레이션에 사용 되는 대상 SQL Server의 버전)을 입력할 수 있습니다. 자세한 내용은 [SSMA (새 프로젝트)](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3) 를 참조 하세요.  
  
## <a name="add-access-databases-page"></a>액세스 데이터베이스 추가 페이지  
액세스 데이터베이스 추가 페이지에서 하나 이상의 Access 데이터베이스를 프로젝트에 추가할 수 있습니다. **데이터베이스 추가**를 클릭 한 다음 **열기** 창에서 데이터베이스를 선택 하 여 개별 데이터베이스를 추가할 수 있습니다. 또는 데이터베이스 **찾기** 단추를 사용 하 여 데이터베이스를 찾을 수 있습니다. 자세한 내용은 아래 항목을 참조하세요.  
  
-   [Access 데이터베이스 파일 추가 및 제거](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [데이터베이스 찾기 마법사(위치 선택)](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [데이터베이스 찾기 마법사(파일 선택)](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [데이터베이스 찾기 마법사(선택 영역 확인)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>마이그레이션할 개체 선택 페이지  
마이그레이션할 개체 선택 페이지에서 변환할 개체를 선택 합니다. 모든 개체, 개체 그룹 또는 개별 개체를 선택할 수 있습니다.  
  
**개체를 선택 하려면**  
  
1.  **액세스-메타 베이스**를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
2.  다음 중 하나 이상을 수행합니다.  
  
    -   모든 데이터베이스를 변환 하려면 **데이터베이스**옆의 확인란을 선택 합니다.  
  
    -   개별 데이터베이스를 변환 하거나 생략 하려면 데이터베이스 이름 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   쿼리를 변환 하거나 생략 하려면 데이터베이스를 확장 한 다음 **쿼리** 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 테이블을 변환 하거나 생략 하려면 데이터베이스를 확장 하 고 **테이블**을 확장 한 다음 테이블 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
개체가 많은 경우 오른쪽 창에서 **고급 개체 선택** 옵션을 사용 하 여 Access 데이터베이스 개체를 필터링 할 수 있습니다. 예를 들어 왼쪽 창에서 **테이블** 을 선택 하는 경우 **필터** 상자에 문자열을 입력 하 여 테이블 목록을 필터링 할 수 있습니다. 그런 다음 창의 맨 위에 있는 단추를 사용 하 여 마이그레이션할 필터링 된 테이블을 선택 하거나 선택 취소할 수 있습니다.  
  
필터링에 대 한 자세한 내용은 [고급 개체 선택 (SSMA Common)](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c)의 옵션 섹션을 참조 하세요.  
  
## <a name="connect-to-sql-server-page"></a>SQL Server 페이지에 연결  
연결 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에서 연결 속성을 지정 하 고에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 합니다. 자세한 내용은 [SQL Server에 연결](connect-to-sql-server-accesstosql.md)을 참조 하세요.
  
> [!IMPORTANT]  
> 연결이 성공 하는 즉시 테이블 링크 옵션이 있는 **링크 테이블** 페이지가 표시 됩니다. **다음** 을 클릭 하 여 마이그레이션을 시작 합니다.  
  
## <a name="connect-to-sql-azure-page"></a>SQL Azure 페이지에 연결  
SQL Azure에 연결 페이지에서 연결 속성을 지정 하 고 SQL Azure에 연결 합니다. 새 azure 데이터베이스를 만들려면 **찾아보기** 단추 클릭에 표시 되는 **azure 데이터베이스 만들기** 옵션을 사용 하 여이 작업을 수행할 수 있습니다. 자세한 내용은 [SQL Azure에 연결](connect-to-azure-sql-db-accesstosql.md) 을 참조 하세요.  
  
> [!IMPORTANT]  
> 연결이 성공 하는 즉시 테이블 링크 옵션이 있는 **링크 테이블** 페이지가 표시 됩니다. 연결 페이지에서 **다음** 단추를 클릭 하 여 마이그레이션을 시작 합니다.  
  
## <a name="link-tables-page"></a>테이블 연결 페이지  
테이블 연결 페이지를 사용 하 여 마이그레이션된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이 나 SQL Azure 테이블에 원래 액세스 테이블을 연결할 수 있습니다. 테이블을 연결 하면 쿼리, 폼, 보고서 및 데이터 액세스 페이지에서 Access 데이터베이스의 데이터 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스의 데이터를 사용 하도록 access 데이터베이스를 수정 합니다.  
  
**테이블 연결**  
**테이블 연결** 확인란을 선택 하 여 마이그레이션된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 또는 SQL Azure 테이블에 액세스 테이블을 연결 합니다. 마이그레이션을 시작 하려면 [ **다음** ] 단추를 클릭 해야 합니다.  
  
## <a name="migration-status-page"></a>마이그레이션 상태 페이지  
마이그레이션 상태 페이지에는 액세스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마로 변환 하 고, 변환 된 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure로 로드 하 고, 데이터를 마이그레이션하는 진행률이 표시 됩니다.  
  
이 페이지에 대 한 자세한 내용은 [변환, 로드 및 마이그레이션](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b) 을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[Access &#40;AccessToSQL&#41;에 대 한 SQL Server Migration Assistant 시작](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[사용자 인터페이스 참조 (액세스)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
