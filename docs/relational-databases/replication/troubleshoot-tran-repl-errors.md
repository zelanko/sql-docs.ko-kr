---
title: '문제 해결사: SQL Server 트랜잭션 복제를 사용하여 오류 찾기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e25498f1d9d3b1ec3c24b7c2f34031fab9e4341f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057528"
---
# <a name="troubleshooter-find-errors-with-sql-server-transactional-replication"></a>문제 해결사: SQL Server 트랜잭션 복제를 사용하여 오류 찾기 
복제 오류를 해결하는 것은 트랜잭션 복제 작동 방법에 대한 기본적인 이해 없이는 불편을 느낄 수 있습니다. 게시를 만드는 첫 번째 단계는 스냅숏 에이전트가 스냅숏을 만들어 스냅숏 폴더에 저장하게 하는 것입니다. 다음으로 배포 에이전트가 스냅숏을 구독자에게 적용합니다. 

이 프로세스는 게시를 만들어 *동기화* 상태에 배치합니다. 동기화는 세 단계로 작동합니다.
1. 트랜잭션은 복제되는 개체에서 발행하며 트랜잭션 로그에 “복제용”으로 표시됩니다. 
2. 로그 판독기 에이전트는 트랜잭션 로그를 통해 검사하고 “복제용”으로 표시된 트랜잭션을 검색합니다. 그런 다음, 이러한 트랜잭션을 배포 데이터베이스에 저장합니다. 
3. 배포 에이전트는 판독기 스레드를 사용하여 배포 데이터베이스를 통해 검사합니다. 그런 다음, 이 에이전트는 기록기 스레드를 사용하여 구독자에 연결하고 해당 변경을 구독자에게 적용합니다.

이 프로세스의 모든 단계에서 오류가 발생할 수 있습니다. 이러한 오류 찾기는 동기화 문제 해결의 가장 어려운 측면일 수 있습니다. 다행히 복제 모니터를 사용하면 이 프로세스가 쉬어집니다. 

>[!NOTE]
> - 이 문제 해결 가이드의 목적은 문제 해결 방법론을 알려주는 데 있습니다. 이 가이드는 해당 특정 오류를 해결하는 대신 복제를 통해 오류를 찾는 데 일반 지침을 제공하도록 설계되었습니다. 몇 가지 구체적인 예제가 제공되지만 해결 방법은 환경에 따라 달라질 수 있습니다. 
> - 이 가이드에서 예제로서 제공하는 오류는 [트랜잭션 복제 구성](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md) 자습서를 기반으로 합니다.



## <a name="troubleshooting-methodology"></a>문제 해결 방법 

### <a name="questions-to-ask"></a>질문
1. 동기화 프로세스의 어디에서 복제가 실패하나요?
2. 어떤 에이전트에 오류가 발생하고 있습니까?
1. 마지막으로 복제가 제대로 작동한 것은 언제입니까? 그 이후로 변경된 사항이 있습니까?  

### <a name="steps-to-take"></a>수행할 단계
1. 복제 모니터를 사용하여 복제가 오류를 발생시키는 시점(에이전트)를 식별합니다.
   - **게시자에서 배포자로 연결** 섹션에서 오류가 발생하는 경우 문제는 로그 판독기 에이전트에 있습니다. 
   - **배포자에서 구독자로 연결** 섹션에서 오류가 발생하는 경우 문제는 배포 에이전트에 있습니다.  
