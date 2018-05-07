---
title: D b 2 용 SSMA 시작 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
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
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 10e2df8ac76797a8781716c75bc8cd83d0686ce7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>D b 2 용 SSMA 시작 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) DB2 사용 하면 신속 하 게에 대 한 변환 DB2 데이터베이스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 결과 스키마를 업로드 하는 스키마, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 를 d b 2에서 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
이 항목 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있습니다.  
  
## <a name="installing-ssma"></a>SSMA를 설치합니다.  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램 원본 DB2 데이터베이스와의 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 실행 중인 컴퓨터의 DB2 OLEDB 공급자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이러한 구성 요소는 데이터 마이그레이션 및 DB2 시스템 함수의 에뮬레이션을 지원합니다. 설치 지침을 참조 하십시오. [d b 2 용 SSMA 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)합니다.  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**, 가리킨  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for d b 2**, 클릭 하 고  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for d b 2**합니다.  
  
## <a name="ssma-for-db2-user-interface"></a>DB2 사용자 인터페이스용 SSMA  
SSMA를 설치한 후에 DB2 데이터베이스를 마이그레이션할 SSMA를 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 시작 하기 전에 SSMA 사용자 인터페이스에 잘 알고 있을 수 있습니다. 다음 다이어그램은 SSMA를 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창에 대 한 사용자 인터페이스를 보여 줍니다.  
  
![SSMA 사용자 인터페이스](../../ssma/db2/media/ssma_db2_ui.png "SSMA 사용자 인터페이스")  
  
마이그레이션을 시작 하려면 새 프로젝트를 먼저 만들어야 할 합니다. 그런 다음 DB2 데이터베이스에 연결 합니다. 연결 완료 후 DB2 스키마는 DB2 메타 데이터 탐색기에 표시 됩니다. 와 같은 작업을 수행 하는 DB2 메타 데이터 탐색기에서 마우스 오른쪽 단추로 개체 변환이 평가 하는 보고서를 만들 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 도구 모음과 메뉴를 사용 하 여 이러한 작업을 수행할 수도 있습니다.  
  
인스턴스에 연결 해야 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 계층 구조 라는 연결 완료 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스가에 나타납니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기입니다. DB2 스키마를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마에서 이러한 변환 된 스키마 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기와 스키마를 만든 다음 동기화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
변환 된 스키마를 동기화 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], DB2 메타 데이터 탐색기로 되돌린으로 DB2 스키마에서 데이터를 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스.  
  
이러한 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [DB2 데이터베이스를 SQL Server로 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)합니다.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능을 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA 포함을 찾아서 d b 2에서 작업을 수행할 두 메타 데이터 탐색기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스.  
  
#### <a name="db2-metadata-explorer"></a>DB2 메타 데이터 탐색기  
DB2 메타 데이터 탐색기 DB2 스키마에 대 한 정보를 표시 합니다. DB2 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 스키마의 개체를 찾아봅니다.  
  
-   변환에 대 한 개체를 선택 하 고 다음 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문입니다. 자세한 내용은 참조 [DB2 스키마 변환 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)합니다.  
  
-   데이터 마이그레이션에 대 한 테이블을 선택한 다음 해당 테이블에서 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [DB2 데이터베이스를 SQL Server로 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)합니다.  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server 메타 데이터 탐색기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 대 한 정보를 표시 하는 메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 인스턴스로 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변환 된 DB2 데이터베이스 개체를 선택한 다음 해당 개체의 인스턴스와 동기화 메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭이 있습니다. 예를 들어 DB2 메타 데이터 탐색기에서 테이블을 선택 하는 경우 6 개의 탭 표시 됩니다: **테이블**, **SQL**, **유형 매핑, 보고서**, **속성**, 및 **데이터**합니다. **보고서** 탭 선택된 된 개체를 포함 하는 보고서를 만든 후에 정보를 포함 합니다. 테이블을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기 세 가지 탭이 표시 됩니다: **테이블**, **SQL**, 및 **데이터**합니다.  
  
대부분의 설정은 메타 데이터는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   DB2 메타 데이터 탐색기에서 프로시저를 변경 하 고 형식 매핑을 수 있습니다. 변경 된 프로시저를 변환 및 형식 매핑을, 스키마를 변환 하기 전에 변경 내용을 확인 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변경할 수 있습니다 메타 데이터 탐색기는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 저장된 프로시저에 대 한 합니다. 이러한 변경 내용을 확인할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)],으로 스키마를 로드 하기 전에 이러한 변경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
메타 데이터 탐색기에서 변경 내용을 원본 또는 대상 데이터베이스에 없는 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음 프로젝트 작업, DB2에 연결에 연결 하기 위한 단추가 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이 단추에 명령을 유사는 **파일** 메뉴.  
  
#### <a name="migration-toolbar"></a>마이그레이션 도구 모음  
다음 표에서 마이그레이션 도구 모음 명령을 보여 줍니다.  
  
|단추|함수|  
|------|--------|  
|**보고서 만들기**|선택한 DB2 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문 다음 얼마나 성공적인 변환 작업이 보여 주는 보고서를 만듭니다.<br /><br />이 명령은 DB2 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**스키마 변환**|선택한 DB2 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체입니다.<br /><br />이 명령은 DB2 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**데이터 마이그레이션**|DB2 데이터베이스에서 데이터를 마이그레이션하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. DB2 스키마를 변환 해야이 명령을 실행 하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마가 개체를 로드 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br />이 명령은 DB2 메타 데이터 탐색기에서 개체를 선택한 경우가 아니면 비활성화 됩니다.|  
|**중지**|현재 프로세스를 중지합니다.|  
  
### <a name="menus"></a>메뉴  
다음 표에서 SSMA 메뉴를 보여 줍니다.  
  
|메뉴|Description|  
|----|-----------|  
|**파일**|프로젝트 작업, DB2에 연결에 연결 하기 위한 명령이 포함 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.|  
|**편집**|검색 및 텍스트를 복사 하는 등의 세부 정보 페이지에서 작업 하기 위한 명령이 포함 되어 [!INCLUDE[tsql](../../includes/tsql_md.md)] SQL 세부 정보 창에서. 도 포함 되어는 **관리 책갈피** 여기서 기존 책갈피의 목록을 볼 수는 옵션입니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **동기화 메타 데이터 탐색기** 명령입니다. DB2 메타 데이터 탐색기 간에 개체를 동기화 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기입니다. 표시 하거나 숨기는 명령이 포함 되어는 **출력** 및 **오류 목록** 창과 옵션 **레이아웃** 레이아웃을 관리 하 합니다.|  
|**Tools**|보고서를 만들고 개체 및 데이터 마이그레이션에 명령이 포함 됩니다. 또한에 대 한 액세스를 제공 된 **전역 설정** 및 **프로젝트 설정** 대화 상자.|  
|**도움말**|SSMA 있도록 및에 대 한 액세스를 제공는 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창 및 오류 목록 창  
**보기** 메뉴는 출력 창 및 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환, 개체 동기화 및 데이터 마이그레이션 중 SSMA에서 상태 메시지를 표시 합니다.  
  
-   오류 목록 창 정렬 가능한 목록에서 오류, 경고 및 정보 메시지를 표시 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[DB2 데이터를 SQL Server로 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[사용자 인터페이스 참조 &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
