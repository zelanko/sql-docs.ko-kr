---
title: D b 2 용 SSMA 시작 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0eab4f23e342c95d83baa70dd03aba2f5d4bc8d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989643"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>D b 2 용 SSMA 시작 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 용 SSMA (Migration Assistant)를 사용 하면 DB2 데이터베이스 스키마를 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 신속 하 게 변환 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 결과 스키마를에 업로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하 고, db2에서로 데이터를 마이그레이션할 수 있습니다.  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스를 숙지 하는 방법을 설명 합니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA를 사용 하려면 먼저 원본 DB2 데이터베이스와 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터에 SSMA 클라이언트 프로그램을 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 을 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하는 컴퓨터의 DB2 OLEDB 공급자입니다. 이러한 구성 요소는 데이터 마이그레이션과 DB2 시스템 함수의 에뮬레이션을 지원 합니다. 설치 지침은 [DB2 용 SSMA &#40;DB2ToSQL&#41;설치 ](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)를 참조 하세요.  
  
Ssma를 시작 하려면 **시작**을 클릭 하 고 **모든 프로그램**, d b 2에 ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대 한 Migration Assistant**를 차례로 가리킨 다음 ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] db2 Migration Assistant**를 클릭 합니다.  
  
## <a name="ssma-for-db2-user-interface"></a>D b 2 용 SSMA 사용자 인터페이스  
SSMA가 설치 된 후 SSMA를 사용 하 여 DB2 데이터베이스를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션할 수 있습니다. 시작 하기 전에 SSMA 사용자 인터페이스에 익숙해질 수 있습니다. 다음 다이어그램은 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창을 포함 하 여 SSMA의 사용자 인터페이스를 보여 줍니다.  
  
![SSMA 사용자 인터페이스](../../ssma/db2/media/ssma_db2_ui.png "SSMA 사용자 인터페이스")  
  
마이그레이션을 시작 하려면 먼저 새 프로젝트를 만들어야 합니다. 그런 다음 DB2 데이터베이스에 연결 합니다. 성공적으로 연결 되 면 db2 스키마가 DB2 메타 데이터 탐색기에 나타납니다. 그런 다음 DB2 메타 데이터 탐색기에서 개체를 마우스 오른쪽 단추로 클릭 하 여로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 변환을 평가 하는 보고서 만들기와 같은 태스크를 수행할 수 있습니다. 도구 모음 및 메뉴를 사용 하 여 이러한 작업을 수행할 수도 있습니다.  
  
또한 인스턴스에 연결 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 연결에 성공 하면 메타 데이터 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 계층이 표시 됩니다. DB2 스키마를 스키마로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환한 후 메타 데이터 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 된 스키마를 선택한 다음 스키마를와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]동기화 합니다.  
  
변환 된 스키마를와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]동기화 한 후 Db2 Metadata Explorer로 돌아가서 db2 스키마에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스로 데이터를 마이그레이션할 수 있습니다.  
  
이러한 작업 및 이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 [DB2 데이터베이스를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션 ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)을 참조 하세요.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 대해 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA에는 DB2 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 작업을 검색 하 고 수행 하기 위한 두 개의 메타 데이터 탐색기가 포함 됩니다.  
  
#### <a name="db2-metadata-explorer"></a>DB2 메타 데이터 탐색기  
DB2 메타 데이터 탐색기는 DB2 스키마에 대 한 정보를 표시 합니다. DB2 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 스키마에서 개체를 찾습니다.  
  
-   변환할 개체를 선택한 다음 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문으로 변환 합니다. 자세한 내용은 [DB2 스키마 변환 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)을 참조 하세요.  
  
-   데이터 마이그레이션을 위한 테이블을 선택 하 고 해당 테이블의 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션합니다. 자세한 내용은 [DB2 데이터베이스를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션 ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)을 참조 하세요.  
  
#### <a name="sql-server-metadata-explorer"></a>메타 데이터 탐색기 SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메타 데이터 탐색기에는 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]정보가 표시 됩니다. 인스턴스에 연결 하면 ssma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 해당 인스턴스에 대 한 메타 데이터를 검색 하 여 프로젝트 파일에 저장 합니다.  
  
메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 변환 된 DB2 데이터베이스 개체를 선택한 다음 해당 개체를 인스턴스와 동기화 할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]수 있습니다.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 DB2 메타 데이터 탐색기에서 테이블을 선택 하면 **테이블**, **SQL**, **형식 매핑, 보고서**, **속성**및 **데이터**와 같은 6 개의 탭이 표시 됩니다. 선택한 개체가 포함 된 보고서를 만든 후에만 **보고서** 탭에 정보가 포함 됩니다. 메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 테이블을 선택 하면 **테이블**, **SQL**및 **데이터**라는 세 개의 탭이 표시 됩니다.  
  
