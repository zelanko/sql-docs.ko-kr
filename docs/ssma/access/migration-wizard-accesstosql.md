---
title: 마이그레이션 마법사 (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03b556d7fa5f49d69d9554d3416e3277adc4f504
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="migration-wizard-accesstosql"></a>마이그레이션 마법사 (AccessToSQL)
마이그레이션 마법사는 과정을 안내해 하나 이상의 데이터베이스 마이그레이션에 대 한 액세스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 마법사를 사용 하 여 있습니다 됩니다 프로젝트 만들기, 프로젝트에 데이터베이스를 추가에 연결 하 고 마이그레이션하려는 개체를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 있습니다는 또한 변환, 로드 및 액세스 스키마 및 데이터 마이그레이션. 필요에 따라 액세스 테이블을 연결할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 테이블입니다.  
  
대부분의 마이그레이션 마법사 페이지와 동일한 옵션을 기존 SSMA 대화 상자를 포함 합니다. 따라서 마법사 페이지는 여기에서 설명 하 고 개별 옵션에 대 한 자세한 내용은 있도록 링크가 다음 제공 됩니다. 고유 옵션이 한 페이지에 있는 경우 여기 설명 되어 있습니다.  
  
## <a name="starting-the-migration-wizard"></a>마이그레이션 마법사를 시작합니다.  
기본적으로 마이그레이션 마법사는 SSMA를 시작 하면 나타납니다. 마법사를 시작할 수도 있습니다는 **파일** 메뉴를 선택 하 여 **마이그레이션 마법사**합니다.  
  
## <a name="welcome-page"></a>시작 페이지  
마이그레이션 마법사를 소개 하 고 마법사를 시작 하기 위한 다음 옵션을 제공 하는 시작 페이지입니다.  
  
**시작 시이 마법사를 시작 합니다.**  
기본적으로 SSMA SSMA를 시작 하는 경우 마이그레이션 마법사가 시작 됩니다. 마법사의 자동 시작을 방지 하려면이 확인란의 선택을 취소 합니다.  
  
## <a name="create-new-project-page"></a>새 프로젝트 페이지 만들기  
새 프로젝트 만들기 페이지 프로젝트 파일 이름, 위치 및 마이그레이션 프로젝트 형식 (대상 마이그레이션에 사용 되는 SQL Server의 버전)을 입력 하면 됩니다. 자세한 내용은 참조 [새 프로젝트 (SSMA)](http://msdn.microsoft.com/en-us/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Access 데이터베이스 페이지를 추가 합니다.  
Access 데이터베이스 추가 페이지에는 프로젝트에 하나 이상의 Access 데이터베이스를 추가 하는 위치입니다. 클릭 하 여 개별 데이터베이스를 추가할 수 있습니다 **추가 데이터베이스**, 한 다음 데이터베이스를 선택 하는 **열려** 창. 또는 사용 하 여 데이터베이스를 찾을 수 있습니다는 **찾을 데이터베이스** 단추입니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Access 데이터베이스 파일 추가 및 제거](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
-   [찾기 데이터베이스 마법사 (선택 위치)](http://msdn.microsoft.com/en-us/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [찾기 데이터베이스 마법사 (파일 선택)](http://msdn.microsoft.com/en-us/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [데이터베이스 찾기 마법사(선택 확인)](http://msdn.microsoft.com/en-us/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>페이지 마이그레이션할 개체를 선택 합니다.  
개체 선택 마이그레이션 페이지에서 변환 하는 개체를 선택 합니다. 모든 개체, 개체 또는 개별 개체의 그룹을 선택할 수 있습니다.  
  
**개체를 선택 하려면**  
  
1.  확장 **액세스 메타 베이스**을 펼친 다음 **데이터베이스**합니다.  
  
2.  다음 중 하나 이상을 수행 합니다.  
  
    -   모든 데이터베이스를 변환 하려면 확인란을 옆에 선택 **데이터베이스**합니다.  
  
    -   변환 하거나 생략 개별 데이터베이스를 선택 하거나 데이터베이스 이름 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 쿼리를 생략 하려면 데이터베이스를 확장 한 다음 선택 하거나 선택 취소 된 **쿼리** 확인란 합니다.  
  
    -   를 변환 하거나 개별 테이블을 생략 하려면 데이터베이스를 확장 하 고 **테이블**, 다음을 선택 하거나 테이블 옆 확인란의 선택을 취소 합니다.  
  
사용 하려는 많은 개체를 사용 하도록 설정한 경우는 **고급 개체 선택** 옵션 오른쪽 창에 대 한 액세스를 필터링 할 데이터베이스 개체입니다. 예를 들어, 선택 하는 경우 **테이블** 왼쪽된 창에서 필터링 할 수 있습니다 다음 테이블 목록에서 문자열을 입력 하 여는 **필터** 상자입니다. 다음 선택 하거나 창의 위쪽에 단추를 사용 하 여 마이그레이션에 대 한 필터링 된 테이블을 지울 수 있습니다.  
  
필터링에 대 한 자세한 내용은 옵션 섹션을 참조 하십시오. [(SSMA 공통) 개체 선택 고급](http://msdn.microsoft.com/en-us/f53b0c79-5473-410a-a0dc-d8f544f7a63c)합니다.  
  
## <a name="connect-to-sql-server-page"></a>SQL Server 페이지에 연결  
연결에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 페이지에서 연결 속성을 지정 하 고 다음에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [SQL Server에 연결](http://msdn.microsoft.com/en-us/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> 발생 하 게 연결 되는 즉시 **테이블 연결** 는 테이블을 연결 하는 옵션 있는 페이지. 클릭 **다음** 마이그레이션을 시작 합니다.  
  
## <a name="connect-to-sql-azure-page"></a>SQL에 연결할 Azure 페이지  
SQL Azure 페이지에 대 한 연결, 연결 속성을 지정 하 고 SQL Azure에 연결 합니다. 새 azure 데이터베이스를 만들려고 하면 사용 하 여 **Azure 데이터베이스 만들기** 를 클릭할 때 표시 되는 옵션 **찾아보기** 단추입니다. 자세한 내용은 참조 [SQL Azure에 연결](http://msdn.microsoft.com/en-us/bf44b236-d9be-41ae-a5fd-bd73038e505f)  
  
> [!IMPORTANT]  
> 발생 하 게 연결 되는 즉시 **테이블 연결** 는 테이블을 연결 하는 옵션 있는 페이지. 클릭 **다음** 마이그레이션을 시작 하려면 링크가 페이지에 단추입니다.  
  
## <a name="link-tables-page"></a>링크 테이블 페이지  
테이블 연결 페이지를 사용 하면 원래 Access 테이블을 마이그레이션된 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 테이블입니다. 테이블 연결을 수정 하 Access 데이터베이스에서 데이터를 사용 하는 쿼리, 폼, 보고서 및 데이터 액세스 페이지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Access 데이터베이스의 데이터 대신 SQL Azure 데이터베이스입니다.  
  
**테이블 연결**  
선택 된 **테이블을 연결** Access 테이블을 마이그레이션된 연결 하려면 확인란 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 테이블입니다. 클릭 하 여 해야 마이그레이션을 시작 하려면 **다음** 단추입니다.  
  
## <a name="migration-status-page"></a>마이그레이션 상태 페이지  
마이그레이션 상태 페이지에 대 한 액세스 스키마 변환 진행률이 표시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는으로 변환 된 스키마를 로드 하는 SQL Azure 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 하 고 다음 데이터를 실행 합니다.  
  
이 페이지에 대 한 자세한 내용은 참조 [변환, 로드 및 마이그레이션](http://msdn.microsoft.com/en-us/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>관련 항목:  
[Getting Started with SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[사용자 인터페이스 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
