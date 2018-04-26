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
ms.openlocfilehash: a931ddb3cf3229970de4b301e18002484acbaf53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
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
- [AdventureWorks2016 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 다운로드합니다. SSMS에서 데이터베이스를 복원하기 위한 지침은 여기: [데이터베이스 복원](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)에서 찾을 수 있습니다. 


## <a name="script-queries-from-gui"></a>GUI에서 쿼리 스크립팅
언제든지 SSMS에서 GUI를 사용하여 작업을 수행할 때 해당 작업과 관련된 T-SQL 코드를 생성할 수도 있습니다. 다음 예제는 데이터베이스의 백업을 수행하고 트랜잭션 로그를 축소하는 경우 수행하는 방법을 보여줍니다.  이러한 동일한 단계를 GUI를 통해 완료한 모든 작업에도 적용할 수 있습니다. 

### <a name="script-t-sql-when-backing-up-a-database"></a>데이터베이스를 백업할 때 T-SQL 스크립팅
1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. 마우스 오른쪽 단추로 **Adventureworks2016** 데이터베이스 > **작업** > **백업**을 클릭합니다.

    ![데이터베이스 백업](media/scripting-ssms/backupdb.png)

4. 원하는 대로 백업을 구성합니다. 이 자습서에서는 모든 항목은 기본값으로 남겨져 있습니다. 그러나 창에서 변경된 내용은 스크립트에도 반영됩니다. 
5. **스크립트** > **쿼리 동작 스크립팅 창**에 대한 옵션을 선택합니다.
 
    ![DB 백업 스크립팅](media/scripting-ssms/scriptdbbackup.PNG)
6. 쿼리 창에 채워진 T-SQL을 검토합니다. 

    ![DB 백업에 대한 스크립트](media/scripting-ssms/dbbackupscript.PNG)
7. **실행**을 선택하여 T-SQL을 통해 데이터베이스를 백업하는 쿼리를 실행합니다. 


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>트랜잭션 로그를 축소하는 경우 T-SQL 스크립팅
1. **AdventureWorks2016** 데이터베이스 > **작업** > **축소** > **파일**을 마우스 오른쪽 단추로 클릭합니다.

     ![파일 축소](media/scripting-ssms/shrinkfiles.png)

2. **파일 형식** 드롭다운에서 **로그**를 선택합니다.

    ![트랜잭션 로그 축소](media/scripting-ssms/shrinktlog.png)

3. **스크립트** 및 **클립보드 동작 스크립팅** 옵션을 선택합니다.

    ![클립보드로 스크립팅](media/scripting-ssms/scriptactiontoclipboard.png)

4. **새 쿼리** 창을 열고 붙여넣습니다(창에서 마우스 오른쪽 단추로 **붙여넣기** 클릭).

    ![스크립트 붙여넣기](media/scripting-ssms/paste.png)
5. **실행**을 선택하여 쿼리를 실행하고 트랜잭션 로그를 축소합니다. 


## <a name="script-databases"></a>데이터베이스 스크립팅
다음 섹션에서는 **스크립팅** 옵션 및 **스크립트 생성** 옵션을 사용하여 데이터베이스를 스크립팅하는 방법을 설명합니다.  **스크립팅** 옵션은 데이터베이스 및 해당 항목에 대한 구성 옵션을 다시 만듭니다. **스크립트 생성** 옵션을 사용하면 스키마와 데이터 모두를 스크립팅할 수 있습니다. 이 섹션에서는 **스크립팅** 옵션을 사용하여 두 새 데이터베이스 *AdventureWorks2016a*를 만듭니다.  *AdventureWorks2016b*는 **스크립트 생성** 옵션으로 만들어집니다. 


### <a name="script-database-using-script-option"></a>스크립트 옵션을 사용하여 데이터베이스 스크립팅
1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **AdventureWorks2016** 데이터베이스를 마우스 오른쪽 단추로 클릭하여 **데이터베이스 스크립팅** > **만들기** > **새 쿼리 창**을 선택합니다.

    ![DB 스크립팅](media/scripting-ssms/scriptdb.png)

4. 창에서 데이터베이스 생성 쿼리를 검토합니다. 

    ![DB 스크립팅됨](media/scripting-ssms/scriptedoutdb.png)
    - 이 옵션은 데이터베이스 구성 옵션만을 스크립팅합니다.
5. 키보드에서 **Ctrl + F**를 선택하여 **찾기** 대화 상자를 열고 아래쪽 화살표를 선택하여 **바꾸기** 옵션을 엽니다. 위쪽의 **찾기** 줄에 *AdventureWorks2016*을 입력하고 아래쪽 **바꾸기** 줄에  *AdventureWorks2016a*를 입력합니다. 
6. **모두 바꾸기**를 선택하여 *AdventureWorks2016* 인스턴스를 *AdventureWorks2016a*로 바꿉니다. 

    ![찾기 및 바꾸기](media/scripting-ssms/findandreplace.png)

1. **실행**을 선택하여 쿼리를 실행하고 새 *AdventureWorks2016a* 데이터베이스를 만듭니다. 

### <a name="script-database-using-generate-scripts-option"></a>스크립트 생성 옵션을 사용하여 데이터베이스 스크립팅
1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **AdventureWorks2016** 데이터베이스 > **작업** > **스크립트 생성**을 마우스 오른쪽 단추로 클릭합니다.

    ![DB에 대한 스크립트 생성](media/scripting-ssms/generatescriptsfordb.png)

4. **소개** 페이지가 열리며 **다음**을 선택하여 **개체 선택** 페이지를 엽니다. 전체 데이터베이스나, 데이터베이스의 특정 개체를 선택하는 옵션이 있습니다. **전체 데이터베이스 및 모든 데이터베이스 개체 스크립팅** 옵션을 선택합니다. 
 
    ![개체에 대한 스크립트 생성](media/scripting-ssms/scriptobjects.png)
 
5. **다음**을 선택하여 **스크립팅 옵션 설정** 페이지를 엽니다. 여기서는 스크립트 저장 위치와 몇 가지 추가적인 고급 옵션을 구성할 수 있습니다. 

    1. **새 쿼리 창에 저장** 옵션을 선택합니다. 

    2. **고급**을 선택하여 다음 옵션의 설정을 확인합니다. 

      - **통계 스크립팅**은 *통계 스크립팅*으로 설정
      - **스크립팅할 데이터 형식**은 *스키마 전용*으로 설정
      - **인덱스 스크립팅**은 *true*로 설정

   ![스크립트 개체](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > **스크립팅할 데이터 형식** 옵션에 *스키마 및 데이터*를 선택하면 데이터베이스에 대한 데이터를 스크립팅할 수 있습니다. 그러나 SSMS이 할당할 수 있는 것보다 많은 메모리를 차지할 수 있으므로 대형 데이터베이스에는 적합하지 않습니다. 그러나 소형 데이터베이스의 데이터를 더 큰 규모의 데이터베이스로 이동하려는 경우 유용하며 [가져오기 및 내보내기 마법사](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)를 사용해야 합니다.



1. **확인**선택하고 **다음**을 선택합니다. 
2. **요약**에서 **다음**을 선택한 후 다시 **다음**을 선택하여 스크립트를 생성하기 위한 **새 쿼리** 창을 엽니다.  
3. 키보드에서 **Ctrl + F**를 선택하여 **찾기** 대화 상자를 열고 아래쪽 화살표를 선택하여 **바꾸기** 옵션을 엽니다. 위쪽의 **찾기** 줄에 *AdventureWorks2016*을 입력하고 아래쪽 **바꾸기** 줄에 *AdventureWorks2016b*를 입력합니다. 
    1. **모두 바꾸기**를 선택하여 *AdventureWorks2016* 인스턴스를 *AdventureWorks2016b*로 바꿉니다. 

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)
7. **실행**을 선택하여 쿼리를 실행하고 새 *AdventureWorks2016b* 데이터베이스를 만듭니다. 
 
## <a name="script-tables"></a>테이블 스크립팅
이 섹션에서는 데이터베이스에서 테이블을 스크립팅하는 방법을 다룹니다. 이 옵션을 사용하여 테이블을 만들거나, 테이블을 삭제하고 만들 수 있습니다. 또한 이 옵션으로 테이블 수정(예: 삽입, 업데이트)과 관련한 T-SQL 스크립트를 작성할 수 있습니다. 이 섹션에서는 테이블을 삭제한 다음에 다시 만듭니다. 

1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **AdventureWorks** 데이터베이스 노드를 확장합니다. 
4. **테이블** 노드를 확장합니다.
5. 마우스 오른쪽 단추로 **dbo.ErrorLog** >  **테이블 스크립팅** > **삭제 및 만들기** > **새 쿼리 편집기 창**을 선택합니다.
    
    ![테이블 스크립팅](media/scripting-ssms/scripttable.png)

6. **실행**을 선택하여 쿼리를 실행합니다. 그러면 *Errorlog* 테이블을 삭제하고 다시 만들게 됩니다. 

    >[!NOTE]
    > AdventureWorks2016에서 *Errorlog* 테이블은 기본적으로 비어 있으므로 테이블을 삭제해도 사라지는 데이터는 없습니다. 그러나 데이터가 있는 테이블에 이 단계를 수행하면 데이터 손실이 발생합니다. 
 
## <a name="script-stored-procedures"></a>저장 프로시저 스크립팅
이 섹션에서는 저장 프로시저를 삭제하고 만드는 방법을 알아봅니다.  

1. SQL Server에 연결합니다.
2. **데이터베이스** 노드를 확장합니다.
3. **프로그래밍 기능** 노드를 확장합니다. 
4. **저장 프로시저** 노드를 확장합니다.
5. 저장 프로시저를 마우스 오른쪽 단추로 클릭하고 **dbo.uspGetBillOfMaterials**> **저장 프로시저 스크립팅** > **삭제 및 만들기** > **새 쿼리 창**을 선택합니다.
    
    ![저장 프로시저 스크립팅](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>확장 이벤트 스크립팅
이 섹션에서는 [확장 이벤트](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events)를 스크립팅하는 방법을 다룹니다. 

1. SQL Server에 연결합니다.
2. **관리** 노드를 확장합니다.
3. **확장 이벤트** 노드를 확장합니다.
4. **세션** 노드를 확장합니다.
5. 원하는 확장 세션을 마우스 오른쪽 단추로 클릭하고 **세션 스크립팅** > **새 쿼리 편집기 창**을 선택합니다.

    ![xEvents 스크립팅](media/scripting-ssms/scriptxevents.png) 
6. **새 쿼리 창**에서 세션의 새 이름을 *system_health*에서 *system_health2*로 변경하고 **실행**을 클릭하여 쿼리를 실행합니다. 

    1. **개체 탐색기**에서 **세션**을 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택하여 새 확장 이벤트 세션을 표시합니다. 세션 옆에 녹색 아이콘은 세션이 실행 중임을, 빨간색 아이콘은 세션이 중지되었음을 나타냅니다. 

    ![새 xEvent](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > 마우스 오른쪽 단추를 클릭하고 **시작**을 선택하여 세션을 시작할 수 있습니다. 그러나 이미 실행 중인 *system_health* 세션의 사본이기 때문에 이 단계를 건너뛸 수 있습니다. 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택하여 확장된 이벤트 세션의 사본을 삭제할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
다음 문서에서는 SSMS 내에 있는 미리 빌드된 T-SQL 템플릿을 소개합니다. 

자세히 알아보려면 다음 문서로 진행합니다.
> [!div class="nextstepaction"]
> [다음 단계](templates-ssms.md)


