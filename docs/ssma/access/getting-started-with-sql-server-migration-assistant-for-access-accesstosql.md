---
title: "SQL Server Migration Assistant for Access 시작 | Microsoft Docs"
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
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
caps.latest.revision: 24
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bb4a52bd22d4ab9ad2b2602704e133aa3713b064
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>SQL Server Migration Assistant for Access (AccessToSQL) 시작
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA)에 액세스 하면 신속 하 게 변환 Access 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 개체에 결과 개체의 업로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB에 대 한 액세스에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 필요한 액세스 테이블을 연결할 수도 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 와 기존 Access 프런트 엔드 응용 프로그램을 사용 하도록 계속할 수 있도록 Azure SQL DB 테이블 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다.  
  
이 항목 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있습니다.  
  
## <a name="installing-ssma"></a>SSMA를 설치합니다.  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램 마이그레이션하려는 두 데이터베이스에 액세스할 수 있는 컴퓨터와의 대상 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 설치 지침을 참조 하세요. [설치 SQL Server Migration Assistant for Access &#40; AccessToSQL &#41; ](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**, 가리킨 **SQL Server Migration Assistant for Access**를 선택한 후 **SQL Server Migration Assistant for Access**합니다.  
  
## <a name="using-ssma"></a>SSMA를 사용 하 여  
Access 데이터베이스를 마이그레이션할 SSMA SSMA를 설치한 후 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 시작 하기 전에 SSMA 사용자 인터페이스에 잘 알고 있을 수 있습니다. 다음 다이어그램에서는 SSMA 사용자 인터페이스 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창에이 포함 됩니다.  
  
![Access 그래픽 사용자 인터페이스용 SSMA](../../ssma/access/media/ssmaforaccessgui.gif "Access 그래픽 사용자 인터페이스용 SSMA")  
  
마이그레이션 시작 하 고 새 프로젝트를 만들고 다음 Access 데이터베이스 액세스 메타 데이터 탐색기에 추가 합니다. Access 데이터베이스 개체를의 인벤토리 내보내기와 같은 작업을 수행 하는 액세스 메타 데이터 탐색기에서 개체 단추로 클릭 한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 변환이 평가 하는 보고서를 만들 Azure SQL DB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 액세스 스키마를 변환 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 스키마입니다. 또한 도구 모음과 메뉴를 통해 이러한 작업을 수행할 수 있습니다.  
  
인스턴스에 연결 해야 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 계층 구조 라는 연결 완료 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스가에 나타납니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기입니다. 액세스 스키마를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마에서 이러한 변환 된 스키마를 선택할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기 다음으로 스키마를 로드 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
새 프로젝트 대화 상자에서 드롭다운에 Azure SQL DB 마이그레이션에서 선택한 경우에 Azure SQL DB에 연결 해야 합니다. Azure SQL DB 데이터베이스의 계층 구조는 연결 완료 후 Azure SQL DB 메타 데이터 탐색기에 표시 됩니다. Azure SQL DB 메타 데이터 탐색기에서 변환 된 해당 스키마를 선택 하 고 다음으로 스키마를 로드할 수 Azure SQL DB 스키마에 액세스 스키마를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
으로 변환 된 스키마를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 있고 Azure SQL DB 액세스 메타 데이터 탐색기로 돌아갑니다에 Access 데이터베이스에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 데이터베이스. 필요한 액세스 테이블을 연결할 수도 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 테이블입니다.  
  
이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 다음 섹션을 참조 합니다.  
  
