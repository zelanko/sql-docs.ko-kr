---
title: Access에 대 한 SQL Server Migration Assistant 시작 | Microsoft Docs
description: SSMA를 사용 하 여 Access 데이터베이스 개체를 SQL Server 또는 Azure SQL Database 개체로 변환 하 고, 결과 개체를 업로드 하 고, 데이터를 마이그레이션하는 작업을 시작 합니다.
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: e49e55c31e346671f7f66a42e23c39e7a64e3808
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293950"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>액세스를 위한 SQL Server Migration Assistant 시작 (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access 용 SSMA (Migration Assistant)를 사용 하면 Access 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL db 개체로 신속 하 게 변환 하 고, 결과 개체를 또는 azure SQL db로 업로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고, access에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 azure sql db로 데이터를 마이그레이션할 수 있습니다. 필요한 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AZURE SQL db에서 기존 access 프런트 엔드 응용 프로그램을 계속 사용할 수 있도록 액세스 테이블을 또는 AZURE SQL db 테이블에 연결할 수도 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스를 익히는 데 도움을 줍니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA를 사용 하려면 먼저 마이그레이션하려는 데이터베이스와 대상 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 모두에 액세스할 수 있는 컴퓨터에 ssma 클라이언트 프로그램을 설치 해야 합니다. 설치 지침은 [AccessToSQL&#41;&#40;액세스 SQL Server Migration Assistant 설치 ](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)를 참조 하세요.  
  
SSMA를 시작 하려면 **시작**을 클릭 하 고 **모든 프로그램**, **액세스 SQL Server Migration Assistant**을 차례로 가리킨 다음 **액세스를 위한 SQL Server Migration Assistant**를 선택 합니다.  
  
## <a name="using-ssma"></a>SSMA 사용  
SSMA를 설치한 후에는 도구를 사용 하 여 Access 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB로 마이그레이션하기 전에 ssma 사용자 인터페이스를 익히는 데 도움이 됩니다. 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창이 포함 된 SSMA 사용자 인터페이스가 다음 다이어그램에 표시 됩니다.  
  
![Access 그래픽 사용자 인터페이스용 SSMA](../../ssma/access/media/ssmaforaccessgui.gif "Access 그래픽 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 새 프로젝트를 만든 다음 access 데이터베이스를 추가 하 여 메타 데이터 탐색기에 액세스 합니다. 그런 다음 액세스 메타 데이터 탐색기에서 개체를 마우스 오른쪽 단추로 클릭 하 여 다음과 같은 작업을 수행할 수 있습니다.
- 또는 Azure SQL DB로 Access 데이터베이스 개체의 인벤토리 내보내기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
- 또는 Azure SQL DB로의 변환을 평가 하는 보고서를 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
- 액세스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 스키마로 변환 합니다.

도구 모음 및 메뉴를 사용 하 여 이러한 작업을 수행할 수도 있습니다.  
  
또한 인스턴스에 연결 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 연결에 성공 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기에 데이터베이스 계층이 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 액세스 스키마를 스키마로 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고에 스키마를 로드할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
새 프로젝트의 드롭다운에서 마이그레이션 대화 상자에서 Azure SQL DB를 선택한 경우 Azure SQL DB에 연결 해야 합니다. 성공적으로 연결 되 면 azure sql db 데이터베이스의 계층이 Azure SQL DB 메타 데이터 탐색기에 나타납니다. 액세스 스키마를 Azure SQL DB 스키마로 변환한 후에는 Azure SQL DB 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고에 스키마를 로드할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
변환 된 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL db로 로드 한 후에는를 반환 하 여 메타 데이터 탐색기에 액세스 하 고 access 데이터베이스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE sql db 데이터베이스로 데이터를 마이그레이션할 수 있습니다. 필요한 경우 액세스 테이블을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 테이블에 연결할 수도 있습니다.  
  
이러한 작업 및 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하십시오.  
  
-   [마이그레이션을 위해 Access 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [SQL Server에 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 대해 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA는 액세스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 데이터베이스에 대 한 작업을 탐색 하 고 수행 하는 데 사용할 수 있는 두 개의 메타 데이터 탐색기를 포함 합니다.  
  
#### <a name="access-metadata-explorer"></a>메타데이터 탐색기에 액세스  
액세스 메타 데이터 탐색기에는 프로젝트에 추가 된 액세스 데이터베이스에 대 한 정보가 표시 됩니다. Access 데이터베이스를 추가 하면 SSMA에서 해당 데이터베이스에 대 한 메타 데이터 (Access Metadata Explorer에서 사용할 수 있는 메타 데이터)를 검색 합니다.  
  
액세스 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 Access 데이터베이스에서 테이블을 찾습니다.  
  
-   변환할 개체를 선택 하 고 개체를 구문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)을 참조 하세요.  
  
-   데이터 마이그레이션을 위한 개체를 선택 하 고 해당 개체의 데이터를로 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SQL Server로 Access 데이터 마이그레이션](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)을 참조 하세요.  
  
-   액세스 및 테이블 연결 및 연결 해제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 또는 Azure SQL DB 메타 데이터 탐색기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 Azure SQL DB 메타 데이터 탐색기에 인스턴스 또는 Azure SQL DB에 대 한 정보가 표시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]또는 AZURE SQL DB 인스턴스에 연결 하는 경우 SSMA는 해당 인스턴스에 대 한 메타 데이터를 검색 하 여 프로젝트 파일에 저장 합니다.  
  
