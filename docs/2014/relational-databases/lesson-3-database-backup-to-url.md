---
title: '4단원: Windows Azure Storage에서 데이터베이스 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7361cb5d0e68cfa3f45f46d7f99d68c88c1a556b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090815"
---
# <a name="lesson-4-create-a-database-in-windows-azure-storage"></a>4단원: Microsoft Azure Storage에서 데이터베이스 만들기
  이 섹션에서는 Windows Azure의 SQL Server 데이터 파일 기능을 사용하여 데이터베이스를 만드는 방법을 배웁니다. 이 단원 전에 1, 2, 3단원을 완료해야 합니다. 3단원은 4단원 전에 Windows Azure 스토리지 컨테이너에 대한 정보와 관련 정책 이름 및 SAS 키를 SQL Server 자격 증명 저장소에 저장해야 하기 때문에 매우 중요한 단계입니다.  
  
 데이터 또는 로그 파일에서 사용하는 각 스토리지 컨테이너에 대해 컨테이너 경로와 일치하는 이름의 SQL Server 자격 증명을 만들어야 합니다. 이렇게 하면 Windows Azure 스토리지에서 새 데이터베이스를 만들 수 있습니다.  
  
 이 단원에서는 다음 단계를 이미 완료했다고 가정합니다.  
  
-   Microsoft Azure Storage 계정이 있습니다.  
  
-   Microsoft Azure Storage 계정에서 컨테이너를 만들었습니다.  
  
-   읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들었습니다. SAS 키도 생성했습니다.  
  
-   원본 컴퓨터에서 SQL Server 자격 증명을 만들었습니다.  
  
 향상된 Windows Azure 스토리지의 SQL Server 데이터 파일 기능을 사용하여 Windows Azure에서 데이터베이스를 만들려면 다음 단계를 수행합니다.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  개체 탐색기에서 설치된 데이터베이스 엔진의 인스턴스에 연결합니다.  
  
3.  표준 도구 모음에서 새 쿼리를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 창에 붙여 넣고 필요한 대로 수정합니다. FILENAME 필드는 스토리지 컨테이너에 있는 데이터베이스 파일의 URI 경로를 가리키며 https로 시작해야 합니다.  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     데이터베이스에 일부 데이터를 추가합니다.  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  온-프레미스 SQL Server에서 새로운 TestDB1을 보려면 개체 탐색기에서 데이터베이스를 새로 고칩니다.  
  
6.  이와 마찬가지로 스토리지 계정에서 새로 만든 데이터베이스를 보려면 SSMS(SQL Server Management Studio)를 통해 스토리지 계정에 연결합니다. SQL Server Management Studio를 사용하여 Windows Azure 스토리지에 연결하는 방법을 알아보려면 다음 단계를 수행하십시오.  
  
    1.  먼저 스토리지 계정 정보를 가져옵니다. 관리 포털에 로그인한 다음 **저장소** 를 클릭하고 저장소 계정을 선택합니다. 스토리지 계정이 선택되면 페이지 아래쪽에서 **액세스 키 관리** 를 클릭합니다. 다음과 유사한 대화 상자가 열립니다.  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  **저장소 계정 이름** 및 **기본 액세스 키** 값을 SSMS의 **Windows Azure 저장소에 연결** 대화 상자에 복사한 다음 **연결**을 클릭합니다. 다음 스크린 샷에서와 같이 스토리지 계정 컨테이너에 대한 정보가 SSMS에 나타납니다.  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 다음 스크린 샷에서는 온-프레미스 및 Windows Azure 스토리지 환경 모두에서 새로 만든 데이터베이스를 보여 줍니다.  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **참고:** 컨테이너의 데이터 파일에 대 한 활성 참조가 없으면 연결 된 SQL Server 자격 증명을 삭제 하려는 모든 시도가 실패 합니다. 이와 마찬가지로 BLOB의 특정 데이터베이스 파일에 대한 임대가 이미 있는 경우 SQL Server 자격 증명을 삭제하려면 먼저 BLOB에서 임대를 해제해야 합니다. 임대를 중단하려면 [Blob 임대](https://msdn.microsoft.com/library/azure/ee691972.aspx)를 사용할 수 있습니다.  
  
 이 새로운 기능을 사용하면 CREATE DATABASE 문이 기본적으로 클라우드 사용 데이터베이스로 설정되도록 SQL Server를 구성할 수 있습니다. 즉, SQL Server Management Studio 서버 인스턴스 속성에서 기본 데이터 및 로그 위치를 설정하여 데이터베이스를 만들 때마다 모든 데이터베이스 파일(.mdf, .ldf)이 Windows Azure 스토리지에서 페이지 BLOB으로 만들어지도록 할 수 있습니다.  
  
 SQL Server Management Studio 사용자 인터페이스를 사용하여 Windows Azure 스토리지에서 데이터베이스를 만들려면 다음 단계를 수행합니다.  
  
1.  개체 탐색기에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 새 데이터베이스를 클릭합니다.  
  
3.  새 데이터베이스 대화 상자에서 데이터베이스 이름을 입력합니다.  
  
4.  주 데이터 및 트랜잭션 로그 파일의 기본값을 변경하려면 데이터베이스 파일 표에서 해당 셀을 클릭한 다음 새 값을 입력합니다. 또한 파일의 경로를 지정합니다. Path의 경우 스토리지 컨테이너의 URL 경로를 입력합니다(예: `https://teststorageaccnt.blob.core.windows.net/testcontainer/`). FileName의 경우 데이터베이스 파일(.mdf, .ldf)의 물리적 파일 이름을 입력합니다.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     자세한 내용은 [데이터베이스에 데이터 또는 로그 파일 추가](databases/add-data-or-log-files-to-a-database.md)을 참조하세요.  
  
5.  다른 모든 기본값을 유지합니다.  
  
6.  확인을 클릭합니다.  
  
 온-프레미스 SQL Server에서 새로운 TestDB1을 보려면 개체 탐색기에서 데이터베이스를 새로 고칩니다. 이 단원의 앞에서 설명한 대로 스토리지 계정에서 새로 만든 데이터베이스를 보려면 SSMS(SQL Server Management Studio)를 통해 스토리지 계정에 연결합니다.  
  
 **다음 단원:**  
  
 [5 단원입니다. &#40;옵션&#41; TDE를 사용 하 여 데이터베이스를 암호화 합니다.](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
