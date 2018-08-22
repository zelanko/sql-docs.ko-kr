---
title: DB2 용 SSMA 시작 (DB2ToSQL) | Microsoft Docs
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
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7cd773d2d92190ece25ae2048773f2357454528e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396158"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>DB2 용 SSMA 시작 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) DB2 사용 하면 신속 하 게에 대 한 DB2 데이터베이스 스키마로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마의 경우 결과 스키마를 업로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 DB2에서 데이터를 마이그레이션하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
이 항목에서는 설치 프로세스를 소개 하 고 SSMA 사용자 인터페이스에 익숙해질 수 있도록 돕습니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA를 사용 하려면 먼저 설치 해야 SSMA 클라이언트 프로그램 DB2 원본 데이터베이스와의 대상 인스턴스 모두에 액세스할 수 있는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 실행 중인 컴퓨터의 DB2 OLEDB 공급자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이러한 구성 요소는 데이터 마이그레이션 및 DB2 시스템 함수의 에뮬레이션을 지원합니다. 설치 지침은 [DB2 용 SSMA 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)합니다.  
  
SSMA를 시작 하려면 **시작**, 가리킨 **모든 프로그램**를 가리킨  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**를 클릭 하 고  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**합니다.  
  
## <a name="ssma-for-db2-user-interface"></a>DB2 사용자 인터페이스용 SSMA  
DB2 데이터베이스를 마이그레이션하려면 SSMA SSMA를 설치한 후 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 시작 하기 전에 SSMA 사용자 인터페이스를 사용 하 여 친숙 한 될 수 있습니다. 다음 다이어그램은 SSMA를 메타 데이터 탐색기, 메타 데이터, 도구 모음, 출력 창 및 오류 목록 창에 대 한 사용자 인터페이스를 보여줍니다.  
  
![SSMA 사용자 인터페이스](../../ssma/db2/media/ssma_db2_ui.png "SSMA 사용자 인터페이스")  
  
마이그레이션을 시작 하려면 먼저 새 프로젝트를 만들어야 합니다. 그런 다음 DB2 데이터베이스에 연결할 수도 있습니다. 연결에 성공한 후 DB2 스키마는 DB2 메타 데이터 탐색기에 표시 됩니다. 와 같은 작업을 수행 하는 DB2 메타 데이터 탐색기에서 마우스 오른쪽 단추로 클릭 개체 변환이 평가 하는 보고서를 만들 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 또한 도구 모음 및 메뉴를 사용 하 여 이러한 작업을 수행할 수 있습니다.  
  
인스턴스에 연결 해야 합니다도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 계층을 성공적으로 연결 되 면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기입니다. DB2 스키마를 변환한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마에서 변환 된 스키마를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기를 사용 하 여 스키마를 추가한 다음 동기화 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
변환 된 스키마를 동기화 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 DB2 메타 데이터 탐색기를 반환 하 고 DB2 스키마에서 데이터를 마이그레이션할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
이러한 작업 및 수행 하는 방법에 대 한 자세한 내용은 참조 하세요. [DB2 데이터베이스를 SQL Server 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)합니다.  
  
다음 섹션에서는 SSMA 사용자 인터페이스의 기능에 설명 합니다.  
  
### <a name="metadata-explorers"></a>메타 데이터 탐색기  
SSMA을 찾아서 DB2에서 작업을 수행 하는 두 명의 메타 데이터 탐색기를 포함 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
#### <a name="db2-metadata-explorer"></a>DB2 메타 데이터 탐색기  
DB2 메타 데이터 탐색기는 DB2 스키마에 대 한 정보를 표시합니다. DB2 메타 데이터 탐색기를 사용 하 여 다음 작업을 수행할 수 있습니다.  
  
-   각 스키마의 개체를 찾아봅니다.  
  
-   변환에 대 한 개체를 선택 하 고 변환한 다음 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문입니다. 자세한 내용은 [DB2 스키마 변환 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)합니다.  
  
-   데이터 마이그레이션에 대 한 테이블을 선택한 다음 해당 테이블에서 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [DB2 데이터베이스를 SQL Server 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)합니다.  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server 메타 데이터 탐색기  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대 한 정보를 표시 하는 메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA 해당 인스턴스에 대 한 메타 데이터를 검색 하 고 프로젝트 파일에 저장 합니다.  
  
사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 된 DB2 데이터베이스 개체를 선택한 다음 해당 개체의 인스턴스를 사용 하 여 동기화 메타 데이터 탐색기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
### <a name="metadata"></a>메타데이터  
각 메타 데이터 탐색기의 오른쪽에는 선택한 개체를 설명 하는 탭 합니다. 예를 들어 DB2 메타 데이터 탐색기에서 테이블을 선택 하면 6 개의 탭 표시 됩니다: **테이블**, **SQL**하십시오 **형식 매핑, 보고서**, **속성**, 및 **데이터**입니다. 합니다 **보고서** 선택한 개체에 포함 된 보고서를 만든 후에 탭 정보를 포함 합니다. 테이블을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기, 세 개의 탭 표시 됩니다. **테이블**, **SQL**, 및 **데이터**.  
  
