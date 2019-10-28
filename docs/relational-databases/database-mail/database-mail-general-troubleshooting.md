---
title: SQL Server에서의 일반 데이터베이스 메일 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 304306edc78229899b0660b99df6f6b78b60e6ca
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72906081"
---
# <a name="general-database-mail-troubleshooting-steps"></a>일반 데이터베이스 메일 문제 해결 단계 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

데이터베이스 메일의 문제 해결 과정은 데이터베이스 메일 시스템의 다음과 같은 일반적인 영역에 대한 확인이 포함됩니다. 이 절차는 논리적 순서로 나열했으나 어떤 순서로도 검사할 수 있습니다.

## <a name="permissions"></a>사용 권한

모든 측면의 데이터베이스 메일 문제를 해결하려면 sysadmin 고정 서버 역할의 멤버여야 합니다. sysadmin 고정 서버 역할의 멤버가 아닌 사용자는 자신이 보내는 이메일 정보만 가져올 수 있고 다른 사용자가 보내는 이메일 정보는 가져올 수 없습니다.

## <a name="is-database-mail-enabled"></a>데이터베이스 메일 사용

1. SQL Server Management Studio에서 쿼리 편집기 창을 사용하여 SQL Server 인스턴스에 연결한 후 다음 코드를 실행합니다.

    ```sql
    sp_configure 'show advanced', 1; 
    GO
    RECONFIGURE;
    GO
    sp_configure;
    GO
    ```

   결과 창에서 [Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)에 대한 run_value가 1로 설정되었는지 확인합니다.
   run_value가 1이 아니면 데이터베이스 메일을 사용하지 않습니다. 악의적인 사용자가 공격에 사용할 수 있는 기능의 수를 줄이기 위해 데이터베이스 메일은 자동으로 사용되도록 설정되지는 않습니다. 자세한 내용은 [노출 영역 구성 이해](../security/surface-area-configuration.md)를 참조하세요.

1. 데이터베이스 메일을 사용하는 것이 적절하다고 판단되는 경우에는 다음 코드를 실행합니다.

    ```sql
    sp_configure 'Database Mail XPs', 1; 
    GO
    RECONFIGURE;
    GO
    ```

1. sp_configure 프로시저를 고급 옵션이 표시되지 않는 기본 상태로 복원하려면 다음 코드를 실행합니다.

    ```sql 
    sp_configure 'show advanced', 0; 
    GO
    RECONFIGURE;
    GO
    ```

## <a name="are-users-properly-configured-to-send-mail"></a>사용자가 올바르게 메일을 보내도록 구성

1. 데이터베이스 메일을 보내려면 사용자가 msdb 데이터베이스에서 DatabaseMailUserRole 데이터베이스 역할의 멤버여야 합니다. sysadmin 고정 서버 역할 및 msdbdb_owner 역할의 멤버는 자동으로 DatabaseMailUserRole 역할의 멤버가 됩니다. DatabaseMailUserRole의 모든 다른 멤버를 표시하려면 다음 명령문을 실행합니다.

    ```sql
    EXEC msdb.sys.sp_helprolemember 'DatabaseMailUserRole';
    ```

1. DatabaseMailUserRole 역할에 사용자를 추가하려면 다음 명령문을 사용합니다.

    ```sql
    USE msdb;
    GO
    
    sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<database user>';
    ```

1. 데이터베이스 메일을 보내려면 사용자는 최소 하나의 데이터베이스 메일 프로필에 액세스 권한이 있어야 합니다. 사용자(보안 주체) 및 사용자가 액세스할 수 있는 프로필을 표시하려면 다음 명령문을 실행합니다.

    ```sql
    EXEC msdb.dbo.sysmail_help_principalprofile_sp;
    ```

1. 데이터베이스 메일 구성 마법사를 사용하여 프로필을 만들고 사용자에게 프로필에 대한 액세스 권한을 부여할 수 있습니다.
 
## <a name="is-database-mail-started"></a>데이터베이스 메일 시작

1. [데이터베이스 메일 외부 프로그램](database-mail-external-program.md)은 처리할 이메일 메시지가 있을 때 활성화됩니다. 지정된 제한 시간 동안 보낼 메시지가 없는 경우 프로그램이 종료됩니다. 데이터베이스 메일 활성화가 시작되었는지 확인하려면 다음 명령문을 실행합니다.

    ```sql
    EXEC msdb.dbo.sysmail_help_status_sp;
    ```
