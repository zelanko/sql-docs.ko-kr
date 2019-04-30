---
title: 프로젝트 (AccessToSQL) 만들기 및 관리 | Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1cf23a076f7e4d7e873f48988364c51b1daa03b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138810"
---
# <a name="creating-and-managing-projects-accesstosql"></a>프로젝트 (AccessToSQL) 만들기 및 관리
Access 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 있습니다 SSMA 프로젝트를 먼저 만들어야 합니다. 마이그레이션하려는 Access 데이터베이스에 대 한 메타 데이터가 포함 된 파일이 프로젝트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 대상 인스턴스에 대 한 메타 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 개체 및 데이터를 받을 SQL Azure 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보 및 프로젝트 설정 합니다.  
  
## <a name="reviewing-default-project-settings"></a>기본 프로젝트 설정을 검토합니다.  
SSMA는 변환 및 데이터베이스 개체를 동기화 하 고 데이터를 변환 하기 위한 몇 가지 옵션을 포함 합니다. 이러한 옵션에 대 한 기본 설정은 많은 사용자에 적합합니다. 그러나 새 SSMA 프로젝트를 만들기 전에 해야 옵션 검토을 원하는 경우 모든 새 프로젝트에 사용할 기본 설정을 변경 합니다.  
  
**기본 프로젝트 설정을 검토 하려면**  
  
1.  에 **도구** 메뉴에서 **기본 프로젝트 설정**합니다.  
  
2.  라는 프로젝트 형식을 선택 **마이그레이션 대상 버전** 설정을 볼 / 변경 하려는 및 클릭에 대 한 드롭다운 **일반** 탭 합니다.  
  
3.  왼쪽된 창에서 클릭 **변환**합니다.  
  
4.  오른쪽 창에서 옵션을 검토 합니다. 이러한 옵션에 대 한 자세한 내용은 참조 하세요. [프로젝트 설정 (변환)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)합니다.  
  
5.  필요에 따라 옵션을 변경 합니다.  
  
6.  에 대 한 이전 단계를 반복 합니다 **마이그레이션**를 **GUI**, 및 **형식 매핑** 페이지입니다.  
  
    -   마이그레이션 옵션에 대 한 자세한 내용은 [프로젝트 설정 (마이그레이션)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)합니다.  
  
    -   사용자 인터페이스 옵션에 대 한 정보를 참조 하세요 [프로젝트 설정 (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)합니다.  
  
    -   데이터 형식 매핑 설정에 대 한 자세한 내용은 참조 하십시오 [프로젝트 설정 (형식 매핑)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)합니다.  
  
    -   SQL Azure 설정에 대 한 자세한 내용은 [프로젝트 설정 (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)합니다.  
  
**참고** SQL Azure 마이그레이션 프로젝트를 만드는 동안 선택한 경우에 SQL Azure 설정이 제공 됩니다.  
  
## <a name="creating-new-projects"></a>새 프로젝트 만들기  
SSMA는 기본 프로젝트를 로드 하지 않고 시작 합니다. Access 데이터베이스에서 데이터를 마이그레이션하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 프로젝트를 만들어야 합니다.  
  
**새 프로젝트를 만들려면**  
  
1.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **이름** 입력란에 프로젝트 이름을  
  
3.  에 **위치** 상자에 입력 하거나 프로젝트에 대 한 폴더를 선택 합니다.  
  
4.  마이그레이션에 드롭에서 다운, SQL Server 2005 중 하나를 선택 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / SQL Server 2016 / Azure SQL DB를 클릭 하 고 **확인**합니다.  
  
SSMA는 프로젝트 파일을 만듭니다. 이제 다음 단계를 수행할 수 있습니다 [하나 이상의 Access 데이터베이스 추가](adding-and-removing-access-database-files-accesstosql.md)합니다.  
  
## <a name="customizing-project-settings"></a>사용자 지정 프로젝트 설정  
또한 모든 새 SSMA 프로젝트에 적용 하는 기본 프로젝트 설정을 정의 하는 것 외에도 각 프로젝트에 대 한 설정을 사용자 지정할 수 있습니다. 자세한 내용은 [설정 변환 및 마이그레이션 옵션](setting-conversion-and-migration-options-accesstosql.md)합니다.  
  
원본 및 대상 데이터베이스 간의 데이터 형식 매핑 사용자 지정 하는 경우 프로젝트, 데이터베이스 또는 개체 수준에서 매핑을 정의할 수 있습니다. 형식 매핑에 대 한 자세한 내용은 참조 하세요. [매핑 소스 및 대상 데이터 형식](mapping-source-and-target-data-types-accesstosql.md)합니다.  
  
## <a name="saving-projects"></a>프로젝트를 저장합니다.  
프로젝트를 저장 하면 SSMA 프로젝트 설정 및 선택적으로 프로젝트 파일에는 데이터베이스 메타 데이터를 유지 합니다.  
  
**프로젝트를 저장 하려면**  
  
-   에 **파일** 메뉴에서 **프로젝트 저장**합니다.  
  
    데이터베이스 프로젝트 내에서 변경 또는 변환 되지 않은 경우 프로젝트에 메타 데이터를 저장 하 SSMA 메시지가 나타납니다. 메타 데이터를 저장 하면 오프 라인으로 작업 합니다. 또한 기술 지원 요원을 비롯 한 다른 사용자에 게 전체 프로젝트 파일을 보낼 수 있습니다. 메타 데이터를 저장 하 라는 메시지가 나타나면 다음을 수행 합니다.  
  
    1.  각 데이터베이스의 상태를 보여 주는 **메타 데이터 누락**, 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
        메타 데이터를 저장 하면 몇 분 정도 걸릴 수 있습니다. 이 시점에서 메타 데이터를 저장 하지 않을 경우 모든 확인란을 선택 하지 마십시오.  
  
    2.  **저장**을 클릭합니다.  
  
        SSMA는 Access 스키마를 구문 분석 하 고 프로젝트 파일에 메타 데이터를 저장 합니다.  
  
## <a name="opening-projects"></a>열린 프로젝트  
프로젝트를 열면에서 연결이 끊어지도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 이 기능을 사용 하면 오프 라인으로 작업할 수 있습니다. 메타 데이터 로드 데이터베이스 개체를 업데이트 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 데이터를 마이그레이션하려면 다시 연결 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
**프로젝트를 열려면**  
  
1.  다음 절차 중 하나를 사용 합니다.  
  
    -   에 **파일** 메뉴에서 **최근에 사용한 프로젝트**, 다음 열려는 프로젝트를 선택 하 고 있습니다.  
  
    -   에 **파일** 메뉴에서 **프로젝트 열기**.a2ssproj 프로젝트 파일 찾기, 파일을 선택 및 클릭 **열기**.  
  
2.  에 다시 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 **파일** 메뉴에서 **SQL Server에 다시 연결**.  
  
3.  SQL Azure 다시 연결 합니다 **파일** 메뉴에서 **SQL Azure 다시 연결 합니다.**  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스에서 다음 단계 [하나 이상의 Access 데이터베이스 추가](adding-and-removing-access-database-files-accesstosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Access 데이터베이스 파일 추가 및 제거](adding-and-removing-access-database-files-accesstosql.md)  
  
