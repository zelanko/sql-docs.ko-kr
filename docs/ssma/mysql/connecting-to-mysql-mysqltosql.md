---
title: MySQL에 연결 (MySQLToSQL) | Microsoft Docs
description: 대상 iMySQL 데이터베이스에 연결 하 여 MySQL 데이터베이스를 마이그레이션하는 방법에 대해 알아봅니다. SSMA는 Azure SQL Database의 데이터베이스에 대 한 메타 데이터를 가져옵니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0246bd83bb7ca75d464452b5b430fbef1bbf128b
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935839"
---
# <a name="connecting-to-mysql-mysqltosql"></a>MySQL에 연결(MySQLToSQL)
MySQL 데이터베이스를 SQL Server 또는 SQL Azure로 마이그레이션하려면 마이그레이션하려는 MySQL 데이터베이스에 연결 해야 합니다. 연결할 때 SSMA는 모든 MySQL 스키마에 대 한 메타 데이터를 가져온 다음 MySQL 메타 데이터 탐색기 창에 표시 합니다. SSMA는 데이터베이스 서버에 대 한 정보를 저장 하지만 암호를 저장 하지는 않습니다.  
  
데이터베이스에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 데이터베이스에 대 한 활성 연결을 원하는 경우 다시 연결 해야 합니다.  
  
MySQL 데이터베이스에 대 한 메타 데이터는 자동으로 업데이트 되지 않습니다. 대신 MySQL 메타 데이터 탐색기에서 메타 데이터를 업데이트 하려면 수동으로 업데이트 해야 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "MySQL 메타 데이터 새로 고침" 섹션을 참조 하십시오.  
  
## <a name="required-mysql-permissions"></a>필요한 MySQL 권한  
MySQL 데이터베이스에 연결 하는 데 사용 되는 계정에는 최소한 **연결** 권한이 있어야 합니다. 이렇게 하면 SSMA가 연결 하는 사용자가 소유한 스키마에서 메타 데이터를 가져올 수 있습니다. 다른 스키마의 개체에 대 한 메타 데이터를 가져온 다음 해당 스키마의 개체를 변환 하려면 계정에 다음 사용 권한이 있어야 합니다.  
  
-   데이터베이스 개체에 대 한 ' SHOW ' 권한  
  
-   ' Information_schema '에 대 한 ' SELECT ' 권한  
  
-   Mysql의 ' SELECT ' 권한 (Udf의 경우)  
  
## <a name="establishing-a-connection-to-mysql"></a>MySQL에 대 한 연결 설정  
데이터베이스에 연결 하는 경우 SSMA는 데이터베이스 메타 데이터를 읽은 다음이 메타 데이터를 프로젝트 파일에 추가 합니다. 이 메타 데이터는 개체를 SQL Server 또는 SQL Azure 구문으로 변환 하 고 데이터를 SQL Server 또는 SQL Azure로 마이그레이션할 때 SSMA에서 사용 됩니다. MySQL 메타 데이터 탐색기 창에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!IMPORTANT]  
> 연결을 시도 하기 전에 데이터베이스 서버가 실행 중이 고 연결을 허용할 수 있는지 확인 합니다.  
  
**MySQL에 연결하려면**  
  
1.  **파일** 메뉴에서 **MySQL에 연결** (이 옵션은 프로젝트를 만든 후에 사용 됨)을 선택 합니다.  
  
    이전에 MySQL에 연결 된 경우 명령 이름이 **mysql에 다시 연결**됩니다.  
  
2.  **공급자** 상자에서 MySQL ODBC 5.1 드라이버 (신뢰할 수 있음)를 선택 합니다. 표준 모드의 기본 공급자입니다.  
  
3.  **모드** 상자에서 **표준 모드**를 선택 합니다. 기본 모드입니다.  
  
    표준 모드를 사용 하 여 서버 이름 및 포트를 지정 합니다.  
  
4.  **표준 모드**에서 다음 값을 제공 합니다.  
  
    1.  **서버 이름** 상자에 MySQL 서버 이름을 입력 합니다. **서버 포트** 상자에 포트 번호를 3306로 입력 합니다. 기본 포트입니다.  
  
    2.  **사용자 이름** 상자에 필요한 권한이 있는 MySQL 계정을 입력 합니다.  
  
    3.  **암호** 상자에 지정 된 사용자 이름의 암호를 입력 합니다.  
  
