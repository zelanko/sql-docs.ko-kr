---
title: Oracle Database에 연결 (OracleToSQL) | Microsoft Docs
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
manager: shamikg
ms.openlocfilehash: fc25c36a0d0133975414f4c7270da2974b552f40
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266194"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Oracle 데이터베이스에 연결(OracleToSQL)
Oracle 데이터베이스를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하려면 마이그레이션하려는 oracle 데이터베이스에 연결 해야 합니다. 연결할 때 SSMA는 모든 Oracle 스키마에 대 한 메타 데이터를 가져온 다음 Oracle 메타 데이터 탐색기 창에 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
데이터베이스에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 데이터베이스에 대 한 활성 연결을 원하는 경우 다시 연결 해야 합니다.  
  
Oracle 데이터베이스에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. 대신 Oracle 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "Oracle 메타 데이터 새로 고침" 섹션을 참조 하십시오.  
  
## <a name="required-oracle-permissions"></a>필요한 Oracle 권한  
Oracle 데이터베이스에 연결 하는 데 사용 되는 계정에는 최소한 **연결** 권한이 있어야 합니다. 이렇게 하면 SSMA가 연결 하는 사용자가 소유한 스키마에서 메타 데이터를 가져올 수 있습니다. 다른 스키마의 개체에 대 한 메타 데이터를 가져온 다음 해당 스키마의 개체를 변환 하려면 계정에 다음 사용 권한이 있어야 합니다.  
  
-   프로시저 만들기  
  
-   프로시저 실행  
  
-   테이블 선택  
  
-   시퀀스 선택  
  
-   모든 형식 만들기  
  
-   트리거를 만듭니다.  
  
-   사전 선택  
  
## <a name="establishing-a-connection-to-oracle"></a>Oracle에 대 한 연결 설정  
데이터베이스에 연결 하는 경우 SSMA는 데이터베이스 메타 데이터를 읽은 다음이 메타 데이터를 프로젝트 파일에 추가 합니다. 이 메타 데이터는 SSMA에서 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문으로 변환 하는 경우와 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션할 때 사용 됩니다. Oracle 메타 데이터 탐색기 창에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 연결을 시도 하기 전에 데이터베이스 서버가 실행 중이 고 연결을 허용할 수 있는지 확인 합니다.  
  
**Oracle에 연결 하려면**  
  
1.  **파일** 메뉴에서 **Oracle에 연결**을 선택 합니다.  
  
    이전에 Oracle에 연결한 경우 명령 이름이 **oracle에 다시 연결**됩니다.  
  
2.  **공급자** 상자에서 설치 된 공급자에 따라 **Oracle 클라이언트 공급자** 또는 **OLE DB 공급자**를 선택 합니다. 기본값은 Oracle client입니다.  
  
3.  **모드** 상자에서 **표준 모드**, **Tnsname 모드**또는 **연결 문자열 모드**중 하나를 선택 합니다.  
  
    표준 모드를 사용 하 여 서버 이름 및 포트를 지정 합니다. 서비스 이름 모드를 사용 하 여 Oracle 서비스 이름을 수동으로 지정 합니다. 연결 문자열 모드를 사용 하 여 전체 연결 문자열을 제공 합니다.  
  
4.  **표준 모드**를 선택 하는 경우 다음 값을 제공 합니다.  
  
    1.  **서버 이름** 상자에서 데이터베이스 서버의 이름 또는 IP 주소를 입력 하거나 선택 합니다.  
  
    2.  데이터베이스 서버가 기본 포트 (1521)의 연결을 허용 하도록 구성 되어 있지 않은 경우 **서버 포트** 상자에서 Oracle 연결에 사용 되는 포트 번호를 입력 합니다.  
  
    3.  **ORACLE SID** 상자에 시스템 식별자를 입력 합니다.  
  
    4.  **사용자 이름** 상자에 필요한 사용 권한이 있는 Oracle 계정을 입력 합니다.  
  
    5.  **암호** 상자에 지정 된 사용자 이름의 암호를 입력 합니다.  
  
5.  **Tnsname 모드**를 선택 하는 경우 다음 값을 제공 합니다.  
  
    1.  **연결 식별자** 상자에 데이터베이스의 연결 식별자 (TNS alias)를 입력 합니다.  
  
    2.  **사용자 이름** 상자에 필요한 사용 권한이 있는 Oracle 계정을 입력 합니다.  
  
    3.  **암호** 상자에 지정 된 사용자 이름의 암호를 입력 합니다.  
  
6.  **연결 문자열 모드**를 선택 하는 **경우 연결 문자열 상자에** 연결 문자열을 입력 합니다.  
  
    다음 예에서는 OLE DB 연결 문자열을 보여 줍니다.  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    다음 예에서는 통합 보안을 사용 하는 Oracle 클라이언트 연결 문자열을 보여 줍니다.  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    자세한 내용은 [Connect To Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)을 참조 하세요.  
  
## <a name="reconnecting-to-oracle"></a>Oracle에 다시 연결  
데이터베이스 서버에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 데이터베이스에 대 한 활성 연결을 원하는 경우 다시 연결 해야 합니다. 메타 데이터를 업데이트 하 고, 데이터베이스 개체를에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로드 하 고, 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
## <a name="refreshing-oracle-metadata"></a>Oracle 메타 데이터 새로 고침  
Oracle 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. Oracle 메타 데이터 탐색기의 메타 데이터는 처음 연결 될 때 또는 메타 데이터를 마지막으로 새로 고친 시간에 메타 데이터에 대 한 스냅숏입니다. 모든 스키마, 단일 스키마 또는 개별 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  데이터베이스에 연결 되어 있는지 확인 합니다.  
  
2.  Oracle 메타 데이터 탐색기에서 업데이트 하려는 각 스키마 또는 데이터베이스 개체 옆의 확인란을 선택 합니다.  
  
3.  **스키마**를 마우스 오른쪽 단추로 클릭 하거나 개별 스키마 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 새로 고침**을 선택 합니다.  
  
    활성 연결이 없는 경우 SSMA는 연결할 수 있도록 **Oracle에 연결** 대화 상자를 표시 합니다.  
  
4.  데이터베이스에서 새로 고침 대화 상자에서 새로 고칠 개체를 지정 합니다.  
  
    -   개체를 새로 고치려면 화살표가 나타날 때까지 개체 옆에 있는 **활성** 필드를 클릭 합니다.  
  
    -   개체를 새로 고치지 않으려면 **X** 가 나타날 때까지 개체 옆에 있는 **활성** 필드를 클릭 합니다.  
  
    -   개체의 범주를 새로 고치거 나 거부 하려면 category 폴더 옆의 **활성** 필드를 클릭 합니다.  
  
    색 구분의 정의를 보려면 **범례** 단추를 클릭 합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>다음 단계  
  
-   마이그레이션 프로세스의 다음 단계는 [SQL Server 인스턴스에 연결](connecting-to-sql-server-oracletosql.md)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
