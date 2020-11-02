---
description: MSSQLSERVER_17892
title: MSSQLSERVER_17892
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17892 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 59cf1ed10d71bf9813f2ce814d88e7f7d64b6b2e
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418788"
---
# <a name="mssqlserver_17892"></a>MSSQLSERVER_17892
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|17892|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|SRV_LOGON_FAILED_BY_TRIGGER|
|메시지 텍스트|트리거 실행으로 인해 \<Login Name> 로그인에 대해 로그온하지 못했습니다.|
||

## <a name="explanation"></a>설명

로그온 트리거 코드를 성공적으로 실행하지 못하면 오류 17892가 발생합니다. [로그온 트리거](/sql/relational-databases/triggers/logon-triggers)는 로그온 이벤트에 대한 응답으로 저장 프로시저를 실행합니다. 이 이벤트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 사용자 세션이 설정된 경우 발생합니다. 사용자에게 보고되는 오류 메시지는 다음과 같습니다.

> 메시지 17892, 수준 14, 상태 1, 서버 \<Server Name>, 줄 1  
트리거 실행으로 인해 \<Login Name> 로그인에 대해 로그온하지 못했습니다.

## <a name="possible-causes"></a>가능한 원인

오류로 인해 특정 사용자 계정에 대해 트리거 코드를 실행하지 못할 경우 이 문제가 발생할 수 있습니다. 몇 가지 시나리오는 다음과 같습니다.

- 트리거가 존재하지 않는 테이블에 데이터를 삽입하려고 합니다.
- 로그인에 로그온 트리거가 참조하는 개체에 대한 권한이 없습니다.

## <a name="user-action"></a>사용자 조치

해당 시나리오에 따라 아래 해결 방법 중 하나를 사용할 수 있습니다.

- **시나리오 1** : 현재 관리자 계정으로 열려 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션에 액세스할 수 있습니다.

  이 경우에는 트리거 코드를 수정하는 데 필요한 정정 작업을 수행할 수 있습니다.

  - 예제 1: 트리거 코드에서 참조하는 개체가 없는 경우 해당 개체를 만들어 로그인 트리거가 성공적으로 실행될 수 있도록 합니다.

  - 예제 2: 트리거 코드에서 참조하는 개체가 존재하지만 사용자에게 권한이 없는 경우 개체에 액세스하는 데 필요한 권한을 부여합니다.  
  
  또는 사용자가 계속해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인할 수 있도록 로그인 트리거를 삭제하거나 사용하지 않도록 설정할 수 있습니다.  

- **시나리오 2** : 현재 관리자 권한으로 열려 있는 세션은 없지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 DAC(관리자 전용 연결)를 사용할 수 있습니다.

    이 경우에는 로그인 트리거의 영향을 받지 않는 DAC 연결을 사용하여 사례 1에서 설명한 것과 동일한 단계를 수행할 수 있습니다. DAC 연결에 대한 자세한 내용은 다음을 참조하세요. [데이터베이스 관리자를 위한 진단 연결](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators)

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 DAC를 사용할 수 있는지 확인하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 다음과 같은 메시지가 있는지 살펴봅니다.

    > 2020-02-09 16:17:44.150 서버 전용 관리자 연결 지원이 포트 1434의 로컬 수신 대기용으로 설정되었습니다.  

- **시나리오 3** : 서버에서 DAC를 사용할 수 없으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 기존 관리자 세션도 없습니다.

    이 시나리오에서 문제를 해결하려면 다음 단계를 수행해야 합니다.
  
    1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 관련 서비스를 중지합니다.
    2. 시작 매개 변수 `-c`, `-m`, `-f`를 사용하여 [명령 프롬프트](/previous-versions/sql/sql-server-2008-r2/ms180965(v=sql.105))에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작합니다. 이렇게 하면 로그인 트리거가 사용하지 않도록 설정되고, 위의 **사례 1** 에서 설명한 것과 동일한 수정 조치를 수행할 수 있습니다.
  
        > [!NOTE]
        > 위의 절차를 수행하려면 *SA* 또는 이와 동등한 관리자 계정이 필요합니다.
  
         관련 시작 옵션 및 기타 시작 옵션에 대한 자세한 내용은 다음을 참조하세요. [데이터베이스 엔진 서비스 시작 옵션](/sql/database-engine/configure-windows/database-engine-service-startup-options)

## <a name="more-information"></a>자세한 정보

로그온 트리거가 실패하는 또 다른 상황은 `EVENTDATA` 함수를 사용하는 경우입니다. 이 함수는 XML을 반환하며 대/소문자를 구분합니다.  따라서 IP 주소를 기준으로 액세스를 차단하기 위해 다음과 같은 로그온 트리거를 만들면 문제가 발생할 수 있습니다.

``` sql
 CREATE TRIGGER tr_logon_CheckIP  
 ON ALL SERVER  
 FOR LOGON  
 AS
 BEGIN
  IF IS_SRVROLEMEMBER ( 'sysadmin' ) = 1  
     BEGIN
         DECLARE @IP NVARCHAR ( 15 );  
         SET @IP = ( SELECT EVENTDATA ().value ( '(/EVENT_INSTANCE/ClientHost)[1]' , 'NVARCHAR(15)' ));  
         IF NOT EXISTS( SELECT IP FROM DBAWork.dbo.ValidIP WHERE IP = @IP )  
         ROLLBACK ;  
     END ;  
 END ;  
 GO
```

사용자는 인터넷을 통해 다음 트리거 쪽에서 이 스크립트를 복사할 때 대/소문자를 유지하지 않았습니다.

```sql
 SELECT EVENTDATA ().value ( '(/event_instance/clienthost)[1]' , 'NVARCHAR(15)' ));  
```

결과적으로 `EVENTDATA`에서 항상 **NULL** 이 반환되었으며, SA와 동등한 모든 로그인에 대해 액세스가 거부되었습니다. 이 경우에는 DAC 연결을 사용할 수 없기 때문에 트리거를 삭제하기 위해 위에 나열된 시작 매개 변수로 서버를 다시 시작해야 했습니다.