1. 데이터베이스 메일이 시작되지 않은 경우 다음 명령문을 실행하여 시작합니다.

    ```sql
    EXEC msdb.dbo.sysmail_start_sp;
    ```

1. 데이터베이스 메일 외부 프로그램이 시작된 경우 다음 명령문으로 메일 큐의 상태를 확인합니다.

    ```sql
    EXEC msdb.dbo.sysmail_help_queue_sp @queue_type = 'mail';
    ```
  
   메일 큐에는 RECEIVES_OCCURRING 문이 있어야 합니다. 상태 큐는 시시각각 달라집니다. 메일 큐 상태가 RECEIVES_OCCURRING이 아니라면 큐를 다시 시작합니다. 다음 명령문을 사용하여 큐를 중지합니다.
   
```sql
EXEC msdb.dbo.sysmail_stop_sp;
```

이 후 다음 명령문을 사용하여 큐를 시작합니다.

```sql
EXEC msdb.dbo.sysmail_start_sp;
```

  > [!NOTE]
  >  sysmail_help_queue_sp 결과 집합의 length 열을 사용하여 메일 큐의 이메일 수를 확인합니다.

## <a name="do-problems-affect-some-or-all-accounts"></a>문제가 일부 또는 전체 계정에 영향을 미침

1. 일부 프로필에서 메일을 보낼 수 없는 문제를 확인한 경우 문제가 있는 프로필에서 사용하는 데이터베이스 메일 계정에 문제가 있을 수 있습니다. 메일 보내기가 가능한 계정을 확인하려면 다음 명령문을 실행합니다.

    ```sql
    SELECT sent_account_id, sent_date FROM msdb.dbo.sysmail_sentitems;
    ```

1. 작동하지 않는 프로필이 목록의 계정 중 어느 것도 사용하지 않는 경우, 해당 프로필에서 사용 가능한 모든 계정이 제대로 작동하지 않을 수 있습니다. 개별 계정을 테스트하려면 데이터베이스 메일 구성 마법사를 사용하여 단일 계정이 있는 새 프로필을 만든 다음, 테스트 이메일 보내기 대화 상자에서 새 계정을 사용하여 메일을 보냅니다. 
1. 데이터베이스 메일이 반환한 오류 메시지를 보려면 다음 명령문을 실행합니다.

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log;
    ```

   > [!NOTE]
   > 데이터베이스 메일은 메일이 SMTP 메일 서버로 배달되면 메일을 보낸 것으로 간주합니다. 이후 잘못된 수신인 이메일 주소와 같은 오류로 인해 메일이 배달되지 않더라도 데이터베이스 메일 로그에는 나타나지 않을 수 있습니다.

## <a name="retry-mail-delivery"></a>메일 배달 다시 시도

1. SMTP 서버에 접근할 수 없어 데이터베이스 메일의 배달이 실패했음을 확인한 경우 데이터베이스 메일이 각 메시지를 보내려는 시도 횟수를 늘려 메일 배달 성공률을 높일 수 있습니다. 데이터베이스 메일 구성 마법사를 시작하고 시스템 매개 변수 확인 또는 변경 옵션을 선택합니다. 또는 추가 계정을 장애 조치(failover) 계정으로 해당 프로필에 연결하여 기본 계정이 실패하면 데이터베이스 메일이 장애 조치 계정을 사용하여 이메일을 보내도록 할 수 있습니다.
1. 시스템 매개 변수 구성 페이지에서 기본값 5회로 지정된 계정 다시 시도 횟수와 기본값 60초로 지정된 계정 다시 시도 간격은 SMTP 서버에 5분 동안 접근할 수 없으면 메시지 배달이 실패함을 의미합니다. 이 매개 변수 값을 늘리면 메시지 배달이 실패하기까지의 시간을 늘릴 수 있습니다.

    > [!NOTE]
    > 기본값이 높아지면 안정성이 향상될 수 있으나 많은 메시지를 보낼 경우 계속해서 많은 메시지의 배달을 시도하므로 리소스 사용도 많아집니다. 데이터베이스 메일이 SMTP 서버에 즉시 연결하지 못하도록 하는 네트워크나 SMTP 서버 문제를 찾아 근본적인 원인을 해결하십시오.



##  <a name="RelatedContent"></a> 참고 항목
  
-   [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)  
  
-   [데이터베이스 메일 메시징 개체](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
-   [데이터베이스 메일 외부 프로그램](../../relational-databases/database-mail/database-mail-external-program.md)  
  
-   [데이터베이스 메일 로그 및 감사](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
-   [데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
  
