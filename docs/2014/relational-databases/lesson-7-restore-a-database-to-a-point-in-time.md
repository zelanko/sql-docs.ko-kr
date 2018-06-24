---
title: '8단원: Windows Azure 저장소에 데이터베이스를 복원 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ea9ec20e60fb879b17434e8fe4581d28b3d7a551
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080407"
---
# <a name="lesson-8-restore-a-database-to-windows-azure-storage"></a>8단원: Microsoft Azure Storage에 데이터베이스 복원
  이 단원에서는 로컬로 백업 파일을 만들고 Microsoft Azure Storage에 복원하는 방법을 배웁니다. 온-프레미스나 Windows Azure의 가상 컴퓨터에 데이터베이스가 있을 수 있습니다. 이 단원을 수행하기 위해 4, 5, 6, 7단원을 완료할 필요는 없습니다.  
  
 이 단원에서는 다음 단계를 이미 완료했다고 가정합니다.  
  
-   Windows Azure 저장소 계정이 있습니다.  
  
-   Windows Azure 저장소 계정에서 컨테이너를 만들었습니다.  
  
-   읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들었습니다. SAS 키도 생성했습니다.  
  
-   원본 컴퓨터에서 공유 액세스 서명 기반의 SQL Server 자격 증명을 만들었습니다.  
  
-   원본 컴퓨터에서 데이터베이스를 만들었습니다.  
  
 Microsoft Azure Storage에 데이터베이스를 복원하려면 다음 단계를 수행합니다.  
  
1.  원본 컴퓨터에서 SQL Server Management Studio를 시작합니다.  
  
2.  새로 만든 데이터베이스에 연결된 경우 쿼리 창을 열고 다음 문을 실행합니다.  
  
    ```tsql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  다음 문을 복사하여 쿼리 창에서 실행합니다.  
  
    ```tsql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     이 단계가 끝나면 컨테이너에 관리 포털의 데이터 파일(.mdf 및 .ldf)이 나열됩니다.  
  
 SQL Server Management Studio 사용자 인터페이스를 사용하여 Microsoft Azure Storage를 가리키는 데이터 및 로그 파일이 포함된 데이터베이스를 복원하려면 다음 단계를 수행합니다.  
  
1.  **개체 탐색기**, 서버 트리를 확장할 서버 이름을 클릭 합니다.  
  
2.  확장 **데이터베이스**, 및 해당 데이터베이스를 선택 합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **복원**을 클릭합니다.  
  
4.  에 **일반** 페이지는 **복원** 원본 섹션을 클릭 **소스** 장치입니다.  
  
5.  에 대 한 찾아보기 단추를 클릭는 **소스** 열 수 있는 장치 텍스트 상자는 **백업 장치 선택** 대화 상자.  
  
6.  백업 미디어 입력란에서 선택 **파일**를 클릭 하 고는 **추가** 단추 백업 (.bak) 파일을 찾습니다. **확인**을 클릭합니다.  
  
7.  클릭 **파일** 첫 페이지에 있습니다.  
  
8.  에 **데이터베이스 파일 복원** 섹션의 **으로 복원** 필드에 다음과 같이 입력 합니다.  
  
     데이터 파일에 대 한 입력: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`합니다. 로그 파일에 대 한 입력: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`합니다.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. **확인**을 클릭합니다.  
  
 복원이 완료되면 관리 포털에 로그인합니다. 다음과 같이 컨테이너에서 .mdf 및 .ldf 파일을 볼 수 있습니다.  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **다음 단원:**  
  
 [9단원. Microsoft Azure Storage에서 데이터베이스 복원](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  