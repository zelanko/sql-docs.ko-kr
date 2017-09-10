---
title: "MySQL (MySQLToSQL) 용 SSMA 시작 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 38ce5c0e27703094e4d7ff2415d0bc91d501d1b4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>MySQL (MySQLToSQL) 용 SSMA 시작
SQL Server Migration Assistant (SSMA) MySQL에 대 한 신속 하 게 MySQL 데이터베이스 스키마를 SQL Server 또는 Azure SQL DB 스키마로 변환 결과 스키마를 SQL Server 또는 Azure SQL DB에 업로드 하 고 MySQL에서 SQL Server 또는 Azure SQL DB에 데이터를 마이그레이션할 수 있습니다.  
  
이 항목 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있습니다.  
  
## <a name="installing-ssma"></a>SSMA를 설치합니다.  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램 원본 MySQL 데이터베이스와 SQL Server 또는 Azure SQL DB의 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터에 있습니다. SSMA 클라이언트 프로그램을 실행 하는 컴퓨터에서 MySQL 공급자 (MySQL ODBC 5.1 드라이버 (신뢰할 수 있는))를 설치 합니다. 설치 지침을 참조 하세요. [MySQL &#40; 설치 SSMA MySqlToSql &#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**, 가리킨 **SQL Server Migration Assistant for MySQL**, 클릭 하 고 **SQL Server Migration Assistant for MySQL**합니다.  
  
## <a name="ssma-for-mysql-user-interface"></a>MySQL 사용자 인터페이스용 SSMA  
SSMA는 설치 하 고 사용이 허가 되 면 SQL Server 또는 Azure SQL DB에 MySQL 데이터베이스를 마이그레이션할 SSMA를 사용할 수 있습니다. 시작 하기 전에 SSMA 사용자 인터페이스에 잘 알고 있을 수 있습니다. 다음 다이어그램은 SSMA를 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창에 대 한 사용자 인터페이스를 보여 줍니다.  
  
![MySql 그래픽 사용자 인터페이스용 SSMA](../../ssma/mysql/media/ssmaformysqlgui.gif "MySql 그래픽 사용자 인터페이스용 SSMA")  
  
마이그레이션을 시작 하려면 다음을 수행 해야 합니다.  
  
1.  새 프로젝트를 만듭니다.  
  
2.  MySQL 데이터베이스에 연결 합니다.  
  
3.  연결 완료 후 MySQL 스키마 MySQL 메타 데이터 탐색기에 표시 됩니다. 마우스 오른쪽 단추로 개체 MySQL 메타 데이터 탐색기와 같은 작업을 수행 하는 SQL Server/Azure SQL DB에 변환이 평가 하는 보고서를 만듭니다.  
  
도구 모음과 메뉴를 사용 하 여 이러한 작업을 수행할 수도 있습니다.  
  
또한 SQL Server의 인스턴스에 연결 해야 합니다. 연결 완료 후 SQL Server 데이터베이스의 계층 구조는 SQL Server 메타 데이터 탐색기에 표시 됩니다. MySQL 스키마를 SQL Server 스키마로 변환 하면 SQL Server 메타 데이터 탐색기에서 이러한 변환 된 스키마를 선택 하 고 SQL Server와 함께 스키마를 동기화 합니다.  
  
새 프로젝트 대화 상자에서 드롭다운에 Azure SQL DB 마이그레이션에서 선택한 경우에 Azure SQL DB에 연결 해야 합니다. Azure SQL DB 데이터베이스의 계층 구조는 연결 완료 후 Azure SQL DB 메타 데이터 탐색기에 표시 됩니다. Azure SQL DB 스키마를 MySQL 스키마를 변환한 후 Azure SQL DB 메타 데이터 탐색기에서 이러한 변환 된 스키마를 선택 하 고 Azure SQL DB를 통해 스키마를 동기화 하십시오.  
  
SQL Server 또는 Azure SQL DB로 변환 된 스키마를 동기화 한 후 MySQL 메타 데이터 탐색기로 돌아갑니다 및 MySQL 스키마에서 데이터를 SQL Server 또는 Azure SQL DB 데이터베이스를 마이그레이션할 수 있습니다.  
  