5.  **SSL:** MySQL에 안전 하 게 연결 하려는 경우 **ssl** 확인란을 선택 하 여 Ssl (Secure Socket Layer)을 사용 합니다.  
  
6.  **구성:** SSL (Secure Socket Layer)을 통해 MySQL에 대 한 연결을 구성 하는 옵션을 제공 합니다.  
  
    > [!NOTE]  
    > **구성을**사용 하도록 설정 하려면 SSL을 **True**로 설정 해야 합니다.  
  
    "구성" 단추를 클릭 하면 대화 상자가 나타납니다. MySQL 데이터베이스에 연결 하는 동안 암호화를 사용 하려면 대화 상자에 있는 다음 세 가지 인증서 파일의 경로를 정의 해야 [Privacy Enhanced Mail 인증서 (PEM)].  
  
    -   **SSL 인증 기관:** 신뢰 SSL Ca 목록이 포함 된 파일의 경로를 지정 합니다.  
  
    -   **SSL 인증서:** 보안 연결을 설정 하는 데 사용할 SSL 인증서 파일의 이름을 지정 합니다.  
  
    -   **SSL 키:** 보안 연결을 설정 하는 데 사용할 SSL 키 파일의 이름을 지정 합니다.  
  
    > [!NOTE]  
    > -   필요한 정보가 제공 되 면 **확인** 단추를 사용할 수 있습니다. 파일 경로가 잘못 된 경우 "확인" 단추는 사용 하지 않도록 설정 된 상태로 유지 됩니다.  
    > -   **취소** 단추를 클릭 하면 대화 상자가 닫히고 주 연결 양식에서 SSL 옵션이 **해제** 됩니다.  
  
7.  자세한 내용은 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md) 을 참조 하세요.  
  
## <a name="reconnecting-to-mysql"></a>MySQL에 다시 연결  
데이터베이스 서버에 대 한 연결은 프로젝트를 닫을 때까지 활성 상태로 유지 됩니다. 프로젝트를 다시 열 때 데이터베이스에 대 한 활성 연결을 원하는 경우 다시 연결 해야 합니다. 메타 데이터를 업데이트 하 고, 데이터베이스 개체를 SQL Server 또는 SQL Azure에 로드 하 고, 데이터를 마이그레이션할 때까지 오프 라인으로 작업할 수 있습니다.  
  
## <a name="refreshing-mysql-metadata"></a>MySQL 메타 데이터 새로 고침  
MySQL 데이터베이스에 대 한 메타 데이터는 자동으로 새로 고쳐지지 않습니다. MySQL 메타 데이터 탐색기의 메타 데이터는 처음 연결 될 때 또는 메타 데이터를 마지막으로 새로 고친 시간에 메타 데이터에 대 한 스냅숏입니다. 모든 스키마, 단일 스키마 또는 개별 데이터베이스 개체에 대 한 메타 데이터를 수동으로 업데이트할 수 있습니다.  
  
**메타 데이터를 새로 고치려면**  
  
1.  데이터베이스에 연결 되어 있는지 확인 합니다.  
  
2.  MySQL 메타 데이터 탐색기에서 업데이트 하려는 각 스키마 또는 데이터베이스 개체 옆의 확인란을 선택 합니다.  
  
3.  **스키마**를 마우스 오른쪽 단추로 클릭 하거나 개별 스키마 또는 데이터베이스 개체를 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 새로 고침**을 선택 합니다.  
  
    활성 연결이 없는 경우 SSMA는 연결할 수 있도록 **MySQL에 연결** 대화 상자를 표시 합니다.  
  
4.  데이터베이스에서 새로 고침 대화 상자에서 새로 고칠 개체를 지정 합니다.  
  
    -   개체를 새로 고치려면 화살표가 나타날 때까지 개체 옆에 있는 **활성** 필드를 클릭 합니다.  
  
    -   개체를 새로 고치지 않으려면 **X** 가 나타날 때까지 개체 옆에 있는 **활성** 필드를 클릭 합니다.  
  
    -   개체의 범주를 새로 고치거 나 거부 하려면 category 폴더 옆의 **활성** 필드를 클릭 합니다.  
  
    -   색 구분의 정의를 보려면 **범례** 단추를 클릭 합니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SQL Server &#40;MySQLToSQL에 연결 하](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md) 는 것&#41;  
  
## <a name="see-also"></a>참고 항목  
[MySQL 데이터베이스를 SQL Server-Azure SQL Database &#40;MySQLToSql&#41;로 마이그레이션](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