2. 오류의 세부 정보를 식별하려면 작업 활동 모니터에서 해당 에이전트의 작업 기록을 조사합니다. 작업 기록이 충분한 세부 정보를 보여주지 않는 경우 해당 특정 에이전트에서 [자세한 정보 로깅을 사용](#enable-verbose-logging-on-any-agent)할 수 있습니다.
3. 오류에 대한 해결책을 결정하려고 합니다.


## <a name="find-errors-with-the-snapshot-agent"></a>스냅숏 에이전트로 오류 찾기
스냅숏 에이전트는 스냅숏을 생성하여 지정된 스냅숏 폴더에 기록합니다. 

1. 스냅숏 에이전트의 상태를 봅니다.

    1. 개체 탐색기에서 **복제** 아래에서 **로컬 게시** 노드를 확장합니다.

    2. 해당 게시 **AdvWorksProductTrans** > **스냅숏 에이전트 상태 보기**를 마우스 오른쪽 단추로 클릭합니다. 

    ![바로 가기 메뉴의 “스냅숏 에이전트 상태 보기” 명령](media/troubleshooting-tran-repl-errors/view-snapshot-agent-status.png)

1. 스냅숏 에이전트 상태에 오류가 보고되면 스냅숏 에이전트 작업 기록에서 자세한 내용을 확인할 수 있습니다.

    1. 개체 탐색기에서 **SQL Server 에이전트**를 확장하고 작업 활동 모니터를 엽니다. 

    2. **범주**로 정렬하고 **REPL-스냅숏** 범주로 스냅숏 에이전트를 식별합니다.

    c. 스냅숏 에이전트를 오른쪽 단추로 클릭한 다음, **기록 보기**를 선택합니다. 

   ![스냅숏 에이전트 기록을 열기 위한 선택](media/troubleshooting-tran-repl-errors/snapshot-agent-history.png)
    
1. 스냅숏 에이전트 기록에서 관련 로그 항목을 선택합니다. 오류를 보고 하는 항목 *앞에* 하나 또는 두 개의 줄입니다. (빨간색 X가 오류를 나타냅니다.) 로그 아래의 상자에서 메시지 텍스트를 검토합니다. 

    ![액세스가 거부된 스냅숏 에이전트 오류](media/troubleshooting-tran-repl-errors/snapshot-access-denied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.

스냅숏 폴더에 Windows 권한이 올바르게 구성되지 않은 경우 스냅숏 에이전트의 “액세스가 거부됨” 오류가 표시됩니다. 스냅숏이 저장되는 폴더에 대한 사용 권한을 확인해야 하며, 스냅숏 에이전트를 실행하는 데 사용된 계정이 공유에 액세스할 수 있는 권한이 있는지 확인합니다.  

## <a name="find-errors-with-the-log-reader-agent"></a>로그 판독기 에이전트를 사용하여 오류 찾기
로그 판독기 에이전트는 게시자 데이터베이스에 연결하고 트랜잭션 로그에서 '복제용'으로 표시된 트랜잭션을 검색합니다. 그런 다음, 해당 트랜잭션을 배포 데이터베이스에 추가합니다. 

1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결합니다. 서버 노드를 확장하고 **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **복제 모니터 시작**을 선택합니다.  

    ![바로 가기 메뉴에서 "복제 모니터 시작" 명령](media/troubleshooting-tran-repl-errors/launch-repl-monitor.png)
  
    복제 모니터가 열립니다. ![복제 모니터](media/troubleshooting-tran-repl-errors/repl-monitor.png) 
   
2. 빨간색 X는 게시가 동기화되지 않음을 나타냅니다. 왼쪽에서 **내 게시자**를 확장한 다음, 관련 게시자 서버를 확장합니다.  
  
3.  왼쪽에 있는 **AdvWorksProductTrans** 게시를 선택한 다음, 탭 중 하나에서 빨간색 X를 찾아 문제가 어디에 있는지 확인합니다. 이 경우 빨간색 X가 **에이전트** 탭에 있으므로 에이전트 중 하나에 오류가 발생합니다. 

    ![“에이전트” 탭의 빨간색 X](media/troubleshooting-tran-repl-errors/agent-error.png)

4. **에이전트 탭**을 선택하여 오류가 발생한 에이전트를 확인합니다. 

    ![실패한 로그 판독기 에이전트의 빨간색 X](media/troubleshooting-tran-repl-errors/log-reader-agent-failure.png)


5. 이 보기에서는 스냅숏 에이전트와 로그 판독기 에이전트라는 두 에이전트를 보여줍니다. 오류가 발생한 에이전트에 빨간색 X가 있습니다. 이 경우는 로그 판독기 에이전트입니다. 

    오류를 보고하는 줄을 두 번 클릭하여 로그 판독기 에이전트에 대한 에이전트 기록을 엽니다. 이 기록은 오류에 대한 자세한 정보를 제공합니다. 
    
    ![로그 판독기 에이전트에 대한 오류 세부 정보](media/troubleshooting-tran-repl-errors/log-reader-error.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. 오류는 일반적으로 게시자 데이터베이스의 소유자가 올바로 설정되어 있지 않은 경우에 발생합니다. 이는 데이터베이스가 복원되는 경우 발생할 수 있습니다. 이를 확인하려면

    1. 개체 탐색기에서 **데이터베이스**를 확장합니다.

    2. **AdventureWorks2012** > **속성**을 마우스 오른쪽 단추로 클릭합니다. 

    c. **파일** 페이지 아래에 소유자가 있는지 확인합니다. 이 박스가 비어 있는 경우 문제의 가능한 원인은 다음과 같습니다. 

   !["소유자" 상자가 비어 있는 데이터베이스 속성의 "파일" 페이지](media/troubleshooting-tran-repl-errors/db-properties.png)

7. **파일** 페이지에서 소유자가 비어 있는 경우 AdventureWorks2012 데이터베이스의 컨텍스트 내에서 **새 쿼리** 창을 엽니다. 다음 T-SQL 코드를 실행합니다.

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. 로그 판독기 에이전트를 다시 시작해야 할 수 있습니다.

    1. 개체 탐색기에서 **SQL Server 에이전트** 노드를 확장하고 작업 활동 모니터를 엽니다.

    2. **범주**로 정렬하고 **'REPL-LogReader'** 범주로 로그 판독기 에이전트를 확인합니다. 

    c. **로그 판독기 에이전트** 작업을 마우스 오른쪽 단추로 클릭하고 **작업 시작 단계**를 선택합니다. 

    ![로그 판독기 에이전트를 다시 시작하도록 선택](media/troubleshooting-tran-repl-errors/start-job-at-step.png)

9. 복제 모니터를 다시 열어 게시가 동기화되고 있는지 확인합니다. 아직 열려 있지 않은 경우 개체 탐색기에서 **복제**를 마우스 오른쪽 단추로 클릭하여 찾을 수 있습니다. 
10. **AdvWorksProductTrans** 게시, **에이전트** 탭을 차례로 선택하고 로그 판독기 에이전트를 두 번 클릭하여 에이전트 기록을 엽니다. 이제 로그 판독기 에이전트가 실행 중이며 명령을 복제하고 있거나 "복제된 트랜잭션 없음"이라는 메시지가 나타납니다.

    ![복제된 트랜잭션이 없이 실행되는 로그 판독기 에이전트](media/troubleshooting-tran-repl-errors/log-reader-running.png)

## <a name="find-errors-with-the-distribution-agent"></a>배포 에이전트로 오류 찾기
배포 에이전트는 배포 데이터베이스에서 데이터를 찾은 다음, 구독자에게 적용합니다. 

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결합니다. 서버 노드를 확장하고 **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **복제 모니터 시작**을 선택합니다.  
2. **복제 모니터**에서 **AdvWorksProductTrans** 게시를 선택하고, **모든 구독** 탭을 선택합니다. 구독을 오른쪽 단추로 클릭하고 **자세히 보기**를 선택합니다.

    ![바로 가기 메뉴에서 "자세히 보기" 명령](media/troubleshooting-tran-repl-errors/view-details.png)

2. **배포자에서 구독자로 연결 기록** 대화 상자가 열리고, 에이전트에 발생한 오류에 대한 설명이 표시됩니다. 

     ![배포 에이전트에 대한 오류 세부 정보](media/troubleshooting-tran-repl-errors/dist-history-error.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. 이 오류는 배포 에이전트가 다시 시도 중이라는 것을 나타냅니다. 자세한 정보를 찾으려면 배포 에이전트에 대한 작업 기록을 확인합니다. 

    1. 개체 탐색기에서 **SQL Server 에이전트** > **작업 활동 모니터**를 확장합니다. 
    
    2. **범주**별로 작업을 정렬합니다. 

    c. **REPL-Distribution** 범주를 사용하여 배포 에이전트를 확인합니다. 에이전트를 마우스 오른쪽 단추로 클릭하고 **기록 보기**를 선택합니다.

    ![배포 에이전트 기록 보기에 대한 선택](media/troubleshooting-tran-repl-errors/view-dist-agent-history.png)

5. 오류 항목 중 하나를 선택하고 창 아래쪽에서 오류 텍스트를 확인합니다.  

    ![배포 에이전트에 대한 잘못된 암호를 나타내는 오류 텍스트](media/troubleshooting-tran-repl-errors/dist-pw-wrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. 이 오류는 배포 에이전트에서 사용한 암호가 잘못되었음을 나타냅니다. 이를 확인하려면

    1. 개체 탐색기에서 **복제** 노드를 확장합니다.
    
    2. 구독 > **속성**을 마우스 오른쪽 단추로 클릭합니다.
    
    c. **에이전트 프로세스 계정** 옆에 있는 줄임표(...)를 선택하고 암호를 수정합니다.

    ![배포 에이전트에 대한 암호를 수정하기 위한 선택](media/troubleshooting-tran-repl-errors/dist-agent-pw-change.png)

7. 개체 탐색기에서 **복제**를 마우스 오른쪽 단추로 클릭하여 복제 모니터를 다시 확인합니다. **모든 구독**에 있는 빨간색 X는 배포 에이전트에 여전히 오류가 있음을 나타냅니다. 

    **복제 모니터** > **세부 정보 보기**에서 구독을 마우스 오른쪽 단추로 클릭하여 **구독자에게 배포** 기록을 엽니다. 이제 여기에는 오류가 다르게 표시됩니다. 

    ![배포 에이전트가 연결할 수 없음을 나타내는 오류](media/troubleshooting-tran-repl-errors/dist-agent-cant-connect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. 이 오류는 사용자 **NODE2\repl_distribution**에 대한 로그인이 실패했으므로 배포 에이전트가 구독자에게 연결할 수 없음을 나타냅니다. 더 자세히 조사하려면 구독자에 연결하고 개체 탐색기의 **관리** 노드에 있는 *현재*SQL 오류 로그를 엽니다. 

    ![구독자에 대한 로그인이 실패했음을 나타내는 오류](media/troubleshooting-tran-repl-errors/login-failed.png)
    
    이 오류가 표시되는 경우 구독자에 대한 로그인은 누락됩니다. 이 오류를 해결하려면 [복제에 대한 사용 권한](../../relational-databases/replication/security/security-role-requirements-for-replication.md)을 참조합니다.

9. 로그인 오류가 해결된 후 복제 모니터를 다시 확인합니다. 모든 문제가 해결되었으면 **모든 구독**에서 **게시 이름** 옆에 녹색 화살표 및 **실행 중** 상태가 표시됩니다. 

    성공을 확인하려면 구독을 마우스 오른쪽 단추로 클릭하여 **배포자에서 구독자로 연결** 기록을 한 번 더 엽니다. 배포 에이전트를 처음 실행하는 경우, 스냅숏이 구독자에게 대량 복사되었음을 알 수 있습니다. 

     !["실행 중" 상태 및 대량 복사에 대한 메시지가 표시되는 배포 에이전트](media/troubleshooting-tran-repl-errors/dist-agent-success.png)   


## <a name="enable-verbose-logging-on-any-agent"></a>모든 에이전트에 대한 자세한 로깅을 사용하도록 설정
복제 토폴로지의 모든 에이전트에서 발생하는 오류에 대한 더 자세한 정보를 보려면 자세한 로깅을 사용할 수 있습니다. 단계는 각 에이전트의 단계와 동일합니다. 작업 활동 모니터에서 올바른 에이전트를 선택하는지 확인합니다. 

   >[!NOTE]   
   > 에이전트는 구독 밀어넣기 또는 끌어오기 여부에 따라 게시자 또는 구독자 중에 있을 수 있습니다. 바라보고 있는 서버에서 원하는 에이전트를 찾을 수 없는 경우 다른 서버를 확인하도록 하십시오.  

1. 자세한 로깅을 저장할지 여부를 결정하고 폴더가 존재하는지 확인합니다. 이 예에서는 c:\temp를 사용합니다. 
2. 개체 탐색기에서 **SQL Server 에이전트** 노드를 확장하고 작업 활동 모니터를 엽니다. 

    ![작업 활동 모니터에 대한 바로 가기 메뉴의 "작업 활동 보기" 명령](media/troubleshooting-tran-repl-errors/job-activity-monitor.png)    

1. **범주**로 정렬하고 관심 있는 에이전트를 확인합니다. 이 예제에서는 로그 판독기 에이전트를 사용 합니다. 관심 있는 에이전트 > **속성**을 마우스 오른쪽 단추로 클릭합니다.

    ![에이전트 속성을 열기 위한 선택](media/troubleshooting-tran-repl-errors/log-agent-properties.png)

1. **단계** 페이지를 선택한 다음, **에이전트 실행** 단계를 강조 표시합니다. **편집**을 선택합니다. 

    !["에이전트 실행" 단계를 편집하기 위한 선택](media/troubleshooting-tran-repl-errors/edit-steps.png)

1. **명령** 상자에서 새 줄을 시작하고, 다음 텍스트를 입력하고 **확인**을 선택합니다. 

       -Output C:\Temp\OUTPUTFILE.txt -Outputverboselevel 3
    
    선호도에 따라 위치 및 자세한 표시 수준을 수정할 수 있습니다.

    ![작업 단계에 대한 속성에서 자세한 정보 출력](media/troubleshooting-tran-repl-errors/verbose.png)

   > [!NOTE]
   > 이러한 것은 자세한 출력 매개 변수를 추가할 경우 에이전트가 실패하거나 출력 파일이 누락되게 할 수 있습니다.
   > - 대시가 하이픈이 된 경우 서식 지정 문제가 있습니다. 
   > - 해당 위치가 디스크에 존재하지 않거나 에이전트를 실행하는 계정이 지정된 위치에 쓸 수 있는 권한이 부족합니다. 
   > - 마지막 매개 변수 및 `-Output` 매개 변수 간에 누락된 공간이 있습니다. 
   > - 다른 에이전트는 다른 수준의 자세한 정도를 지원합니다. 자세한 로깅을 사용하도록 설정했지만 에이전트가 시작하지 못한 경우 지정된 자세한 표시 수준을 1로 줄여보십시오. 

1. 에이전트 > **중지 작업 단계**를 마우스 오른쪽 단추로 클릭하여 로그 판독기 에이전트를 다시 시작합니다. 도구 모음에서 **새로 고침** 아이콘을 선택하여 새로 고침합니다. 에이전트 > **작업 시작 단계**를 마우스 오른쪽 단추로 클릭합니다.
2. 디스크에서 출력을 검토합니다. 

    ![출력 텍스트 파일](media/troubleshooting-tran-repl-errors/output.png)

    
1. 자세한 정보 로깅을 사용하지 않으려면 이전과 동일한 단계를 따라 전에 추가했던 전체 `-Output` 줄을 제거합니다. 

자세한 내용은 [복제 에이전트에 대한 자세한 정보 로깅 사용하도록 설정](https://support.microsoft.com/help/312292/how-to-enable-replication-agents-for-logging-to-output-files-in-sql-se)을 참조합니다. 


## <a name="see-also"></a>관련 항목:
<br>[트랜잭션 복제 개요](../../relational-databases/replication/transactional/transactional-replication.md)
<br>[복제 자습서](../../relational-databases/replication/replication-tutorials.md)
<br>[ReplTalk 블로그](https://blogs.msdn.microsoft.com/repltalk)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

