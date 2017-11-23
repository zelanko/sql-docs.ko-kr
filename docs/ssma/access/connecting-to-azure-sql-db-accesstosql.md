---
title: "Azure SQL DB (AccessToSQL)에 연결 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
caps.latest.revision: "21"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aeba0333b93f1649673268cd35e535cb766fd076
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Azure SQL DB (AccessToSQL)에 연결
Access 데이터베이스를 SQL Azure로 마이그레이션하려면 SQL Azure의 대상 인스턴스에 연결 해야 합니다. 에 연결할 때 SSMA는 SQL Azure의 인스턴스에서 모든 데이터베이스에 대 한 메타 데이터를 가져오고 SQL Azure 메타 데이터 탐색기에서 데이터베이스 메타 데이터를 표시 합니다. SSMA는 SQL Azure의 어떤 인스턴스에 대 한 연결 되어, 않지만 암호를 저장 하지 않는 정보를 저장 합니다.  
  
SQL Azure에 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 다시 연결 해야 SQL azure 서버에 연결 되어 하려는 경우. SQL Azure에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
SQL Azure의 인스턴스에 대 한 메타 데이터를 자동으로 동기화 되지 않습니다. 대신, SQL Azure 메타 데이터 탐색기의 메타 데이터를 업데이트 하려면 SQL Azure 메타 데이터 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "SQL Azure 메타 데이터 동기화 중" 섹션을 참조 하십시오.  
  
## <a name="required-sql-azure-permissions"></a>필요한 SQL Azure 사용 권한  
SQL Azure에 연결 하는 데 사용 되는 계정에는 계정 수행 하는 작업에 따라 다른 권한이 필요 합니다.  
  
-   Access 개체를 변환 하려면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 를 SQL Azure에서 메타 데이터를 업데이트 하거나 저장 하는 변환 된 구문을 구문, 스크립트, 계정에는 SQL Azure 인스턴스에 로그온 할 수 있는 권한이 있어야 합니다.  
  
-   SQL Azure 데이터베이스 개체를 로드,의 최소 권한 요구 사항은의 멤버 자격이 **db_owner** 대상 데이터베이스의 데이터베이스 역할입니다.  
  
## <a name="establishing-a-sql-azure-connection"></a>설정 SQL Azure 연결  
SQL Azure 구문으로 액세스 데이터베이스 개체를 변환 하기 전에 Access 데이터베이스 또는 데이터베이스를 마이그레이션할 하려는 SQL Azure 인스턴스에 대 한 연결을 설정 해야 합니다.  
  
연결 속성을 정의할 때도 데이터베이스 개체와 데이터 마이그레이션할 수를 지정 합니다. SQL Azure에 연결한 후 액세스 스키마 수준에서이 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [Access 데이터베이스를 SQL Server 스키마로 매핑](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> SQL Azure에 연결 하려고 하기 전에 SQL Azure의 인스턴스가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**SQL Azure에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **SQL Azure에 연결** (이 옵션은 프로젝트를 만든 후).  
  
    명령 이름은 됩니다 이전에 SQL Azure에 연결한 경우 **SQL Azure에 다시 연결**합니다.  
  
2.  연결 대화 상자에서 입력 하거나 SQL Azure의 서버 이름을 선택 합니다.  
  
3.  선택, 입력 또는 **찾아보기** 데이터베이스 이름입니다.  
  
4.  입력 하거나 선택 **UserName**합니다.  
  
5.  입력은 **암호**합니다.  
  
6.  SSMA는 SQL Azure에 암호화 된 연결을 권장합니다.  
  
7.  **연결**을 클릭합니다.  
  
> [!IMPORTANT]  
> Access 용 SSMA 연결을 지원 하지 않습니다 **마스터** SQL Azure 데이터베이스입니다.  
  
SQL Azure 계정에서 데이터베이스가 없는 경우 사용 하 여 첫 번째 데이터베이스 만들 수 있습니다 **Azure 데이터베이스 만들기** 를 클릭할 때 표시 되는 옵션 **찾아보기** 단추입니다.  
  
## <a name="synchronizing-sql-azure-metadata"></a>동기화 SQL Azure 메타 데이터  
SQL Azure 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. SQL Azure 메타 데이터 탐색기에서 메타 데이터는 마지막 시간을 수동으로 또는 SQL Azure에 처음 연결 하는 경우 메타 데이터의 스냅숏을 메타 데이터를 업데이트 합니다. 모든 데이터베이스에 대해 또는 모든 단일 데이터베이스 또는 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 동기화 하려면**  
  
1.  SQL Azure에 연결 되어 있는지 확인 합니다.  
  
2.  SQL Azure 메타 데이터 탐색기에서 데이터베이스 또는 데이터베이스 스키마를 업데이트 하려면 옆에 있는 확인란을 선택 합니다.  
  
    예를 들어 모든 데이터베이스에 대 한 메타 데이터를 업데이트 하려면 데이터베이스 옆의 상자를 선택 합니다.  
  
3.  데이터베이스 또는 개별 데이터베이스 또는 데이터베이스 스키마를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터베이스와 동기화**합니다.  
  
## <a name="refreshing-sql-azure-metadata"></a>SQL 새로 고침 Azure 메타 데이터  
SQL Azure 스키마 변경에 연결한 후 서버에서 메타 데이터를 새로 고칠 수 있습니다.  
  
**SQL Azure 메타 데이터를 새로 고치려면**  
  
-   SQL Azure 메타 데이터 탐색기에서 마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **데이터베이스에서 새로 고침**합니다.  
  
## <a name="reconnecting-to-sql-azure"></a>SQL Azure에 다시 연결  
SQL Azure에 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 다시 연결 해야 SQL azure 서버에 연결 되어 하려는 경우. SQL Azure에 데이터베이스 개체를 로드 하 고 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
SQL Azure에 다시 연결 하는 절차에 대 한 연결을 설정 하는 절차와 같습니다.  
  
## <a name="next-step"></a>다음 단계  
다음 단계는 마이그레이션에서 프로젝트 요구 사항에 따라 달라 집니다.  
  
-   액세스 스키마 및 SQL Azure 데이터베이스와 스키마 간의 매핑, 사용자 지정 하려면 참조 [매핑 Access 데이터베이스를 SQL Server 스키마로](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)합니다.  
  
-   참조 프로젝트에 대 한 구성 옵션을 사용자 지정 하려면 [프로젝트 옵션 설정](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)합니다.  
  
-   원본 및 대상 데이터 형식 매핑, 사용자 지정 하려면 참조 [매핑 소스 및 대상 데이터 형식](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)합니다.  
  
-   이러한 작업을 수행 해야 하는 경우 SQL Azure 개체 정의를 Access 데이터베이스 개체 정의 변환할 수 있습니다. 자세한 내용은 참조 [Access 데이터베이스 변환](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
