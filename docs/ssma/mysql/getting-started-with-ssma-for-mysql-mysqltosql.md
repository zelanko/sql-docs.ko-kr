---
title: (MySQLToSQL) MySQL 용 SSMA 시작 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a6ab8bdc69707374eaff1600db78abbca3ea41be
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984185"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>(MySQLToSQL) MySQL 용 SSMA 시작
SQL Server Migration Assistant (SSMA) for MySQL 사용 하 여 신속 하 게 MySQL 데이터베이스 스키마를 SQL Server 또는 Azure SQL DB 스키마로 변환, SQL Server 또는 Azure SQL DB에 결과 스키마를 업로드 및 MySQL에서 SQL Server 또는 Azure SQL DB에 데이터를 마이그레이션할 수 있습니다.  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있도록 돕습니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램 소스 MySQL 데이터베이스와 SQL Server 또는 Azure SQL DB의 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터입니다. SSMA 클라이언트 프로그램을 실행 하는 컴퓨터에서 MySQL 공급자 (MySQL ODBC 5.1 드라이버 (신뢰할 수 있는))를 설치 합니다. 설치 지침은 [MySQL 용 SSMA 설치 &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**를 가리키고 **SQL Server Migration Assistant for MySQL**, 클릭 하 고 **SQL Server 마이그레이션 MySQL에 대 한 도우미**합니다.  
  
## <a name="ssma-for-mysql-user-interface"></a>MySQL 사용자 인터페이스용 SSMA  
SSMA를 설치 및 사용이 허가 된 SQL Server 또는 Azure SQL DB에 MySQL 데이터베이스를 마이그레이션하려면 SSMA를 사용할 수 있습니다. 시작 하기 전에 SSMA 사용자 인터페이스를 사용 하 여 친숙 한 될 수 있습니다. 다음 다이어그램은 SSMA를 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창에 대 한 사용자 인터페이스를 보여줍니다.  
  
![MySql 그래픽 사용자 인터페이스용 SSMA](../../ssma/mysql/media/ssmaformysqlgui.gif "MySql 그래픽 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 다음을 수행 해야 합니다.  
  
1.  새 프로젝트를 만듭니다.  
  
2.  MySQL 데이터베이스에 연결 합니다.  
  
3.  성공적으로 연결 되 면 MySQL 스키마는 MySQL 메타 데이터 탐색기에 표시 됩니다. 와 같은 작업을 수행 하려면 MySQL 메타 데이터 탐색기에서 마우스 오른쪽 단추로 클릭 개체는 SQL Server/Azure SQL DB 변환이 평가 하는 보고서를 만듭니다.  
  
또한 도구 모음 및 메뉴를 사용 하 여 이러한 작업을 수행할 수 있습니다.  
  
또한 SQL Server 인스턴스에 연결 해야 합니다. 성공적으로 연결 되 면 SQL Server 데이터베이스의 계층 구조는 SQL Server 메타 데이터 탐색기에 표시 됩니다. MySQL 스키마를 SQL Server 스키마로 변환한 후 SQL Server 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고 SQL Server를 사용 하 여 스키마를 동기화 합니다.  
  
마이그레이션에서 Azure SQL DB 새 프로젝트 대화 상자에서 드롭다운을 선택한 경우 Azure SQL DB에 연결 해야 합니다. 성공적으로 연결 되 면 Azure SQL DB 데이터베이스의 계층 구조는 Azure SQL DB 메타 데이터 탐색기에 표시 됩니다. MySQL 스키마를 Azure SQL DB 스키마로 변환한 후 Azure SQL DB 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고 Azure SQL DB를 사용 하 여 스키마를 동기화 합니다.  
  
SQL Server 또는 Azure SQL DB를 사용 하 여 변환 된 스키마를 동기화 한 후에 MySQL 메타 데이터 탐색기를 반환 하 고 MySQL 스키마에서 SQL Server 또는 Azure SQL DB 데이터베이스로 데이터를 마이그레이션할 수 있습니다.  
  
이러한 작업 및 수행 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server-Azure SQL DB로 MySQL 데이터베이스 마이그레이션 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)합니다.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA을 찾아서 MySQL 및 SQL Server 데이터베이스에서 작업을 수행 하는 두 명의 메타 데이터 탐색기를 포함 합니다.  
  
### <a name="mysql-metadata-explorer"></a>MySQL 메타 데이터 탐색기  
MySQL 메타 데이터 탐색기는 MySQL 스키마에 대 한 정보를 표시합니다. MySQL 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 스키마의 개체를 찾아봅니다.  
  
-   변환에 대 한 개체를 선택 하 고 SQL Server 구문에 개체를 변환 합니다. 자세한 내용은 [MySQL 데이터베이스 변환 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   데이터 마이그레이션에 대 한 테이블을 선택 하 고 SQL Server에 해당 테이블에서 데이터를 마이그레이션하십시오. 자세한 내용은 [MySQL 데이터를 SQL Server-Azure SQL DB를 마이그레이션 &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 또는 Azure SQL DB 메타 데이터 탐색기  
SQL Server 또는 Azure SQL DB 메타 데이터 탐색기의 SQL Server 또는 Azure SQL DB 인스턴스에 대 한 정보를 표시 합니다. SQL Server 또는 Azure SQL DB 인스턴스에 연결 하면 SSMA 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
이 메타 데이터 탐색기를 사용 하 여 변환 된 MySQL 데이터베이스 개체를 선택 하 고 SQL Server 또는 Azure SQL DB의 인스턴스를 사용 하 여 해당 개체를 동기화 할 수 있습니다.  
  
자세한 내용은 참조 하세요. [동기화 (SQL Server에는 MySQL / Azure SQL DB)](http://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭 합니다. 예를 들어 MySQL 메타 데이터 탐색기에서 테이블을 선택 하면 9 개의 탭 표시 됩니다. **테이블**, **SQL**를 **형식 매핑**를 **데이터**,  **설정을**, **문자 집합 매핑**를 **SQL 모드**를 **속성**, 및 **보고서**합니다. 합니다 **보고서** 선택한 개체에 포함 된 보고서를 만든 후에 탭 정보를 포함 합니다. SQL Server 메타 데이터 탐색기에서 테이블을 선택 하는 경우에 세 개의 탭 표시 됩니다. **테이블**, **SQL** 하 고 **데이터**입니다.  
  
대부분의 메타 데이터 설정에는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   MySQL 메타 데이터 탐색기에서 형식 매핑, 문자 집합 매핑 SQL 모드를 변경할 수 있습니다. 변경된 형식 매핑 또는 문자 집합 매핑 또는 SQL 모드 변환할 스키마를 변환 하기 전에 변경 해야 합니다.  
  
-   SQL Server 메타 데이터 탐색기에서 테이블 탭에 테이블 및 인덱스 속성을 변경할 수 있습니다. 에서 SQL Server에서 이러한 변경 내용을 보려면 SQL Server에 스키마를 로드 하기 전에 이러한 변경 내용을 확인 합니다.  
  
메타 데이터 탐색기에서 변경 내용은 원본 또는 대상 데이터베이스에 없는 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음에 프로젝트를 사용 하 여 작업, MySQL에 연결 및 SQL Server 또는 Azure SQL DB에 연결 하는 단추가 있습니다. 이러한 단추는 명령에서 유사 합니다 **파일** 메뉴.  
  
### <a name="migration-toolbar"></a>마이그레이션 도구 모음  
다음 표에서 마이그레이션 도구 모음 명령을 보여 줍니다.  
  
|||  
|-|-|  
|**단추**|**함수**|  
|**보고서 만들기**|SQL Server 또는 Azure SQL DB 개체를 선택한 MySQL 개체를 변환 하 고 변환 얼마나 성공적인 성과 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 MySQL 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**스키마 변환**|SQL Server 또는 Azure SQL DB 개체를 선택한 MySQL 개체를 변환합니다.<br /><br />이 명령은 MySQL 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**데이터 마이그레이션**|MySQL 데이터베이스에서 SQL Server 또는 Azure SQL DB로 데이터를 마이그레이션합니다. 이 명령을 실행 하기 전에 MySQL 스키마를 SQL Server 또는 Azure SQL DB 스키마로 변환 하 고 SQL Server 또는 Azure SQL DB에 개체를 로드 합니다.<br /><br />이 명령은 MySQL 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**중지**|현재 프로세스를 중지합니다.|  
  
### <a name="menus"></a>메뉴  
다음 표에서 SSMA 메뉴를 보여 줍니다.  
  
|||  
|-|-|  
|**메뉴**|**설명**|  
|**최근에 사용한 파일**|프로젝트를 사용 하 여 작업, MySQL에 연결 및 SQL Server 또는 Azure SQL DB에 연결 하는 명령을 포함 합니다.|  
|**편집**|찾기 및 세부 정보 페이지에서 텍스트를 사용 하 여 작업에 대 한 명령을 포함 합니다. 열려는 **책갈피 관리** 대화 상자에서 편집 메뉴에서 관리 하는 책갈피를 클릭 합니다. 대화 상자에서 기존 책갈피 목록으로 표시 됩니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **메타 데이터 탐색기 동기화** 명령입니다. MySQL 메타 데이터 탐색기와 SQL Server 또는 Azure SQL DB 메타 데이터 탐색기 간에 개체를 동기화 하는 합니다. 표시 하거나 숨기려면 명령도 포함 됩니다는 **출력** 및 **오류 목록** 창과 옵션 **레이아웃** 레이아웃을 사용 하 여 관리 합니다.|  
|**Tools**|보고서를 만들고, 스키마 변환, 데이터베이스에서 새로 고침, 개체 및 데이터 마이그레이션 스크립트로 저장 하는 명령을 포함 합니다. 또한에 대 한 액세스를 제공 합니다 **전역 설정, 기본 프로젝트 설정** 하 고 **프로젝트 설정** 대화 상자.|  
|**도움말**|SSMA 데 및에 대 한 액세스를 제공 합니다 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창과 오류 목록 창  
합니다 **보기** 메뉴는 출력 창과 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환과 개체 동기화 데이터 마이그레이션 중 SSMA에서 상태 메시지를 보여 줍니다.  
  
-   오류 목록 창에 정렬 가능한 목록을의 오류, 경고 및 정보 메시지를 표시 합니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 인터페이스 참조 &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[MySQL 데이터를 SQL Server-Azure SQL DB로 마이그레이션 &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