대부분의 메타 데이터 설정은 읽기 전용입니다. 그러나 다음 메타 데이터를 변경할 수 있습니다.  
  
-   DB2 메타 데이터 탐색기에서 프로시저 및 형식 매핑을 변경할 수 있습니다. 변경 된 프로시저와 형식 매핑을 변환 하려면 스키마를 변환 하기 전에 변경 해야 합니다.  
  
-   메타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 탐색기에서 저장 프로시저에 대 [!INCLUDE[tsql](../../includes/tsql-md.md)] 한를 변경할 수 있습니다. 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이러한 변경 내용을 보려면에 스키마를 로드 하기 전에 이러한 변경을 수행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
메타 데이터 탐색기에서 변경한 내용은 원본 또는 대상 데이터베이스가 아니라 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA에는 프로젝트 도구 모음과 마이그레이션 도구 모음 이라는 두 가지 도구 모음이 있습니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음에는 프로젝트로 작업 하 고, d b 2에 연결 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],에 연결 하는 단추가 포함 되어 있습니다. 이러한 단추는 **파일** 메뉴의 명령과 유사 합니다.  
  
#### <a name="migration-toolbar"></a>마이그레이션 도구 모음  
다음 표에서는 마이그레이션 도구 모음 명령을 보여 줍니다.  
  
|단추|함수|  
|------|--------|  
|**보고서 만들기**|선택한 DB2 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문으로 변환한 다음 변환의 성공 여부를 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 DB2 메타 데이터 탐색기에서 개체를 선택 하지 않으면 사용할 수 없습니다.|  
|**스키마 변환**|선택한 DB2 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체로 변환 합니다.<br /><br />이 명령은 DB2 메타 데이터 탐색기에서 개체를 선택 하지 않으면 사용할 수 없습니다.|  
|**데이터 마이그레이션**|DB2 데이터베이스에서로 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션합니다. 이 명령을 실행 하기 전에 DB2 스키마를 스키마로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환한 다음 개체를에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로드 해야 합니다.<br /><br />이 명령은 DB2 메타 데이터 탐색기에서 개체를 선택 하지 않으면 사용할 수 없습니다.|  
|**중지**|현재 프로세스를 중지 합니다.|  
  
### <a name="menus"></a>메뉴  
다음 표에서는 SSMA 메뉴를 보여 줍니다.  
  
|메뉴|Description|  
|----|-----------|  
|**파일**|에는 프로젝트 작업, d b 2에 연결 및 연결에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]한 명령이 포함 되어 있습니다.|  
|**편집**|SQL 세부 정보 창에서 복사 [!INCLUDE[tsql](../../includes/tsql-md.md)] 와 같이 세부 정보 페이지에서 텍스트를 찾고 사용 하는 명령이 포함 되어 있습니다. 또한에는 기존 책갈피 목록을 볼 수 있는 **책갈피 관리** 옵션도 포함 되어 있습니다. 대화 상자의 오른쪽에 있는 단추를 사용 하 여 책갈피를 관리할 수 있습니다.|  
|**보기**|**메타 데이터 탐색기 동기화** 명령을 포함 합니다. DB2 메타 데이터 탐색기와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기 간에 개체를 동기화 합니다. 에는 **출력** 및 **오류 목록** 창 및 레이아웃을 관리 하는 옵션 **레이아웃** 을 표시 하 고 숨기는 명령도 포함 됩니다.|  
|**도구**|보고서를 만들고 개체와 데이터를 마이그레이션하는 명령을 포함 합니다. 또한 **전역 설정** 및 **프로젝트 설정** 대화 상자에 대 한 액세스를 제공 합니다.|  
|**도움말**|SSMA 도움말과 정보 대화 상자에 대 **한** 액세스를 제공 합니다.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창의 표시 여부를 전환 하는 명령을 제공 합니다.  
  
-   출력 창에는 개체 변환, 개체 동기화 및 데이터 마이그레이션 중에 SSMA의 상태 메시지가 표시 됩니다.  
  
-   오류 목록 창에는 정렬 가능한 목록에서 오류, 경고 및 정보 메시지가 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[DB2 데이터를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[DB2ToSQL&#41;&#40;사용자 인터페이스 참조](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
