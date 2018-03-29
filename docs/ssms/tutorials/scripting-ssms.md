---
Title: 'Tutorial: Script Objects in SQL Server Management Studio'
description: SSMS에서 개체 스크립팅에 대한 자습서입니다.
keywords: SQL Server, SSMS, SQL Server Management Studio, 스크립트, 스크립팅
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: bc20cc573c6b0890e5b16f4876636534f9fbb916
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>자습서: SQL Server Management Studio에서 개체 스크립팅
이 자습서에서는 SQL Server Management Studio 내에서 발견되는 다양한 개체에 대한 T-SQL(Transact-SQL) 스크립트를 생성하는 방법을 설명합니다.  이 자습서에서는 다음 개체를 스크립팅하는 방법의 예제를 찾을 수 있습니다. 

> [!div class="checklist"]
> * GUI 내에서 작업을 수행할 때 쿼리
> * 두 가지 방법의 데이터베이스("스크립팅" 및 "스크립트 생성")
> * 테이블
> * 저장 프로시저
> * 확장 이벤트

이 자습서의 요약은 **개체 탐색기**의 모든 개체를 마우스 오른쪽 단추로 클릭하고 **개체 스크립팅** 옵션을 선택하여 스크립팅할 수 있다는 것입니다. 


## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio, SQL Server에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하기 위한 지침은 여기: [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)에서 찾을 수 있습니다. 


## <a name="script-queries-from-gui"></a>GUI에서 쿼리 스크립팅
언제든지 SSMS에서 GUI를 사용하여 작업을 수행할 때 해당 작업과 관련된 T-SQL 코드를 생성할 수도 있습니다. 다음 예제는 데이터베이스의 백업을 수행하고 트랜잭션 로그를 축소하는 경우 수행하는 방법을 보여줍니다.  이러한 동일한 단계를 GUI를 통해 완료한 모든 작업에도 적용할 수 있습니다. 

### <a name="script-t-sql-when-backing-up-a-database"></a>데이터베이스를 백업할 때 T-SQL 스크립팅
1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. 데이터베이스 > **작업** > **백업**을 마우스 오른쪽 단추로 클릭합니다.

    ![데이터베이스 백업](media/scripting-ssms/backupdb.png)

4. 원하는 대로 백업을 구성합니다. 이 자습서의 목적을 위해 모든 항목은 기본값으로 남겨져 있습니다. 그러나 창에서 변경된 내용은 스크립트에도 반영됩니다. 
5. **스크립트** > **쿼리 창 동작 스크립팅**에 대한 옵션을 클릭합니다.
 
    ![DB 백업 스크립팅](media/scripting-ssms/scriptdbbackup.PNG)
6. 쿼리 창에 채워진 T-SQL을 검토합니다. 

    ![DB 백업에 대한 스크립트](media/scripting-ssms/dbbackupscript.PNG)


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>트랜잭션 로그를 축소하는 경우 T-SQL 스크립팅
1. 데이터베이스 > **작업** > **축소** > **파일**을 마우스 오른쪽 단추로 클릭합니다.

     ![파일 축소](media/scripting-ssms/shrinkfiles.png)

2. **파일 형식** 드롭다운에서 **로그**를 선택합니다.

    ![트랜잭션 로그 축소](media/scripting-ssms/shrinktlog.png)

3. 옵션 **스크립트** 및 **클립보드 동작 스크립팅**을 클릭합니다.

    ![클립보드로 스크립팅](media/scripting-ssms/scriptactiontoclipboard.png)

4. **새 쿼리** 창을 열고 붙여넣습니다(창에서 마우스 오른쪽 단추로 **붙여넣기** 클릭).

    ![스크립트 붙여넣기](media/scripting-ssms/paste.png)


## <a name="script-databases"></a>데이터베이스 스크립팅
다음 섹션에서는 **스크립팅** 옵션 및 **스크립트 생성** 옵션을 사용하여 데이터베이스를 스크립팅하는 방법을 설명합니다.  **스크립팅** 옵션은 데이터베이스 및 해당 항목에 대한 구성 옵션을 다시 만듭니다. **스크립트 생성** 옵션은 데이터가 아닌 데이터베이스의 모든 개체를 스크립팅합니다. 데이터도 스크립팅하려면 [가져오기 및 내보내기 마법사](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/start-the-sql-server-import-and-export-wizard)를 사용해야 합니다.  


