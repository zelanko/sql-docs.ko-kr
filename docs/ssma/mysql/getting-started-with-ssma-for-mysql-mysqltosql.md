---
title: MySQL 용 SSMA 시작 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5a1adb6d9354dc870c11fab0a68f6c92e704ebfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67984541"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>MySQL용 SSMA 시작(MySQLToSQL)
Mysql 용 SSMA (SQL Server Migration Assistant)를 사용 하면 MySQL 데이터베이스 스키마를 SQL Server 또는 Azure SQL DB 스키마로 신속 하 게 변환 하 고, 결과 스키마를 SQL Server 또는 Azure SQL DB로 업로드 하 고, MySQL에서 SQL Server 또는 Azure SQL DB로 데이터를 마이그레이션할 수 있습니다.  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스를 숙지 하는 방법을 설명 합니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA를 사용 하려면 먼저 SQL Server 또는 Azure SQL DB의 원본 MySQL 데이터베이스와 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터에 SSMA 클라이언트 프로그램을 설치 해야 합니다. 그런 다음 SSMA 클라이언트 프로그램을 실행 하는 컴퓨터에 MySQL 공급자 (MySQL ODBC 5.1 드라이버 (신뢰할 수 있음))를 설치 합니다. 설치 지침은 [MySQL 용 SSMA 설치 &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md) 를 참조 하세요.  
  
SSMA를 시작 하려면 **시작**을 클릭 하 고 **모든 프로그램**, **mysql에 대 한 SQL Server Migration Assistant**를 차례로 가리킨 다음 **SQL Server Migration Assistant mysql**을 클릭 합니다.  
  
## <a name="ssma-for-mysql-user-interface"></a>MySQL 사용자 인터페이스용 SSMA  
SSMA가 설치 되 고 사용이 허가 된 후 SSMA를 사용 하 여 MySQL 데이터베이스를 SQL Server 또는 Azure SQL DB로 마이그레이션할 수 있습니다. 시작 하기 전에 SSMA 사용자 인터페이스에 익숙해질 수 있습니다. 다음 다이어그램은 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창을 포함 하 여 SSMA의 사용자 인터페이스를 보여 줍니다.  
  