대부분의 메타 데이터 설정에는 읽기 전용입니다. 그러나 다음과 같은 메타 데이터를 변경할 수 있습니다.  
  
-   DB2 메타 데이터 탐색기에서 프로시저를 변경 하 고 형식 매핑 수 있습니다. 변경된 절차를 변환 및 형식 매핑, 스키마를 변환 하기 전에 변경 내용을 확인 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변경할 수 있습니다 메타 데이터 탐색기는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장된 프로시저에 대 한 합니다. 이러한 변경 내용을 보려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 스키마를 로드 하기 전에 이러한 변경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
메타 데이터 탐색기에서 변경 내용은 원본 또는 대상 데이터베이스에 없는 프로젝트 메타 데이터에 반영 됩니다.  
  
### <a name="toolbars"></a>도구 모음  
SSMA는 두 개의 도구 모음: 프로젝트 도구 모음 및 마이그레이션 도구 모음입니다.  
  
#### <a name="the-project-toolbar"></a>프로젝트 도구 모음  
프로젝트 도구 모음 단추가 DB2에 연결 및 연결 프로젝트 작업의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이러한 단추는 명령에서 유사 합니다 **파일** 메뉴.  
  
#### <a name="migration-toolbar"></a>마이그레이션 도구 모음  
다음 표에서 마이그레이션 도구 모음 명령을 보여 줍니다.  
  
|단추|기능|  
|------|--------|  
|**보고서 만들기**|선택한 DB2 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문을 다음 얼마나 성공적인 변환 된 보여 주는 보고서를 만듭니다.<br /><br />개체는 DB2 메타 데이터 탐색기에서 선택 하지 않으면이 명령이 비활성화 됩니다.|  
|**스키마 변환**|선택한 DB2 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체입니다.<br /><br />개체는 DB2 메타 데이터 탐색기에서 선택 하지 않으면이 명령이 비활성화 됩니다.|  
|**데이터 마이그레이션**|DB2 데이터베이스에서 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 명령은 실행 하기 전에 DB2 스키마를 변환 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.<br /><br />개체는 DB2 메타 데이터 탐색기에서 선택 하지 않으면이 명령이 비활성화 됩니다.|  
|**중지**|현재 프로세스를 중지합니다.|  
  
### <a name="menus"></a>메뉴  
다음 표에서 SSMA 메뉴를 보여 줍니다.  
  
|메뉴|Description|  
|----|-----------|  
|**최근에 사용한 파일**|프로젝트, DB2에 연결 및 작업에 연결 하기 위한 명령을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**편집**|찾기 및 텍스트 세부 정보 페이지를 복사 하는 등의 작업에 대 한 명령을 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL 세부 정보 창에서. 도 포함 되어 있습니다 합니다 **책갈피 관리** 옵션을 여기서 기존 책갈피의 목록을 볼 수는 있습니다. 책갈피를 관리 하는 대화 상자의 오른쪽에 단추를 사용할 수 있습니다.|  
|**보기**|포함 된 **메타 데이터 탐색기 동기화** 명령입니다. DB2 메타 데이터 탐색기 간에 개체를 동기화 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터 탐색기입니다. 표시 하거나 숨기려면 명령도 포함 됩니다는 **출력** 및 **오류 목록** 창과 옵션 **레이아웃** 레이아웃을 관리 합니다.|  
|**Tools**|보고서를 만들고, 개체 및 데이터를 마이그레이션하는 명령을 포함 합니다. 또한에 대 한 액세스를 제공 합니다 **전역 설정** 하 고 **프로젝트 설정** 대화 상자.|  
|**도움말**|SSMA 데 및에 대 한 액세스를 제공 합니다 **에 대 한** 대화 상자.|  
  
### <a name="output-pane-and-error-list-pane"></a>출력 창과 오류 목록 창  
합니다 **보기** 메뉴는 출력 창과 오류 목록 창 표시 유형을 전환 하려면 명령을 제공 합니다.  
  
-   출력 창 개체 변환과 개체 동기화 데이터 마이그레이션 중 SSMA에서 상태 메시지를 보여 줍니다.  
  
-   오류 목록 창에 정렬 가능한 목록을의 오류, 경고 및 정보 메시지를 표시 합니다.  
  
## <a name="see-also"></a>관련 항목  
[DB2 데이터를 SQL Server로 마이그레이션 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[사용자 인터페이스 참조 &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
