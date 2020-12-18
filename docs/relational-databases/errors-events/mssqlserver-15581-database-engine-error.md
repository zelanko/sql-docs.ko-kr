---
description: MSSQLSERVER_15581
title: MSSQLSERVER_15581
ms.custom: ''
ms.date: 09/03/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha, VenCher
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15581 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f1221474d86d95400ca955d64b4a0812cffe1c0d
ms.sourcegitcommit: f87f2f0f1edc91fe400040d8e3a5810347aa8d70
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96868905"
---
# <a name="mssqlserver_15581"></a>MSSQLSERVER_15581
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|15581|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|SEC_NODBMASTERKEYERR|
|메시지 텍스트|이 작업을 수행하기 전에 데이터베이스에서 마스터 키를 만들거나 세션의 마스터 키를 여십시오.|
||

## <a name="explanation"></a>설명

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TDE(투명한 데이터 암호화)를 사용하도록 설정된 데이터베이스를 복구할 수 없는 경우 오류 15581이 발생합니다. 다음과 같은 오류 메시지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 기록됩니다.

> 2020-01-14 22:16:26.47 spid20s 오류: 15581, 심각도: 16, 상태: 3.  
2020-01-14 22:16:26.47 spid20s 이 작업을 수행하기 전에 데이터베이스에서 마스터 키를 만들거나 세션의 마스터 키를 열어야 합니다.

## <a name="possible-cause"></a>가능한 원인

이 문제는 다음 명령을 실행할 때 master 데이터베이스의 데이터베이스 마스터 키에 대한 서비스 마스터 키 암호화가 제거될 때 발생합니다.

```sql
Use master
go
alter master key drop encryption by service master key
```

서비스 마스터 키는 데이터베이스 마스터 키에 사용되는 인증서를 암호화하는 데 사용됩니다. TDE 사용 데이터베이스를 사용하려면 master 데이터베이스의 데이터베이스 마스터 키에 액세스해야 합니다. 서비스 마스터 키로 암호화되지 않은 마스터 키는 마스터 키에 액세스해야 하는 각 세션에서 암호와 함께 [OPEN MASTER KEY(Transact-SQL)](/sql/t-sql/statements/open-master-key-transact-sql) 문을 사용하여 열어야 합니다. 이 명령은 시스템 세션에서 실행할 수 없기 때문에 TDE 사용 데이터베이스에서 복구를 완료할 수 없습니다.

## <a name="user-action"></a>사용자 조치

이 문제를 해결하려면 마스터 키의 자동 암호 해독을 사용하도록 설정합니다. 이렇게 하려면 다음 명령을 실행합니다.

```sql
Use master
go
open master key DECRYPTION BY PASSWORD = 'password'
alter master key add encryption by service master key
```

다음 쿼리를 사용하여 master 데이터베이스에 대해 서비스 마스터 키에 의한 마스터 키의 자동 암호 해독이 사용하지 않도록 설정되었는지를 확인합니다.

```sql
select is_master_key_encrypted_by_server from sys.databases where name = 'master'
```

이 쿼리에서 0 값을 반환하면 서비스 마스터 키에 의한 마스터 키의 자동 암호 해독이 사용하지 않도록 설정된 것입니다.

## <a name="more-information"></a>자세한 정보

경우에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 응답하지 않을 수 있습니다. `sys.dm_exec_requests` 동적 관리 뷰를 쿼리하면 DML 작업을 수행하는 `LogWriter` 스레드 및 기타 스레드가 WRITELOG wait_type을 사용하여 무기한 대기하고 있음을 알 수 있습니다. 잠금을 가져오려고 하는 동안 다른 세션도 대기할 수 있습니다.