-   [Access 데이터베이스 마이그레이션을 준비](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
-   [SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
-   [SQL Server에 대 한 액세스 응용 프로그램 연결](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능을 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA 포함을 찾아서 액세스 작업을 수행 하는 두 명의 메타 데이터 탐색기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 데이터베이스.  
  
#### <a name="access-metadata-explorer"></a>메타 데이터 탐색기에 액세스  
액세스 메타 데이터 탐색기는 프로젝트에 추가 된 Access 데이터베이스에 대 한 정보를 표시 합니다. SSMA는 Access 데이터베이스에 추가 하면 해당 데이터베이스에 대 한 메타 데이터를 검색 합니다. 이 액세스 메타 데이터 탐색기에서 사용할 수 있는 메타 데이터입니다.  
  
액세스 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 Access 데이터베이스의 테이블을 탐색 합니다.  
  
-   변환에 대 한 개체를 선택 하 고 다음 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문입니다. 자세한 내용은 참조 [Access 데이터베이스 개체가 변환](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)합니다.  
  
-   데이터 마이그레이션에 대 한 개체를 선택한 다음 해당 개체에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [액세스 데이터를 SQL Server로 마이그레이션](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625)합니다.  
  
-   에 연결 하 고 액세스 연결을 해제 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 테이블입니다.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 또는 Azure SQL DB 메타 데이터 탐색기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]인스턴스에 대 한 정보를 표시 하는 Azure SQL DB 메타 데이터 탐색기 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 인스턴스로 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB, SSMA 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
이 메타 데이터 탐색기를 사용 하 여 변환 된 Access 데이터베이스 개체를 선택한 다음 로드 (동기화)의 인스턴스로 해당 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다.  
  
자세한 내용은 참조 [를 SQL Server로 변환 된 데이터베이스 개체를 로드](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)합니다.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 액세스 메타 데이터 탐색기에서 테이블을 선택 하는 경우 4 개의 탭 표시 됩니다: **테이블**, **유형 매핑, 속성**, 및 **데이터**합니다. 테이블을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기 세 가지 탭이 표시 됩니다: **테이블**, **SQL**, 및 **데이터**합니다.  
  
대부분의 설정은 메타 데이터는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   액세스 메타 데이터 탐색기에 형식 매핑을 변경할 수 있습니다. 보고서를 만들거나 스키마를 변환 하기 전에 이러한 변경 내용을 확인 해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기에서 테이블 및 인덱스 속성을 변경할 수 있습니다는 **테이블** 탭 합니다. 스키마를 로드 하기 전에 이러한 변경 내용을 확인 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [Access 데이터베이스 개체가 변환](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)합니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음 프로젝트 작업 Access 데이터베이스 파일을 추가 하 고, 연결에 대 한 단추가 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 이 단추에 명령을 유사는 **파일** 메뉴.  
  
#### <a name="the-migration-toolbar"></a>마이그레이션 도구 모음  
마이그레이션 도구 모음에는 다음 명령도 포함 됩니다.  
  
|단추|함수|  
|----------|------------|  
|**변환, 로드 및 마이그레이션**|Access 데이터베이스 변환, 변환된 된 개체에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 고 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 한꺼번에 합니다.|  
|**보고서 만들기**|선택한 Access 스키마를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 구문 다음 얼마나 성공적인 변환 작업이 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 액세스 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**스키마 변환**|선택한 Access 스키마를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 스키마입니다.<br /><br />이 명령은 액세스 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**데이터 마이그레이션**|Access 데이터베이스에서 데이터를 마이그레이션하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다. 이 명령을 실행 하기 전에 액세스 스키마를 변환 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 스키마가 개체를 로드 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다.<br /><br />이 명령은 액세스 메타 데이터 탐색기에서 개체를 선택한 경우에 있습니다.|  
|**중지**|개체를 쓰는 등 현재 프로세스를 중단 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 구문이 있습니다.|  
  
### <a name="menus"></a>메뉴  
SSMA 메뉴가 포함 되어 있습니다.  
  
|메뉴|Description|  
|--------|---------------|  
|**파일**|마이그레이션 마법사, 프로젝트, 작업 및 추가 하 고, Access 데이터베이스 파일을 제거 하 고, 연결에 대 한 명령을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다.|  
|**편집**|검색 및 텍스트를 복사 하는 등의 세부 정보 페이지에서 작업 하기 위한 명령이 포함 되어 [!INCLUDE[tsql](../../includes/tsql_md.md)] SQL 세부 정보 창에서. 열려는 **관리 책갈피** 대화 상자에서 편집 메뉴에서 관리 하는 책갈피를 클릭 합니다. 대화 상자에서 기존 책갈피의 목록이 표시 됩니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **동기화 메타 데이터 탐색기** 명령입니다. 이 액세스 메타 데이터 탐색기 간에 개체를 동기화 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 메타 데이터 탐색기입니다. 표시 하거나 숨기려면 명령도 포함는 **출력** 및 **오류 목록** 창과 옵션 **레이아웃** 를 사용할 수 있는 레이아웃을 사용 하 여 관리 합니다.|  
|**Tools**|보고서 만들기, 데이터 내보내기, 개체 및 데이터 마이그레이션, 테이블을 연결 하는 명령을 포함 하 고 대화 상자 프로젝트 설정과 전역에 대 한 액세스를 제공 합니다.|  
|**도움말**|SSMA 있도록 및에 대 한 액세스를 제공는 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환, 개체 동기화 및 데이터 마이그레이션 중 SSMA에서 상태 메시지를 표시 합니다.  
  
-   오류 목록 창에 정렬할 수 있는 목록의 오류, 경고 및 정보 메시지를 표시 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

