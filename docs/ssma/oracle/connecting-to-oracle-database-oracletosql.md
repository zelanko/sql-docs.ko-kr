---
title: Oracle 데이터베이스 (OracleToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 4ad868122fd8986c642bace1b2c9cf419bb89182
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288396"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Oracle 데이터베이스에 연결(OracleToSQL)
Oracle 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 마이그레이션하려는 Oracle 데이터베이스에 연결 해야 합니다. 에 연결 하면 SSMA는 모든 Oracle 스키마에 대 한 메타 데이터를 가져오고 Oracle 메타 데이터 탐색기 창에 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지 않습니다.  
  
데이터베이스에 대 한 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 대 한 활성 연결 하려는 경우 다시 연결 해야 합니다.  
  
Oracle 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. 대신 Oracle 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려는 경우 수동으로 업데이트 해야 해당 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "Oracle 메타 데이터 새로 고침" 섹션을 참조 하세요.  
  
## <a name="required-oracle-permissions"></a>필요한 Oracle 권한  
Oracle 데이터베이스에 연결 하는 데 사용 되는 계정을 하나 이상 있어야 합니다 **CONNECT** 권한. 이렇게 하면 SSMA를 연결 하는 사용자가 소유한 스키마에서 메타 데이터를 가져올 수 있습니다. 다른 스키마에서 개체에 대 한 메타 데이터를 가져올 다음 해당 스키마에서 개체를 변환 하 고 계정에 다음 권한이 있어야 합니다.  
  
-   모든 프로시저 만들기  
  
-   모든 프로시저를 실행 합니다.  
  
-   테이블 선택  
  
-   시퀀스를 선택 합니다.  
  
-   모든 형식 만들기  
  
-   모든 트리거 만들기  
  
-   모든 사전 선택  
  
## <a name="establishing-a-connection-to-oracle"></a>Oracle에 연결  
데이터베이스에 연결할 때 SSMA는 데이터베이스 메타 데이터를 읽고 프로젝트 파일에이 메타 데이터를 추가 합니다. 개체를 변환 하는 경우이 메타 데이터 SSMA 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문 및 데이터를 마이그레이션한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. Oracle 메타 데이터 탐색기 창에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 연결 하려고 하기 전에 데이터베이스 서버가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**Oracle에 연결 하려면**  
  
1.  에 **파일** 메뉴에서 **Connect to Oracle**합니다.  
  
    이전에 Oracle에 연결 하는 경우 명령 이름 됩니다 **Oracle에 다시 연결**합니다.  
  
2.  에 **공급자** 상자에서 **Oracle Client 공급자** 또는 **OLE DB Provider**는 공급자가 설치에 따라 합니다. 기본값은 Oracle 클라이언트.  
  
3.  에 **모드** 상자 중 하나를 선택 합니다 **표준 모드**에 **TNSNAME 모드**, 또는 **연결 문자열 모드**합니다.  
  
    서버 이름 및 포트를 지정 하려면 표준 모드를 사용 합니다. Oracle 서비스 이름을 수동으로 지정 하려면 서비스 이름과 모드를 사용 합니다. 연결 문자열 모드를 사용 하 여 전체 연결 문자열을 제공 합니다.  
  
4.  선택 하는 경우 **표준 모드**, 다음 값을 제공 합니다.  
  
    1.  에 **서버 이름** 상자에 입력 하거나 이름 또는 데이터베이스 서버의 IP 주소를 선택 합니다.  
  
    2.  데이터베이스 서버에 연결을 허용 하도록 구성 되지 않은 경우 기본 포트 (1521),이에서 Oracle 연결에 사용 되는 포트 번호를 입력 하는 합니다 **서버 포트** 상자입니다.  
  
    3.  에 **Oracle SID** 시스템 식별자를 입력 합니다.  
  
    4.  에 **사용자 이름** 상자에서 필요한 사용 권한이 있는 Oracle 계정을 입력 합니다.  
  
    5.  에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
5.  선택 하는 경우 **TNSNAME 모드**, 다음 값을 제공 합니다.  
  
    1.  에 **식별자 연결** 상자에 입력 합니다 (TNS 별칭) 데이터베이스의 식별자를 연결 합니다.  
  
    2.  에 **사용자 이름** 상자에서 필요한 사용 권한이 있는 Oracle 계정을 입력 합니다.  
  
    3.  에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
6.  선택 하는 경우 **연결 문자열 모드**에서 연결 문자열을 제공 합니다 **연결 문자열** 상자입니다.  
  
    다음 예제에서는 OLE DB 연결 문자열을 보여 줍니다.  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    다음 예제에서는 통합된 보안을 사용 하는 Oracle 클라이언트 연결 문자열을 보여 줍니다.  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    자세한 내용은 [Oracle에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)합니다.  
  
## <a name="reconnecting-to-oracle"></a>Oracle에 다시 연결  
데이터베이스 서버에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 대 한 활성 연결 하려는 경우 다시 연결 해야 합니다. 메타 데이터 업데이트를 데이터베이스 개체에 로드 될 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터를 마이그레이션합니다.  
  
## <a name="refreshing-oracle-metadata"></a>Oracle 메타 데이터를 새로 고치는 중  
Oracle 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. Oracle 메타 데이터 탐색기에서 메타 데이터를 수동으로 메타 데이터를 새로 고칠는 마지막 시간 또는 처음 연결할 때 메타 데이터의 스냅숏입니다. 모든 스키마, 단일 스키마 또는 개별 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  데이터베이스에 연결 되어 있는지 확인 합니다.  
  
2.  Oracle 메타 데이터 탐색기에서 업데이트 하려는 각 스키마 또는 데이터베이스 개체 옆의 확인란을 선택 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **스키마**, 개별 스키마 또는 데이터베이스 개체를 선택한 후 **데이터베이스에서 새로 고침**합니다.  
  
    활성 연결이 없으면 SSMA 표시 됩니다는 **Connect to Oracle** 대화 상자는 연결할 수 있도록 합니다.  
  
4.  데이터베이스 대화 상자에서 새로 고침에서 새로 고침 하는 개체를 지정 합니다.  
  
    -   개체를 새로 고치려면 클릭 합니다 **활성** 화살표가 나타날 때까지 개체 옆에 있는 필드입니다.  
  
    -   개체를 새로 고치을 방지 하려면 클릭 합니다 **Active** 때까지 개체에 인접 한 필드를 **X** 나타납니다.  
  
    -   새로 고치거 나 개체의 범주를 거부를 클릭 합니다 **활성** 필드 옆에 있는 범주 폴더입니다.  
  
    색 구분의 정의 보려면 클릭 합니다 **범례** 단추입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>다음 단계  
  
-   마이그레이션 프로세스에서 다음 단계 [SQL Server 인스턴스에 연결할](connecting-to-sql-server-oracletosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server로 데이터베이스 마이그레이션 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
