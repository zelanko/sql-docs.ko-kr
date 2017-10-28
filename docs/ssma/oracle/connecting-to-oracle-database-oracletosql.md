---
title: "Oracle 데이터베이스 (OracleToSQL)에 연결 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6a4ac43e0f79e8f7841f8f9d4234ccdd988a7b6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-oracle-database-oracletosql"></a>Oracle 데이터베이스 (OracleToSQL)에 연결
Oracle 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 마이그레이션할 수 있는 Oracle 데이터베이스에 연결 해야 합니다. 에 연결할 때 SSMA는 모든 Oracle 스키마에 대 한 메타 데이터를 가져오고 Oracle 메타 데이터 탐색기 창에 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지 않습니다.  
  
데이터베이스에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 활성 연결 하려는 경우 다시 연결 해야 합니다.  
  
Oracle 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. 대신, Oracle 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려는 경우 수동으로 업데이트 해야 것입니다. 자세한 내용은이 항목의 뒷부분에 나오는 "Oracle 메타 데이터 새로 고침" 섹션을 참조 하십시오.  
  
## <a name="required-oracle-permissions"></a>필요한 Oracle 권한  
Oracle 데이터베이스에 연결 하는 데 사용 되는 계정에 적어도 있어야 **연결** 사용 권한. 따라서 SSMA를 연결 하는 사용자가 소유한 스키마에서 메타 데이터를 가져올 수 있습니다. 다른 스키마에서 개체에 대 한 메타 데이터를 가져올 하 한 다음 이러한 스키마의 개체를 변환, 계정에는 다음 권한이 있어야 합니다.  
  
-   모든 프로시저 만들기  
  
-   모든 프로시저를 실행 합니다.  
  
-   모두 선택  
  
-   모든 시퀀스를 선택 합니다.  
  
-   모든 형식 만들기  
  
-   모든 트리거 만들기  
  
-   모든 사전을 선택 합니다.  
  
## <a name="establishing-a-connection-to-oracle"></a>Oracle에 대 한 연결을 설정합니다.  
데이터베이스에 연결할 때 SSMA는 데이터베이스 메타 데이터를 읽고 후 프로젝트 파일을이 메타 데이터를 추가 합니다. 개체를 변환 하는 경우이 메타 데이터 SSMA 사용한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문에 대 한 데이터를 마이그레이션할 때와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. Oracle 메타 데이터 탐색기 창에서이 메타 데이터를 찾아볼 수 있으며 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 연결 하려고 하기 전에 데이터베이스 서버가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**Oracle에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **Connect to Oracle**합니다.  
  
    이전에 Oracle에 연결 하는 경우 명령 이름 됩니다 **Oracle에 다시 연결**합니다.  
  
2.  에 **공급자** 상자 **Oracle 클라이언트 공급자** 또는 **OLE DB Provider**어떤 공급자가 설치에 따라 합니다. 기본값은 Oracle 클라이언트.  
  
3.  에 **모드** 상자 **표준 모드**, **TNSNAME 모드**, 또는 **연결 문자열 모드**합니다.  
  
    표준 모드를 사용 하 여 서버 이름과 포트를 지정 합니다. Oracle 서비스 이름을 수동으로 지정 하려면 서비스 이름 모드를 사용 합니다. 연결 문자열 모드를 사용 하 여 전체 연결 문자열을 제공 합니다.  
  
4.  선택 하는 경우 **표준 모드**를 다음 값을 제공 합니다.  
  
    1.  에 **서버 이름** 입력란에 입력 하거나 이름 또는 데이터베이스 서버의 IP 주소를 선택 합니다.  
  
    2.  데이터베이스 서버에 연결을 허용 하도록 구성 되지 않은 경우 기본 포트 (1521),이에서 Oracle 연결에 사용 되는 포트 번호를 입력 하는 **서버 포트** 상자입니다.  
  
    3.  에 **Oracle SID** 상자 시스템 식별자를 입력 합니다.  
  
    4.  에 **사용자 이름** 상자에 필요한 사용 권한이 있는 Oracle 계정을 입력 합니다.  
  
    5.  에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
5.  선택 하는 경우 **TNSNAME 모드**를 다음 값을 제공 합니다.  
  
    1.  에 **식별자 연결** 상자에 입력 합니다 (TNS 별칭) 데이터베이스의 식별자를 연결 합니다.  
  
    2.  에 **사용자 이름** 상자에 필요한 사용 권한이 있는 Oracle 계정을 입력 합니다.  
  
    3.  에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
6.  선택 하는 경우 **연결 문자열 모드**에서 연결 문자열을 제공 된 **연결 문자열** 상자입니다.  
  
    다음 예제에서는 OLE DB 연결 문자열을 보여 줍니다.  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    다음 예제에서는 통합된 보안을 사용 하는 Oracle 클라이언트 연결 문자열을 보여 줍니다.  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    자세한 내용은 참조 [Oracle에 연결 &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)합니다.  
  
## <a name="reconnecting-to-oracle"></a>Oracle에 다시 연결  
데이터베이스 서버에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 활성 연결 하려는 경우 다시 연결 해야 합니다. 메타 데이터를 업데이트, 데이터베이스 개체를 로드 하려면 될 때까지 오프 라인으로 작업할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 데이터를 마이그레이션합니다.  
  
## <a name="refreshing-oracle-metadata"></a>Oracle 메타 데이터 새로 고침  
Oracle 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. Oracle 메타 데이터 탐색기에서 메타 데이터는 수동으로 메타 데이터를 새로 고치는 마지막으로 또는 처음 연결 하는 경우 메타 데이터의 스냅숏입니다. 모든 스키마, 단일 스키마 또는 개별 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  데이터베이스에 연결 되어 있는지 확인 합니다.  
  
2.  Oracle 메타 데이터 탐색기에서 업데이트 하려는 각 스키마 또는 데이터베이스 개체 옆의 확인란을 선택 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **스키마**, 개별 스키마 또는 데이터베이스 개체를 선택한 후 **데이터베이스에서 새로 고침**합니다.  
  
    활성 연결이 없는 경우에 SSMA 표시 됩니다는 **Connect to Oracle** 대화 상자를 연결할 수 있습니다.  
  
4.  데이터베이스 대화 상자에서 새로 고침에 새로 고침 할 개체를 지정 합니다.  
  
    -   개체를 새로 고치려면 클릭는 **활성** 화살표가 나타날 때까지 개체 옆에 필드입니다.  
  
    -   개체를 새로 고치 되지 않게 하려면 클릭는 **활성** 될 때까지 개체에 인접 한 필드는 **X** 나타납니다.  
  
    -   새로 고치거 나 거부할 개체의 범주를 클릭 하 여는 **활성** 범주 폴더에 인접 하는 필드입니다.  
  
    색 구분의 정의 보려면 클릭는 **범례** 단추입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>다음 단계  
  
-   마이그레이션 프로세스의 다음 단계에서는 [SQL Server의 인스턴스에 연결](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server &#40; OracleToSQL &#41; Oracle 데이터베이스 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

