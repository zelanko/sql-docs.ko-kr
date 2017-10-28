---
title: "MySQL (MySQLToSQL)에 연결 | Microsoft Docs"
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
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
caps.latest.revision: 13
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dc29e681e7065b3f09a16504ea3fb5bd35f6d65a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-mysql-mysqltosql"></a>MySQL (MySQLToSQL)에 연결
SQL Server 또는 SQL Azure에 MySQL 데이터베이스를 마이그레이션하려면 마이그레이션할 MySQL 데이터베이스에 연결 해야 합니다. 에 연결할 때 SSMA 모든 MySQL 스키마에 대 한 메타 데이터를 가져오고 MySQL 메타 데이터 탐색기 창에 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지 않습니다.  
  
데이터베이스에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 활성 연결 하려는 경우 다시 연결 해야 합니다.  
  
MySQL 데이터베이스에 대 한 메타 데이터를 자동으로 업데이트 되지 않습니다. 대신, MySQL 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려는 경우 수동으로 업데이트 해야 것입니다. 자세한 내용은이 항목의 뒷부분에 나오는 "MySQL 메타 데이터 새로 고침" 섹션을 참조 하십시오.  
  
## <a name="required-mysql-permissions"></a>MySQL 필수 사용 권한  
MySQL 데이터베이스에 연결 하는 데 사용 되는 계정은 적어도 있어야 **연결** 사용 권한. 따라서 SSMA를 연결 하는 사용자가 소유한 스키마에서 메타 데이터를 가져올 수 있습니다. 다른 스키마에서 개체에 대 한 메타 데이터를 가져올 하 한 다음 이러한 스키마의 개체를 변환, 계정에는 다음 권한이 있어야 합니다.  
  
-   데이터베이스 개체에 대해 권한이 'SHOW'  
  
-   ' SELECT' 'Information_schema'에 대 한 권한이  
  
-   Mysql에 대 한 권한이 (Udf)에 대 한 ' SELECT'  
  
## <a name="establishing-a-connection-to-mysql"></a>MySQL에 대 한 연결을 설정합니다.  
데이터베이스에 연결할 때 SSMA는 데이터베이스 메타 데이터를 읽고 후 프로젝트 파일을이 메타 데이터를 추가 합니다. 이 메타 데이터 개체를 SQL Server 또는 SQL Azure 구문, 변환 및 SQL Server 또는 SQL Azure에 데이터를 마이그레이션하면 SSMA에서 사용 됩니다. MySQL 메타 데이터 탐색기 창에서이 메타 데이터를 찾아볼 수 있으며 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 연결 하려고 하기 전에 데이터베이스 서버가 실행 되 고 연결을 허용할 수 있는지 확인 합니다.  
  
**MySQL에 연결 하려면**  
  
1.  에 **파일** 메뉴 선택 **MySQL에 연결** (이 옵션을 설정할 프로젝트를 만든 후).  
  
    MySQL에 연결 했던 경우 명령 이름 됩니다 **MySQL에 다시 연결**합니다.  
  
2.  에 **공급자** 상자 MySQL ODBC 5.1 드라이버 (신뢰할 수 있음)를 선택 합니다. 이 표준 모드에서 기본 공급자입니다.  
  
3.  에 **모드** 상자 **표준 모드**합니다. 기본 모드입니다.  
  
    표준 모드를 사용 하 여 서버 이름과 포트를 지정 합니다.  
  
4.  **표준 모드**를 다음 값을 제공 합니다.  
  
    1.  에 **서버 이름** MySQL 서버 이름을 입력 합니다. 에 **서버 포트** 상자 3306 되도록 포트 번호를 입력 합니다. 기본 포트는 것입니다.  
  
    2.  에 **사용자 이름** 상자에 필요한 권한을 보유 하는 MySQL 계정을 입력 합니다.  
  
    3.  에 **암호** 상자에 지정된 된 사용자 이름에 대 한 암호를 입력 합니다.  
  