![MySQL 그래픽 사용자 인터페이스용 SSMA](../../ssma/mysql/media/ssmaformysqlgui.gif "MySQL 그래픽 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 다음을 수행 해야 합니다.  
  
1.  새 프로젝트 만들기  
  
2.  MySQL 데이터베이스에 연결 합니다.  
  
3.  성공적으로 연결 되 면 mysql 스키마가 MySQL 메타 데이터 탐색기에 나타납니다. MySQL 메타 데이터 탐색기에서 개체를 마우스 오른쪽 단추로 클릭 하 SQL Server/Azure SQL DB로의 변환을 평가 하는 보고서 만들기와 같은 태스크를 수행 합니다.  
  
도구 모음 및 메뉴를 사용 하 여 이러한 작업을 수행할 수도 있습니다.  
  
또한 SQL Server 인스턴스에 연결 해야 합니다. 연결이 성공적으로 완료 되 면 SQL Server 메타 데이터 탐색기에 SQL Server 데이터베이스 계층이 표시 됩니다. MySQL 스키마를 SQL Server 스키마로 변환한 후 SQL Server 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고 스키마를 SQL Server와 동기화 합니다.  
  
새 프로젝트의 드롭다운에서 마이그레이션 대화 상자에서 Azure SQL DB를 선택한 경우 Azure SQL DB에 연결 해야 합니다. 성공적으로 연결 되 면 azure sql DB 데이터베이스의 계층이 Azure SQL DB 메타 데이터 탐색기에 나타납니다. MySQL 스키마를 Azure SQL DB 스키마로 변환한 후에 Azure SQL DB 메타 데이터 탐색기에서 변환 된 스키마를 선택 하 고 Azure SQL DB와 스키마를 동기화 합니다.  
  
변환 된 스키마를 SQL Server 또는 Azure SQL DB와 동기화 한 후 MySQL Metadata Explorer로 돌아가서 MySQL 스키마에서 SQL Server 또는 Azure SQL DB 데이터베이스로 데이터를 마이그레이션할 수 있습니다.  
  
이러한 작업 및 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 [MySQL 데이터베이스를 SQL Server로 마이그레이션-AZURE SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)을 참조 하세요.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 대해 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA는 MySQL 및 SQL Server 데이터베이스에 대 한 작업을 검색 하 고 수행 하는 두 개의 메타 데이터 탐색기를 포함 합니다.  
  
### <a name="mysql-metadata-explorer"></a>MySQL 메타 데이터 탐색기  
Mysql 메타 데이터 탐색기는 MySQL 스키마에 대 한 정보를 표시 합니다. MySQL 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 스키마에서 개체를 찾습니다.  
  
-   변환할 개체를 선택한 다음 개체를 SQL Server 구문으로 변환 합니다. 자세한 내용은 [&#40;MySQLToSQL&#41;MySQL 데이터베이스 변환](../../ssma/mysql/converting-mysql-databases-mysqltosql.md) (영문)을 참조 하세요.  
  
-   데이터 마이그레이션을 위한 테이블을 선택 하 고 해당 테이블의 데이터를 SQL Server로 마이그레이션합니다. 자세한 내용은 [MySQL 데이터를 SQL Server로 마이그레이션-AZURE SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md) 를 참조 하세요.  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 또는 Azure SQL DB 메타 데이터 탐색기  
SQL Server 또는 Azure SQL DB 메타 데이터 탐색기는 SQL Server 또는 Azure SQL DB의 인스턴스에 대 한 정보를 표시 합니다. SQL Server 또는 Azure SQL DB 인스턴스에 연결 하는 경우 SSMA는 해당 인스턴스에 대 한 메타 데이터를 검색 하 여 프로젝트 파일에 저장 합니다.  
  
이 메타 데이터 탐색기를 사용 하 여 변환 된 MySQL 데이터베이스 개체를 선택한 다음 해당 개체를 SQL Server 또는 Azure SQL DB 인스턴스와 동기화 할 수 있습니다.  
  
자세한 내용은 [동기화 (MySQL to SQL Server/AZURE SQL DB)](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3) 를 참조 하세요.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 MySQL 메타 데이터 탐색기에서 테이블을 선택 하면 **테이블**, **SQL**, **형식 매핑**, **데이터**, **설정**, **문자 집합 매핑**, **SQL 모드**, **속성**및 **보고서**와 같은 9 개의 탭이 표시 됩니다. 선택한 개체가 포함 된 보고서를 만든 후에만 **보고서** 탭에 정보가 포함 됩니다. 메타 데이터 탐색기 SQL Server에서 테이블을 선택 하면 **테이블**, **SQL** 및 **데이터**라는 세 개의 탭이 표시 됩니다.  
  
대부분의 메타 데이터 설정은 읽기 전용입니다. 그러나 다음 메타 데이터를 변경할 수 있습니다.  
  
-   MySQL 메타 데이터 탐색기에서 형식 매핑, 문자 집합 매핑, SQL 모드를 변경할 수 있습니다. 변경 된 형식 매핑 또는 문자 집합 매핑 또는 SQL 모드를 변환 하려면 스키마를 변환 하기 전에 변경 해야 합니다.  
  
-   SQL Server 메타 데이터 탐색기에서 테이블 탭의 테이블 및 인덱스 속성을 변경할 수 있습니다. SQL Server에서 이러한 변경 내용을 확인 하려면 SQL Server에 스키마를 로드 하기 전에 이러한 변경을 수행 합니다.  
  
메타 데이터 탐색기에서 변경한 내용은 원본 또는 대상 데이터베이스가 아니라 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA에는 프로젝트 도구 모음과 마이그레이션 도구 모음 이라는 두 가지 도구 모음이 있습니다.  
  
### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음에는 프로젝트 작업, MySQL에 연결, SQL Server 또는 Azure SQL DB에 연결 하는 단추가 포함 되어 있습니다. 이러한 단추는 **파일** 메뉴의 명령과 유사 합니다.  
  
### <a name="migration-toolbar"></a>마이그레이션 도구 모음  
다음 표에서는 마이그레이션 도구 모음 명령을 보여 줍니다.  
  
|||  
|-|-|  
|**단추**|**칩셋용으로**|  
|**보고서 만들기**|선택한 MySQL 개체를 SQL Server 또는 Azure SQL DB 개체로 변환한 후 변환의 성공 여부를 보여 주는 보고서를 만듭니다.<br /><br />MySQL 메타 데이터 탐색기에서 개체를 선택 하지 않은 경우에는이 명령을 사용할 수 없습니다.|  
|**스키마 변환**|선택한 MySQL 개체를 SQL Server 또는 Azure SQL DB 개체로 변환 합니다.<br /><br />MySQL 메타 데이터 탐색기에서 개체를 선택 하지 않은 경우에는이 명령을 사용할 수 없습니다.|  
|**데이터 마이그레이션**|MySQL 데이터베이스에서 SQL Server 또는 Azure SQL DB로 데이터를 마이그레이션합니다. 이 명령을 실행 하기 전에 MySQL 스키마를 SQL Server 또는 Azure SQL DB 스키마로 변환한 다음 개체를 SQL Server 또는 Azure SQL DB로 로드 해야 합니다.<br /><br />MySQL 메타 데이터 탐색기에서 개체를 선택 하지 않은 경우에는이 명령을 사용할 수 없습니다.|  
|**중지**|현재 프로세스를 중지 합니다.|  
  
### <a name="menus"></a>메뉴  
다음 표에서는 SSMA 메뉴를 보여 줍니다.  
  
|||  
|-|-|  
|**메뉴**|**설명**|  
|**파일**|프로젝트 작업, MySQL에 연결, SQL Server 또는 Azure SQL DB에 연결에 대 한 명령이 포함 되어 있습니다.|  
|**편집**|세부 정보 페이지에서 텍스트를 찾고 사용 하는 명령이 포함 되어 있습니다. **책갈피 관리** 대화 상자를 열려면 편집 메뉴에서 책갈피 관리를 클릭 합니다. 대화 상자에서 기존 책갈피의 목록이 표시 됩니다. 대화 상자의 오른쪽에 있는 단추를 사용 하 여 책갈피를 관리할 수 있습니다.|  
|**보기**|**메타 데이터 탐색기 동기화** 명령을 포함 합니다. MySQL 메타 데이터 탐색기와 SQL Server 또는 Azure SQL DB 메타 데이터 탐색기 간에 개체를 동기화 합니다. 에는 **출력과** **오류 목록** 창 및 레이아웃을 사용 하 여 관리 하는 옵션 **레이아웃** 을 표시 하 고 숨기는 명령도 포함 됩니다.|  
|**도구**|보고서를 만들고, 스키마를 변환 하 고, 데이터베이스에서 새로 고치고, 개체 및 데이터를 마이그레이션하고, 스크립트로 저장 하는 명령을 포함 합니다. 또한 **전역 설정, 기본 프로젝트 설정** 및 **프로젝트 설정** 대화 상자에 대 한 액세스를 제공 합니다.|  
|**도움말**|SSMA 도움말과 정보 대화 상자에 대 **한** 액세스를 제공 합니다.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창의 표시 여부를 전환 하는 명령을 제공 합니다.  
  
-   출력 창에는 개체 변환, 개체 동기화 및 데이터 마이그레이션 중에 SSMA의 상태 메시지가 표시 됩니다.  
  
-   오류 목록 창에는 정렬 가능한 목록에서 오류, 경고 및 정보 메시지가 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQLToSQL&#41;&#40;사용자 인터페이스 참조](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[MySQL 데이터를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
