---
description: 데이터베이스 메일로 테스트 이메일 보내기
title: 데이터베이스 메일로 테스트 이메일 보내기 | Microsoft Docs
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
ms.openlocfilehash: b715e65e4dfaa623f56b0caa2a78b03231819deb
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88494543"
---
# <a name="send-a-test-email-with-database-mail"></a>데이터베이스 메일로 테스트 이메일 보내기  
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

테스트 이메일 보내기 대화 상자를 사용하여 특정 프로필을 사용한 메일 보내기 기능을 테스트할 수 있습니다.

## <a name="permissions"></a>사용 권한

테스트 이메일 보내기 대화 상자를 사용하려면 sysadmin 고정 서버 역할의 멤버여야 합니다. sysadmin 고정 서버 역할의 멤버가 아닌 사용자는 [sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) 프로시저를 사용하여 데이터베이스 메일을 테스트할 수 있습니다.

## <a name="procedure"></a>프로시저

1. [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)에서 개체 탐색기를 사용하여 데이터베이스 메일을 구성한 SQL Server Database Engine 인스턴스에 연결하고 관리를 확장한 다음, 데이터베이스 메일을 마우스 오른쪽 단추로 클릭하고 테스트 이메일 보내기를 클릭합니다. 데이터베이스 메일 프로필이 없으면 프로필을 만들지 묻는 메시지가 나타나고 데이터베이스 메일 구성 마법사가 열립니다.
1. <instance name> 대화 상자의 **테스트 이메일 보내기** 에 있는 데이터베이스 메일 프로필 상자에서 테스트할 프로필을 선택합니다.
1. **받는 사람** 입력란에 테스트 이메일의 수신인 이메일 이름을 입력합니다.
1. **제목** 입력란에 테스트 이메일의 제목 줄을 입력합니다. 문제 해결을 위해 사용자의 전자 메일을 보다 잘 식별할 수 있도록 기본 제목을 변경합니다.
1. **본문** 입력란에 테스트 이메일의 본문을 입력합니다. 문제 해결을 위해 사용자의 전자 메일을 보다 잘 식별할 수 있도록 기본 제목을 변경합니다.
1. **테스트 이메일 보내기** 를 선택하여 테스트 이메일을 데이터베이스 메일 큐로 보냅니다.
1. 테스트 이메일을 보내면 데이터베이스 메일 테스트 이메일 대화 상자가 열립니다. 보낸 이메일 부분에 표시되는 숫자를 확인합니다. 이 숫자가 테스트 메시지의 mailitem_id입니다. 확인을 선택합니다.
1. 도구 모음에서 새 쿼리를 선택하여 쿼리 편집기 창을 엽니다. 다음 T-SQL 문을 실행하여 테스트 이메일 메시지의 상태를 확인합니다.

    ```sql
    SELECT * FROM msdb.dbo.sysmail_allitems 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```

    sent_status 열은 테스트 이메일 메시지를 보냈는지 여부를 표시합니다.

1. 오류가 발생한 경우 다음 문을 실행하여 오류 메시지를 확인합니다.

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```


##  <a name="see-also"></a><a name="RelatedContent"></a> 참고 항목 
  
-   [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)
-   [데이터베이스 메일 메시징 개체](../../relational-databases/database-mail/database-mail-messaging-objects.md)
-   [데이터베이스 메일 외부 프로그램](../../relational-databases/database-mail/database-mail-external-program.md)
-   [데이터베이스 메일 로그 및 감사](../../relational-databases/database-mail/database-mail-log-and-audits.md)
-   [데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)
  
  
