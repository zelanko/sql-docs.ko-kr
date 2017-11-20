---
title: "Linux SSMS로 SQL Server 관리 | Microsoft Docs"
description: "이 자습서에서는 Linux에서 실행 중인 Windows에서 SQL Server Management Studio를 사용 하 여 SQL Server에 연결 하는 방법을 보여 줍니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 30cc4564-f389-4707-9b25-8ba782cc5150
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: b4e70106782541d771a2539d025a0a6dd75c34d9
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---
# <a name="use-sql-server-management-studio-ssms-on-windows-to-manage-sql-server-on-linux"></a>Windows에서 SQL Server Management Studio (SSMS)를 사용 하 여 Linux에서 SQL Server 관리

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 사용 하는 방법을 보여 줍니다. [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) SQL Server 2017 Linux에서 연결할 수 있습니다. SSMS는 Windows 응용 프로그램, 따라서 Linux에서 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터는 경우 SSMS를 사용 합니다.

성공적으로 연결한 후 데이터베이스와의 통신을 확인 하려면 간단한 TRANSACT-SQL (T-SQL) 쿼리를 실행 합니다.

## <a name="install-the-newest-version-of-sql-server-management-studio"></a>SQL Server Management Studio의 최신 버전 설치

SQL Server를 사용할 때는 항상 최신 버전의 SQL Server Management Studio (SSMS)를 사용 해야 합니다. 최신 버전의 SSMS 지속적으로 업데이트 되 고 최적화 된와 현재 SQL Server on 2017 Linux 합니다. 참조를 다운로드 하 여 최신 버전을 설치 하려면 [SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)합니다. 최신 상태로 유지, 최신 버전의 SSMS 묻는 메시지를 다운로드 하는 새 버전이 있는 경우. 

## <a name="connect-to-sql-server-on-linux"></a>Linux에서 SQL Server에 연결

다음 단계에는 SQL Server 2017 linux SSMS로 연결 하는 방법을 보여 줍니다.

1. SSMS를 입력 하 여 시작 **Microsoft SQL Server Management Studio** Windows에서 검색 상자 및 데스크톱 응용 프로그램을 클릭 합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png)

2. 에 **서버에 연결** 창에서 다음 정보를 입력 (SSMS 이미 실행 중인 경우 클릭 **연결 > 데이터베이스 엔진** 열려는 **서버에 연결** 창):

   | 설정 | Description |
   |-----|-----|
   | **서버 유형** | 기본값은 데이터베이스 엔진입니다. 이 값을 변경 하지 마십시오. |
   | **서버 이름** | 대상 Linux SQL Server 컴퓨터 또는 IP 주소 이름을 입력 합니다. |
   | **인증** | Linux에서 SQL Server 2017 년에 대 한 사용 하 여 **SQL Server 인증**합니다. |
   | **로그인** | 서버에서 데이터베이스에 액세스할 수 있는 사용자의 이름을 입력 (예를 들어 기본 **SA** 설치 과정에서 생성 하는 계정). |
   | **암호** | 지정된 된 사용자에 대 한 암호를 입력 (에 **SA** 계정을 만든이 설치 하는 동안). |

    ![SQL Server Management Studio: SQL 데이터베이스 서버에 연결](./media/sql-server-linux-develop-use-ssms/connect.png)

3. **연결**을 클릭합니다.

    > [!TIP]
    > 연결 오류가 발생하는 경우 먼저 오류 메시지에서 문제를 진단합니다. 그런 다음 [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection)(연결 문제 해결 권장 사항)를 검토합니다.
 
5. SQL Sever 프로그램에 연결 하 **개체 탐색기** 을 열고 액세스할 수 있습니다 하 여 데이터베이스를 관리 작업을 수행 하거나 데이터를 쿼리 합니다.
 
     ![개체 탐색기](./media/sql-server-linux-develop-use-ssms/object-explorer.png)
     
## <a name="run-sample-queries"></a>예제 쿼리를 실행 합니다.

서버에 연결한 후 데이터베이스에 연결 하 고 예제 쿼리를 실행할 수 있습니다. 경우에 새 쿼리를 작성 하는 참조 [TRANSACT-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)합니다.

1. 에 대 한 쿼리를 실행 하기 위해 사용할 데이터베이스를 식별 합니다. 만든 새 데이터베이스 수는 [TRANSACT-SQL 자습서](../t-sql/tutorial-writing-transact-sql-statements.md)합니다. 일 수는 **AdventureWorks** 샘플 데이터베이스 [다운로드 하 고 복원](sql-server-linux-migrate-restore-database.md)합니다.
2. **개체 탐색기**, 서버에서 대상 데이터베이스로 이동 합니다.
2. 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **새 쿼리**:

    ![새 쿼리 합니다. SQL 데이터베이스 서버에 연결: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/new-query.png)

3. 쿼리 창에서 데이터 테이블 중 하나를 선택 하려면 TRANSACT-SQL 쿼리를 작성 합니다. 데이터를 선택 하는 다음 예제는 **Production.Product** 목차는 **AdventureWorks** 데이터베이스입니다.

        SELECT TOP 10 Name, ProductNumber
        FROM Production.Product
        ORDER BY Name ASC

4. 클릭는 **Execute** 단추:

    ![성공했습니다. SQL 데이터베이스 서버에 연결: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/execute-query.png)

## <a name="next-steps"></a>다음 단계

쿼리 외에 만들고 데이터베이스를 관리 하는 T-SQL 문을 사용할 수 있습니다.

T-SQL을 처음 접하는 경우 참조 [자습서: TRANSACT-SQL 문 쓰기](../t-sql/tutorial-writing-transact-sql-statements.md) 및 [TRANSACT-SQL 참조 (데이터베이스 엔진)](https://msdn.microsoft.com/library/bb510741.aspx)합니다.

SSMS를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [사용 하 여 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)합니다.

