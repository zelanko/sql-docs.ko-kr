---
title: 액세스에 대 한 SQL Server Migration Assistant를 사용 하 여 시작 | Microsoft Docs
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
ms.openlocfilehash: 1168609d35a266f2ac5fe6641aee7ca131bc9d89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759908"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>SQL Server Migration Assistant for Access (AccessToSQL)를 사용 하 여 시작
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 액세스를 사용 하면 Access 데이터베이스 개체를 신속 하 게 변환할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 개체에 결과 개체를 업로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB에 대 한 액세스에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다. 필요에 따라 연결할 수 있습니다도 테이블에 액세스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL DB를 사용 하 여 기존 액세스 프런트 엔드 응용 프로그램을 사용 하 여 계속할 수 있도록 테이블 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다.  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있도록 합니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램에서 마이그레이션할 데이터베이스 모두에 액세스할 수 있는 컴퓨터에 대상 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다. 설치 지침은 [설치 SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)합니다.  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**를 가리킨 **SQL Server Migration Assistant for Access**를 선택한 후 **SQL Server 마이그레이션 Assistant for Access**합니다.  
  
## <a name="using-ssma"></a>SSMA를 사용 하 여  
SSMA를 설치한 후에 익숙해질 SSMA 사용자 인터페이스 도구를 사용 하 여 Access 데이터베이스를 마이그레이션 전에 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다. SSMA 사용자 인터페이스는 다음 다이어그램에 나와 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창이 포함:  
  