SQL Server 또는 Azure SQL DB 메타 데이터 탐색기를 사용 하 여 변환 된 Access 데이터베이스 개체를 선택 하 고 해당 개체를 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL db로 로드 (동기화) 할 수 있습니다.  
  
자세한 내용은 [SQL Server로 변환 된 데이터베이스 개체 로드](loading-converted-database-objects-into-sql-server-accesstosql.md)를 참조 하세요.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 액세스 메타 데이터 탐색기에서 테이블을 선택 하는 경우 **테이블**, **형식 매핑**, **속성**및 **데이터**라는 네 개의 탭이 표시 됩니다. 메타 데이터 탐색기에서 테이블을 선택 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **테이블**, **SQL**및 **데이터**라는 세 개의 탭이 표시 됩니다.  
  
대부분의 메타 데이터 설정은 읽기 전용입니다. 그러나 다음 메타 데이터를 변경할 수 있습니다.  
  
-   액세스 메타 데이터 탐색기에서 형식 매핑을 변경할 수 있습니다. 보고서를 만들거나 스키마를 변환 하기 전에 이러한 변경을 수행 해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메타 데이터 탐색기에서 **테이블** 탭의 테이블 및 인덱스 속성을 변경할 수 있습니다. 스키마를에 로드 하기 전에 이러한 변경 작업을 수행 하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)을 참조 하세요.  
  
### <a name="toolbars"></a>도구 모음  
SSMA에는 프로젝트 도구 모음과 마이그레이션 도구 모음 이라는 두 가지 도구 모음이 있습니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음에는 프로젝트를 사용 하 고, Access 데이터베이스 파일을 추가 하 고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB에 연결 하는 단추가 포함 되어 있습니다. 이러한 단추는 **파일** 메뉴의 명령과 유사 합니다.  
  
#### <a name="the-migration-toolbar"></a>마이그레이션 도구 모음  
마이그레이션 도구 모음에는 다음 명령이 포함 되어 있습니다.  
  
|단추|함수|  
|----------|------------|  
|**변환, 로드 및 마이그레이션**|Access 데이터베이스를 변환 하 고, 변환 된 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL db로 로드 하 고, 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE sql db로 마이그레이션합니다.|  
|**보고서 만들기**|선택한 액세스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 구문으로 변환한 후 변환의 성공 여부를 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 Access Metadata Explorer에서 개체를 선택한 경우에만 사용할 수 있습니다.|  
|**스키마 변환**|선택한 액세스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 스키마로 변환 합니다.<br /><br />이 명령은 Access Metadata Explorer에서 개체를 선택한 경우에만 사용할 수 있습니다.|  
|**데이터 마이그레이션**|Access 데이터베이스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB로 데이터를 마이그레이션합니다. 이 명령을 실행 하기 전에 액세스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL db 스키마로 변환한 다음 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE sql db로 로드 해야 합니다.<br /><br />이 명령은 Access Metadata Explorer에서 개체를 선택한 경우에만 사용할 수 있습니다.|  
|**중지**|개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB 구문으로 변환 하는 등의 방법으로 현재 프로세스를 중지 합니다.|  
  
### <a name="menus"></a>메뉴  
SSMA에는 다음 메뉴가 포함 됩니다.  
  
|메뉴|Description|  
|--------|---------------|  
|**최근에 사용한 파일**|마이그레이션 마법사, 프로젝트 작업, Access 데이터베이스 파일 추가 및 제거, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 AZURE SQL DB에 연결에 대 한 명령이 포함 되어 있습니다.|  
|**편집**|SQL 세부 정보 창에서 복사와 같이 세부 정보 페이지에서 텍스트를 찾고 사용 하는 명령이 포함 되어 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . **책갈피 관리** 대화 상자를 열려면 편집 메뉴에서 책갈피 관리를 클릭 합니다. 대화 상자에 기존 책갈피의 목록이 표시 됩니다. 대화 상자의 오른쪽에 있는 단추를 사용 하 여 책갈피를 관리할 수 있습니다.|  
|**보기**|**메타 데이터 탐색기 동기화** 명령을 포함 합니다. 그러면 액세스 메타 데이터 탐색기와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AZURE SQL DB 메타 데이터 탐색기 간의 개체가 동기화 됩니다. 에는 **출력** 및 **오류 목록** 창과 레이아웃을 관리 하는 옵션 **레이아웃** 을 표시 하 고 숨기는 명령도 포함 되어 있습니다.|  
|**Tools**|보고서를 만들고, 데이터를 내보내고, 개체 및 데이터를 마이그레이션하고, 테이블을 연결 하 고, 전역 및 프로젝트 설정 대화 상자에 대 한 액세스를 제공 하는 명령을 포함 합니다.|  
|**도움말**|SSMA 도움말과 정보 대화 상자에 대 **한** 액세스를 제공 합니다.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창의 표시 여부를 전환 하는 명령을 제공 합니다.  
  
-   출력 창에는 개체 변환, 개체 동기화 및 데이터 마이그레이션 중에 SSMA의 상태 메시지가 표시 됩니다.  
  
-   오류 목록 창에는 정렬할 수 있는 목록에서 오류, 경고 및 정보 메시지가 표시 됩니다.  
  
## <a name="see-also"></a>참조  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
