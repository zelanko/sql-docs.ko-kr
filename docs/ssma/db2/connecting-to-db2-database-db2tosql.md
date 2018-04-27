---
title: DB2 데이터베이스 (DB2ToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6cd697c4e81482db4b23aa7eee34724d44934475
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="connecting-to-db2-database-db2tosql"></a>DB2 데이터베이스 (DB2ToSQL)에 연결
DB2 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 마이그레이션할 DB2 데이터베이스에 연결 해야 합니다. 에 연결할 때 SSMA는 모든 DB2 스키마에 대 한 메타 데이터를 가져오고 DB2 메타 데이터 탐색기 창에 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지 않습니다.  
  
데이터베이스에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 활성 연결 하려는 경우 다시 연결 해야 합니다.  
  
DB2 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. 대신, DB2 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려는 경우 수동으로 업데이트 해야 것입니다. 자세한 내용은이 항목의 뒷부분에 나오는 "DB2 메타 데이터 새로 고침" 섹션을 참조 합니다.  
  
## <a name="required-db2-permissions"></a>DB2 필수 사용 권한  
사용자 권한 부여에는 명령 및 사용자에 대해 사용할 수 있는 개체의 목록을 정의 합니다. 이 목록은 함으로써 사용자 동작을 제어합니다. D b 2에는 인스턴스 수준에서 및 DB2 데이터베이스 수준에서 권한 부여에 대 한 권한 미리 결정 된 그룹이 있습니다. 따라서 SSMA를 연결 하는 사용자가 소유한 스키마에서 메타 데이터를 가져올 수 있습니다. 다른 스키마에서 개체에 대 한 메타 데이터를 가져올 하 한 다음 이러한 스키마의 개체를 변환, 계정에는 다음 권한이 있어야 합니다.  
  
-   스키마 마이그레이션에 대 한 스키마 액세스 제한 키워드에에서 사용 되지 않았으면 만들기에 일반적으로 PUBLIC에 부여 됩니다.  
  
-   데이터 마이그레이션에 대 한 데이터에 액세스 하려면 데이터 액세스  
  
## <a name="establishing-a-connection-to-db2"></a>D b 2에 대 한 연결을 설정합니다.  
데이터베이스에 연결할 때 SSMA는 데이터베이스 메타 데이터를 읽고 후 프로젝트 파일을이 메타 데이터를 추가 합니다. 개체를 변환 하는 경우이 메타 데이터 SSMA 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문에 대 한 데이터를 마이그레이션할 때와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. DB2 메타 데이터 탐색기 창에서이 메타 데이터를 찾아볼 수 있으며 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 연결 하려고 하기 전에 데이터베이스 서버가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**D b 2에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **d b 2에 연결**합니다.  
  
    명령 이름은 d b 2에 이전에 연결한 경우 됩니다 **d b 2에 다시 연결**합니다.  
  
2.  에 **공급자** 상자가 표시 됩니다는 **OLE DB Provider** 는 현재 제공 되는 유일한 DB2 클라이언트 액세스 공급자입니다.  
  
3.  에 **관리자** 상자 중 하나를 선택할 수 있습니다 **zOs 용 Db2**, 또는 **LUW 용 DB2**  
  
4.  에 **모드** 상자 **표준 모드**, 또는 **연결 문자열 모드**합니다.  
  
    표준 모드를 사용 하 여 서버 이름과 포트를 지정 합니다. 서비스 이름 모드를 사용 하 여 DB2 서비스 이름을 수동으로 지정 하려면. 연결 문자열 모드를 사용 하 여 전체 연결 문자열을 제공 합니다.  
  
5.  선택 하는 경우 **표준 모드**를 다음 값을 제공 합니다.  
  
    -   에 **서버 이름** 입력란에 입력 하거나 이름 또는 데이터베이스 서버의 IP 주소를 선택 합니다.  
  
    -   데이터베이스 서버에 연결을 허용 하도록 구성 되지 않은 경우 기본 포트 (1521),이에서 DB2 연결에 사용 되는 포트 번호를 입력 하는 **서버 포트** 상자입니다.  
  
    -   에 **서버 포트** 상자 TCP/IP 포트 번호를 입력 합니다.  
  
    -   에 **초기 카탈로그** 데이터베이스 이름을 입력 합니다  
  
    -   에 **사용자 이름** 상자에 필요한 사용 권한이 있는 DB2 계정을 입력 합니다.  
  
    -   에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
6.  선택 하는 경우 **연결 문자열 모드**에서 연결 문자열을 제공 된 **연결 문자열** 상자입니다.  
  
    다음 예제에서는 OLE DB 연결 문자열을 보여 줍니다.  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    다음 예제에서는 통합된 보안을 사용 하는 DB2 클라이언트 연결 문자열을 보여 줍니다.  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    자세한 내용은 참조 [Oracle 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)합니다.  
  
## <a name="reconnecting-to-db2"></a>D b 2에 다시 연결  
데이터베이스 서버에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 활성 연결 하려는 경우 다시 연결 해야 합니다. 메타 데이터를 업데이트, 데이터베이스 개체를 로드 하려면 될 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 데이터를 마이그레이션합니다.  
  
## <a name="refreshing-db2-metadata"></a>DB2 메타 데이터 새로 고침  
DB2 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. DB2 메타 데이터 탐색기에 있는 메타 데이터는 수동으로 메타 데이터를 새로 고치는 마지막으로 또는 처음 연결 하는 경우 메타 데이터의 스냅숏입니다. 모든 스키마, 단일 스키마 또는 개별 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  데이터베이스에 연결 되어 있는지 확인 합니다.  
  
2.  DB2 메타 데이터 탐색기에서 업데이트 하려는 각 스키마 또는 데이터베이스 개체 옆의 확인란을 선택 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **스키마**, 개별 스키마 또는 데이터베이스 개체를 선택한 후 **데이터베이스에서 새로 고침**합니다.  
  
    활성 연결이 없는 경우에 SSMA 표시 됩니다는 **d b 2에 연결** 대화 상자를 연결할 수 있습니다.  
  
4.  데이터베이스 대화 상자에서 새로 고침에 새로 고침 할 개체를 지정 합니다.  
  
    -   개체를 새로 고치려면 클릭는 **활성** 화살표가 나타날 때까지 개체 옆에 필드입니다.  
  
    -   개체를 새로 고치 되지 않게 하려면 클릭는 **활성** 될 때까지 개체에 인접 한 필드는 **X** 나타납니다.  
  
    -   새로 고치거 나 거부할 개체의 범주를 클릭 하 여는 **활성** 범주 폴더에 인접 하는 필드입니다.  
  
    색 구분의 정의 보려면 클릭는 **범례** 단추입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>다음 단계  
  
-   마이그레이션 프로세스의 다음 단계에서는 [SQL Server에 연결](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server로 데이터베이스 마이그레이션 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