![Access 그래픽 사용자 인터페이스용 SSMA](../../ssma/access/media/ssmaforaccessgui.gif "Access 그래픽 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 새 프로젝트를 만들 추가한 다음 Access 데이터베이스 액세스 메타 데이터 탐색기로 합니다. 개체와 같은 작업을 수행 하는 액세스 메타 데이터 탐색기에서 마우스 오른쪽 단추로 클릭 한 다음 있습니다.
- Access 데이터베이스 개체를의 인벤토리 내보내기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다.
- 변환이 평가 하는 보고서 작성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다.
- 에 대 한 액세스 스키마 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 스키마입니다.

또한 도구 모음 및 메뉴를 사용 하 여 이러한 작업을 수행할 수 있습니다.  
  
인스턴스에 연결 해야 합니다도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 계층을 성공적으로 연결 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 나타나는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기입니다. 액세스 스키마를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마에서 변환 된 스키마를 선택할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기, 스키마 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
Azure SQL DB 마이그레이션에서 새 프로젝트 대화 상자에서 드롭다운을 선택한 경우에 Azure SQL DB에 연결 해야 합니다. 성공적으로 연결 되 면 Azure SQL DB 데이터베이스의 계층 구조는 Azure SQL DB 메타 데이터 탐색기에 표시 됩니다. Azure SQL DB 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고 다음 스키마를 로드할 수 Access 스키마를 Azure SQL DB 스키마로 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
변환 된 스키마를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있고 Azure SQL DB 액세스 메타 데이터 탐색기로 반환에 Access 데이터베이스에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 데이터베이스입니다. 필요에 따라 연결할 수 있습니다도 액세스 테이블을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 테이블입니다.  
  
이러한 작업 및 수행 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 합니다.  
  
-   [Access 데이터베이스 마이그레이션 준비](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [SQL Server에 대 한 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA을 찾아서 액세스 작업을 수행 합니다. 사용할 수 있는 두 명의 메타 데이터 탐색기를 포함 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 데이터베이스입니다.  
  
#### <a name="access-metadata-explorer"></a>메타 데이터 탐색기에 액세스  
액세스 메타 데이터 탐색기는 프로젝트에 추가 된 Access 데이터베이스에 대 한 정보를 표시 합니다. Access 데이터베이스에 추가 하면 SSMA 액세스 메타 데이터 탐색기에서 사용할 수 있는 메타 데이터는 해당 데이터베이스에 대 한 메타 데이터를 검색 합니다.  
  
다음 작업을 수행할 액세스 메타 데이터 탐색기를 사용할 수 있습니다.  
  
-   각 액세스 데이터베이스의 테이블을 찾습니다.  
  
-   변환에 대 한 개체를 선택 하 고 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문입니다. 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)합니다.  
  
-   데이터 마이그레이션에 대 한 개체를 선택 하 고 해당 개체에서 데이터를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [Access 데이터를 SQL Server를 마이그레이션](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)합니다.  
  
-   연결 및 액세스 연결 해제 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 또는 Azure SQL DB 메타 데이터 탐색기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대 한 정보를 표시 하는 Azure SQL DB 메타 데이터 탐색기 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다. 인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB, SSMA 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
변환 된 Access 데이터베이스 개체를 선택 하 고 로드 하는 SQL Server 또는 Azure SQL DB 메타 데이터 탐색기를 사용할 수 있습니다 (동기화)의 인스턴스로 해당 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다.  
  
자세한 내용은 [SQL Server로 변환 된 데이터베이스 개체 로드](loading-converted-database-objects-into-sql-server-accesstosql.md)합니다.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭 합니다. 예를 들어 액세스 메타 데이터 탐색기에서 테이블을 선택 하는 경우 4 개의 탭 표시 됩니다. **테이블**, **형식 매핑**합니다 **속성**, 및 **데이터**입니다. 테이블을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기, 세 개의 탭이 나타납니다. **테이블**하십시오 **SQL**, 및 **데이터**입니다.  
  
대부분의 메타 데이터 설정에는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   액세스 메타 데이터 탐색기에서 형식 매핑을 변경할 수 있습니다. 보고서를 만들거나 스키마로 변환 하기 전에 이러한 변경을 수행 해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기에서 테이블 및 인덱스 속성을 변경할 수 있습니다 합니다 **테이블** 탭 합니다. 스키마를 로드 하기 전에 이러한 변경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)합니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음 단추가 프로젝트로 작업 하 고, Access 데이터베이스 파일을 추가 및 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다. 이러한 단추는 명령에서 유사 합니다 **파일** 메뉴.  
  
#### <a name="the-migration-toolbar"></a>마이그레이션 도구 모음  
마이그레이션 도구 모음에는 다음 명령도 포함 됩니다.  
  
|단추|기능|  
|----------|------------|  
|**변환, 로드 및 마이그레이션**|Access 데이터베이스를 변환, 변환된 된 개체에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 및 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 한 번에 모든 Azure SQL DB입니다.|  
|**보고서 만들기**|선택한 액세스 스키마를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 구문을 다음 얼마나 성공적인 변환 된 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 액세스 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**스키마 변환**|선택한 액세스 스키마를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 스키마입니다.<br /><br />이 명령은 액세스 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**데이터 마이그레이션**|Access 데이터베이스에서 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다. 이 명령은 실행 하기 전에 액세스 스키마를 변환 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 스키마 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다.<br /><br />이 명령은 액세스 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**중지**|개체의 변환과 같은 현재 프로세스가 중지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 구문입니다.|  
  
### <a name="menus"></a>메뉴  
SSMA는 다음과 같은 메뉴가 포함 되어 있습니다.  
  
|메뉴|Description|  
|--------|---------------|  
|**최근에 사용한 파일**|마이그레이션 마법사, 프로젝트, 작업 및 추가 하 고, Access 데이터베이스 파일을 제거 하 고, 연결할 명령을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB입니다.|  
|**편집**|찾기 및 텍스트 세부 정보 페이지를 복사 하는 등의 작업에 대 한 명령을 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL 세부 정보 창에서. 열려는 합니다 **책갈피 관리** 대화 상자에서 편집 메뉴에서 관리 하는 책갈피를 클릭 합니다. 대화 상자에서 기존 책갈피 목록으로 표시 됩니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **메타 데이터 탐색기 동기화** 명령입니다. 그러면 액세스 메타 데이터 탐색기 간에 개체를 동기화 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 메타 데이터 탐색기입니다. 표시 하거나 숨기려면 명령도 포함 됩니다는 **출력** 및 **오류 목록** 창과 옵션 **레이아웃** 레이아웃을 사용 하 여 관리 합니다.|  
|**Tools**|보고서 만들기, 데이터 내보내기, 개체 및 데이터 마이그레이션, 테이블을 연결 하는 명령을 포함 하 고 대화 상자 프로젝트 설정과 전역에 대 한 액세스를 제공 합니다.|  
|**도움말**|SSMA 데 및에 대 한 액세스를 제공 합니다 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창과 오류 목록 창  
합니다 **보기** 메뉴는 출력 창과 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환과 개체 동기화 데이터 마이그레이션 중 SSMA에서 상태 메시지를 보여 줍니다.  
  
-   오류 목록 창을 정렬할 수 있는 목록에서 오류, 경고 및 정보 메시지를 보여 줍니다.  
  
## <a name="see-also"></a>참고자료  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