이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [마이그레이션 MySQL 데이터베이스를 SQL Server-Azure SQL DB &#40; MySQLToSql &#41; ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능을 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA를 찾아보고 MySQL 및 SQL Server 데이터베이스에서 작업을 수행할 두 메타 데이터 탐색기 포함 되어 있습니다.  
  
### <a name="mysql-metadata-explorer"></a>MySQL 메타 데이터 탐색기  
MySQL 메타 데이터 탐색기 MySQL 스키마에 대 한 정보를 표시 합니다. MySQL 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 스키마의 개체를 찾아봅니다.  
  
-   변환에 대 한 개체를 선택 하 고 SQL Server 구문으로 개체를 변환 합니다. 자세한 내용은 참조 [MySQL 데이터베이스 변환 &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   데이터 마이그레이션에 대 한 테이블을 선택 하 고 SQL Server에 있는 테이블에서 데이터를 마이그레이션하십시오. 자세한 내용은 참조 [를 Azure SQL DB &#40; SQL Server-MySQL 데이터 마이그레이션 MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 또는 Azure SQL DB 메타 데이터 탐색기  
SQL Server 또는 Azure SQL DB 메타 데이터 탐색기에는 SQL Server 또는 Azure SQL DB의 인스턴스에 대 한 정보가 표시 됩니다. SQL Server 또는 Azure SQL DB의 인스턴스로 연결할 때 SSMA는 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
이 메타 데이터 탐색기를 사용 하 여 변환 된 MySQL 데이터베이스 개체를 선택할 수 있으며 다음 SQL Server 또는 Azure SQL DB의 인스턴스와 해당 개체는 동기화 할 수 있습니다.  
  
자세한 내용은 참조 [동기화 (SQL Server에는 MySQL / Azure SQL DB)](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 MySQL 메타 데이터 탐색기에서 테이블을 선택 하는 경우 9 개의 탭 표시 됩니다: **테이블**, **SQL**, **유형 매핑**, **데이터**, **설정**, **Charset 매핑**, **SQL 모드**, **속성**, 및 **보고서**합니다. **보고서** 탭 선택된 된 개체를 포함 하는 보고서를 만든 후에 정보를 포함 합니다. SQL Server 메타 데이터 탐색기에서 테이블을 선택 하는 경우에 세 개의 탭 표시 됩니다: **테이블**, **SQL** 및 **데이터**합니다.  
  
대부분의 설정은 메타 데이터는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   MySQL 메타 데이터 탐색기에 형식 매핑, 문자 집합 매핑 SQL 모드를 변경할 수 있습니다. 변경 된 형식 매핑을 또는 문자 집합 매핑 또는 SQL 모드 변환할 스키마를 변환 하기 전에 변경 내용을 확인 합니다.  
  
-   SQL Server 메타 데이터 탐색기에서 테이블 탭에 테이블 및 인덱스 속성을 변경할 수 있습니다. SQL Server에서 이러한 변경 내용을 보려면 SQL Server에 스키마를 로드 하기 전에 이러한 변경 내용을 확인 합니다.  
  
메타 데이터 탐색기에서 변경 내용을 원본 또는 대상 데이터베이스에 없는 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음을 사용 하면 프로젝트 작업 MySQL에 연결 하 고 SQL Server 또는 Azure SQL DB에 연결에 대 한 단추가 있습니다. 이 단추에 명령을 유사는 **파일** 메뉴.  
  
### <a name="migration-toolbar"></a>마이그레이션 도구 모음  
다음 표에서 마이그레이션 도구 모음 명령을 보여 줍니다.  
  
|||  
|-|-|  
|**단추**|**함수**|  
|**보고서 만들기**|SQL Server 또는 Azure SQL DB 개체를 선택한 MySQL 개체를 변환 하 고 변환 작업이 얼마나 성공적인 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 MySQL 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**스키마 변환**|SQL Server 또는 Azure SQL DB 개체를 선택한 MySQL 개체를 변환합니다.<br /><br />이 명령은 MySQL 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**데이터 마이그레이션**|SQL Server 또는 Azure SQL DB에 MySQL 데이터베이스에서 데이터를 마이그레이션합니다. 이 명령을 실행 하기 전에 MySQL 스키마를 SQL Server 또는 Azure SQL DB 스키마로 변환 하 고 SQL Server 또는 Azure SQL DB에 개체를 로드 합니다.<br /><br />이 명령은 MySQL 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**중지**|현재 프로세스를 중지합니다.|  
  
### <a name="menus"></a>메뉴  
다음 표에서 SSMA 메뉴를 보여 줍니다.  
  
|||  
|-|-|  
|**메뉴**|**Description**|  
|**파일**|프로젝트 작업 MySQL에 연결 하 고 SQL Server 또는 Azure SQL DB에 연결 명령에 포함 되어 있습니다.|  
|**편집**|찾기 및 세부 정보 페이지에서 텍스트 작업에 대 한 명령을 포함 합니다. 열려는 **관리 책갈피** 대화 상자에서 편집 메뉴에서 관리 하는 책갈피를 클릭 합니다. 대화 상자에서 기존 책갈피의 목록이 표시 됩니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **동기화 메타 데이터 탐색기** 명령입니다. MySQL 메타 데이터 탐색기 및 SQL Server 또는 Azure SQL DB 메타 데이터 탐색기 간에 개체를 동기화 하는입니다. 표시 하거나 숨기는 명령이 포함 되어는 **출력** 및 **오류 목록** 창과 옵션 **레이아웃** 를 사용할 수 있는 레이아웃을 사용 하 여 관리 합니다.|  
|**Tools**|보고서를 만들고, 스키마를 변환, 데이터베이스에서 새로 고침, 개체 및 데이터를 마이그레이션할 하며 스크립트로 저장 하는 명령이 포함 됩니다. 또한에 대 한 액세스를 제공 된 **전역 설정, 기본 프로젝트 설정,** 및 **프로젝트 설정** 대화 상자.|  
|**도움말**|SSMA 있도록 및에 대 한 액세스를 제공는 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환, 개체 동기화 및 데이터 마이그레이션 중 SSMA에서 상태 메시지를 표시 합니다.  
  
-   오류 목록 창 정렬 가능한 목록에서 오류, 경고 및 정보 메시지를 표시 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[사용자 인터페이스 참조 &#40; MySQLToSQL &#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Azure SQL DB &#40; SQL Server-에 MySQL 데이터 마이그레이션 MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  