### <a name="script-database-using-script-option"></a>스크립트 옵션을 사용하여 데이터베이스 스크립팅
1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. 마우스 오른쪽 단추로 데이터베이스 > **데이터베이스 스크립팅**을 클릭합니다.

    ![DB 스크립팅](media/scripting-ssms/scriptdb.png)

4. 창에서 데이터베이스 생성 쿼리를 검토합니다. 

    ![DB 스크립팅됨](media/scripting-ssms/scriptedoutdb.png)
    - 이 옵션은 데이터베이스 구성 옵션만을 스크립팅합니다.  

### <a name="script-database-using-generate-scripts-option"></a>스크립트 생성 옵션을 사용하여 데이터베이스 스크립팅
1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. 데이터베이스 > **작업** > **스크립트 생성**을 마우스 오른쪽 단추로 클릭합니다.

    ![DB에 대한 스크립트 생성](media/scripting-ssms/generatescriptsfordb.png)

4. **다음**을 선택하면 전체 데이터베이스 또는 데이터베이스 내의 특정 개체를 스크립팅할 수 있는 것을 확인할 수 있습니다. 
 
    ![개체에 대한 스크립트 생성](media/scripting-ssms/scriptobjects.png)
 
5. **다음**을 선택합니다. 이 화면에서 스크립트가 저장되는 위치를 구성할 수 있습니다. 
    - **고급**을 선택하여 고급 옵션을 구성할 수도 있습니다.

    ![고급 스크립트 옵션](media/scripting-ssms/advancedscripts.png)

6. 진행할 준비가 되면 스크립트가 생성되고 **마침**에 도달할 때까지 **다음**을 누릅니다. 데이터베이스 스크립트는 5단계에서 저장된 위치에 위치하게 됩니다. 
    - 이는 데이터가 아닌 데이터베이스 내의 스키마 및 다양한 개체를 스크립팅합니다. 
 
## <a name="script-tables"></a>테이블 스크립팅
이 섹션에서는 데이터베이스에서 테이블을 스크립팅하는 방법을 다룹니다.

1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **AdventureWorks** 데이터베이스 노드를 확장합니다. 
4. **테이블** 노드를 확장합니다.
5. 스크립팅하려는 테이블 > **테이블 스크립팅**을 마우스 오른쪽 단추로 클릭합니다.
    - 여기에는 테이블 만들기 또는 데이터 삽입 등과 같은 다양한 옵션이 있습니다. 
    
    ![테이블 스크립팅](media/scripting-ssms/scripttable.png)
 
## <a name="script-stored-procedures"></a>저장 프로시저 스크립팅
이 섹션에서는 저장 프로시저를 스크립팅하는 방법을 다룹니다. 

1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **프로그래밍 기능** 노드를 확장합니다. 
4. **저장 프로시저** 노드를 확장합니다.
5. 원하는 저장 프로시저 > **저장 프로시저 스크립팅**을 마우스 오른쪽 단추로 클릭합니다.
    
    ![저장 프로시저 스크립팅](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>확장 이벤트 스크립팅
이 섹션에서는 [확장 이벤트](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events)를 스크립팅하는 방법을 다룹니다. 

1. SQL Server에 연결합니다.
2. **관리** 노드를 확장합니다.
3. **확장 이벤트** 노드를 확장합니다.
4. **세션** 노드를 확장합니다.
5. 원하는 확장 세션 > **세션 스크립팅**을 마우스 오른쪽 단추로 클릭합니다.

    ![xEvents 스크립팅](media/scripting-ssms/scriptxevents.png) 

## <a name="next-steps"></a>다음 단계
다음 문서에서는 SSMS 내에 있는 미리 빌드된 템플릿을 소개합니다. 

자세히 알아보려면 다음 문서로 진행합니다.
> [!div class="nextstepaction"]
> [다음 단계 단추](templates-ssms.md)