5.  **SSL:** MySQL에 안전 하 게 연결 하려는 경우를 확인 하 여 Secure Socket Layer (SSL)를 사용 하 여 **SSL** 확인란을 선택 합니다.  
  
6.  **구성:** MySQL 통해 SSL Secure Socket Layer ()에 대 한 연결을 구성 하는 옵션을 제공 합니다.  
  
    > [!NOTE]  
    > 사용할 수 있도록 **구성**, SSL로 설정 해야 **True**합니다.  
  
    "구성" 단추를 클릭 하는 대화 상자가 나타납니다. MySQL 데이터베이스를 대화 상자에 다음 세 가지 인증서 파일에 대 한 경로에 연결 해야 하는 동안 암호화를 사용 하려면 [개인 정보 보호 향상 된 메일 인증서 (PEM)]를 정의 합니다.  
  
    -   **SSL 인증 기관을:** 신뢰 SSL Ca ' 목록이 있는 파일 경로 지정 합니다.  
  
    -   **SSL 인증서:** 보안 연결 구성에 사용할 SSL 인증서 파일의 이름을 지정 합니다.  
  
    -   **SSL 키:** 보안 연결 구성에 사용할 SSL 키 파일의 이름을 지정 합니다.  
  
    > [!NOTE]  
    > -   **확인** 필요한 정보를 제공한 경우 단추를 사용할 수 있습니다. 유효 하지 않으면 파일 경로 있는 "확인" 단추가 비활성화 된 상태로 유지 됩니다.  
    > -   **취소** 단추 대화 상자를 닫습니다 및 **해제** 기본 연결 폼에서 SSL 옵션입니다.  
  
7.  자세한 내용은 참조 [MySQL &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>MySQL에 다시 연결  
데이터베이스 서버에 연결 된 프로젝트를 닫을 때까지 활성 상태를 유지 합니다. 프로젝트를 다시 열 때 데이터베이스에 활성 연결 하려는 경우 다시 연결 해야 합니다. , 메타 데이터를 업데이트 하 고, SQL Server 또는 SQL Azure에 데이터베이스 개체를 로드 하 고, 데이터를 마이그레이션할 때까지 오프 라인으로 작업 합니다.  
  
## <a name="refreshing-mysql-metadata"></a>MySQL 메타 데이터 새로 고침  
MySQL 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. MySQL 메타 데이터 탐색기에서 메타 데이터는 수동으로 메타 데이터를 새로 고치는 마지막으로 또는 처음 연결 하는 경우 메타 데이터의 스냅숏입니다. 모든 스키마, 단일 스키마 또는 개별 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  데이터베이스에 연결 되어 있는지 확인 합니다.  
  
2.  MySQL 메타 데이터 탐색기에서 업데이트 하려는 각 스키마 또는 데이터베이스 개체 옆의 확인란을 선택 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **스키마**, 개별 스키마 또는 데이터베이스 개체를 선택한 후 **데이터베이스에서 새로 고침**합니다.  
  
    활성 연결이 없는 경우에 SSMA 표시 됩니다는 **MySQL에 연결** 대화 상자를 연결할 수 있습니다.  
  
4.  데이터베이스 대화 상자에서 새로 고침에 새로 고침 할 개체를 지정 합니다.  
  
    -   개체를 새로 고치려면 클릭는 **활성** 화살표가 나타날 때까지 개체 옆에 필드입니다.  
  
    -   개체를 새로 고치 되지 않게 하려면 클릭는 **활성** 될 때까지 개체에 인접 한 필드는 **X** 나타납니다.  
  
    -   새로 고치거 나 거부할 개체의 범주를 클릭 하 여는 **활성** 범주 폴더에 인접 하는 필드입니다.  
  
    -   색 구분의 정의 보려면 클릭는 **범례** 단추입니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SQL Server &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

