---
title: '6단원: 원본에서 데이터베이스를 마이그레이션할 온-프레미스를 대상 컴퓨터에 Windows Azure 기계 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a5787a3f5aecd746ac9aafd5850e6109ebcd999
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090689"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-windows-azure"></a>6단원: 온-프레미스의 원본 컴퓨터에서 Windows Azure의 대상 컴퓨터로 데이터베이스 마이그레이션
  이 단원에서는 이미 다른 SQL Server가 있다고 가정합니다. 이 SQL Server는 다른 온-프레미스 컴퓨터나 Microsoft Azure의 가상 머신에 있을 수 있습니다. Microsoft Azure에서 SQL Server 가상 머신을 만드는 방법은 [Microsoft Azure에서 SQL Server 가상 머신 프로비전](http://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/)을 참조하세요. Microsoft Azure에서 SQL Server 가상 머신을 프로비전한 후 다른 컴퓨터에서 SQL Server Management Studio를 통해 이 가상 머신의 SQL Server 인스턴스에 연결할 수 있는지 확인합니다.  
  
 이 단원에서는 다음 단계를 이미 완료했다고 가정합니다.  
  
-   Microsoft Azure Storage 계정이 있습니다.  
  
-   Microsoft Azure Storage 계정에서 컨테이너를 만들었습니다.  
  
-   읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들었습니다. SAS 키도 생성했습니다.  
  
-   원본 컴퓨터에서 SQL Server 자격 증명을 만들었습니다.  
  
-   Microsoft Azure에서 대상 SQL Server 가상 머신을 이미 만들었습니다. SQL Server 2014를 포함하는 플랫폼 이미지를 선택하여 만드는 것이 좋습니다.  
  
 데이터베이스를 SQL Server 온-프레미스에서 Microsoft Azure의 다른 가상 머신으로 마이그레이션하려면 다음 단계를 수행합니다.  
  
1.  원본 컴퓨터(이 자습서의 경우 온-프레미스 컴퓨터)의 SQL Server Management Studio에서 쿼리 창을 엽니다. 다음 문을 실행하여 데이터베이스를 분리하고 다른 컴퓨터로 이동합니다.  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  대상 컴퓨터로 데이터베이스를 전송해야 하는 경우 먼저 대상 컴퓨터를 준비해야 합니다. 대상 컴퓨터를 준비하려면 먼저 대상 컴퓨터에서 SQL Server 자격 증명을 만들어야 합니다. 암호화된 데이터베이스인 경우 원본 컴퓨터에서 대상 컴퓨터로 인증서도 가져와야 합니다.  
  
    1.  대상 컴퓨터에서 SQL Server 자격 증명을 만들려면 다음 단계를 수행합니다.  
  
        1.  원본 컴퓨터에서 SQL Server Management Studio를 통해 대상 컴퓨터에 연결합니다.  또는 대상 컴퓨터에서 SQL Server Management Studio를 직접 시작합니다.  
  
        2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
        3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 필요한 대로 수정합니다. 다음 문은 저장소 컨테이너의 공유 액세스 인증서를 저장할 SQL Server 자격 증명을 만듭니다.  
  
            ```sql  
  
            USE master   
            GO   
            CREATE CREDENTIAL [http://teststorageaccnt.blob.core.windows.net/testcontainer]   
            WITH IDENTITY='SHARED ACCESS SIGNATURE',   
            SECRET = 'your SAS key'   
            GO  
  
            ```  
  
        4.  사용할 수 있는 모든 자격 증명을 보려면 쿼리 창에서 다음 문을 실행합니다.  
  
            ```sql  
            SELECT * from sys.credentials   
            ```  
  
        5.  대상 서버에 연결되었으면 쿼리 창을 열고 다음을 실행합니다.  
  
            ```sql  
  
            -- Create a master key and a server certificate   
            USE master   
            GO   
            CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01'; -- You may use a different password.   
            GO   
            CREATE CERTIFICATE MySQLCert   
            FROM FILE = 'C:\certs\MySQLCert.CER'   
            WITH PRIVATE KEY   
            (   
            FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
            DECRYPTION BY PASSWORD = 'MySQLKey01'   
            );   
            GO  
  
            ```  
  
             이 단계의 끝에서 대상 컴퓨터는 원본 컴퓨터에서 백업된 암호화 인증서를 가져왔습니다. 다음 작업으로, 대상 컴퓨터에서 데이터 파일을 연결할 수 있습니다.  
  
    2.  FOR ATTACH 옵션을 사용하여 Microsoft Azure Storage의 기존 파일을 가리키는 데이터 및 로그 파일이 포함된 데이터베이스를 만듭니다. 쿼리 창에서 다음 문을 실행합니다.  
  
        ```sql  
  
        --Create a database on the destination server   
        CREATE DATABASE TestDB1onDest   
        ON   
        (NAME = TestDB1_data,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf' )   
        LOG ON   
         (NAME = TestDB1_log,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
        FOR ATTACH   
        GO  
  
        ```  
  
    3.  개체 탐색기에서 데이터베이스를 클릭하고 새로 고침을 마우스 오른쪽 단추로 클릭합니다. 새로 만든 데이터베이스인 TestDB1onDest가 표시된 것을 확인할 수 있습니다.  
  
    4.  쿼리 창에서 다음 문을 실행합니다.  
  
        ```sql  
  
        USE TestDB1onDest   
        SELECT * FROM Table1;   
        GO  
  
        ```  
  
         4단원에서 입력한 데이터가 모두 나열됩니다.  
  
 암호화된 데이터베이스가 데이터 이동 없이 다른 컴퓨팅 인스턴스로 전송되었습니다.  
  
 SQL Server Management Studio 사용자 인터페이스를 사용하여 Microsoft Azure Storage의 기존 파일을 가리키는 데이터 및 로그 파일이 포함된 데이터베이스를 만들려면 다음 단계를 수행합니다.  
  
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 클릭합니다. TestDB1을 마우스 오른쪽 단추로 클릭합니다. 태스크를 클릭한 다음 분리를 클릭합니다. 분리 대화 상자에서 연결 삭제를 선택합니다. **확인**을 클릭합니다.  
  
3.  SQL Server 2014 CTP2 이상이 설치된 대상 컴퓨터에 연결합니다. 대상 컴퓨터를 준비하려면 TestDB1을 배치한 동일한 컨테이너를 가리키도록 대상 컴퓨터에서 SQL Server 자격 증명을 만들어야 합니다. 동일한 컴퓨터에서 다시 연결할 경우 다른 자격 증명을 만들 필요가 없습니다.  
  
4.  **개체 탐색기**에서 **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **연결**을 클릭합니다.  
  
5.  **데이터베이스 연결** 대화 상자에서 연결할 데이터베이스를 지정하려면 **추가**를 클릭합니다. **데이터베이스 파일 찾기** 대화 상자에서 다음을 수행합니다.  
  
     데이터베이스 데이터 파일 위치에 대 한 입력: `https://teststorageaccnt.blob.core.windows.net/testcontainer/`합니다.  
  
     파일 이름 입력: `TestDB1Data.mdf`합니다.  
  
6.  **확인**을 클릭합니다.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **다음 단원:**  
  
 [7단원: Windows Azure Storage로 데이터 파일 이동](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
  
