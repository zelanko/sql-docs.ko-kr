---
description: sp_change_log_shipping_secondary_primary(Transact-SQL)
title: sp_change_log_shipping_secondary_primary (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b17019380bc65d1b3d2fcdb16352fe32477c6bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474514"
---
# <a name="sp_change_log_shipping_secondary_primary-transact-sql"></a>sp_change_log_shipping_secondary_primary(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  보조 데이터베이스 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>인수  
`[ @primary_server = ] 'primary_server'`[!INCLUDE[msCoName](../../includes/msconame-md.md)]로그 전달 구성에 있는의 주 인스턴스 이름입니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . *primary_server* 는 **sysname** 이며 NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'` 주 서버에 있는 데이터베이스의 이름입니다. *primary_database* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @backup_source_directory = ] 'backup_source_directory'` 주 서버의 트랜잭션 로그 백업 파일이 저장 되는 디렉터리입니다. *backup_source_directory* 는 **nvarchar (500)** 이며 NULL 일 수 없습니다.  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` 백업 파일이 복사 되는 보조 서버의 디렉터리입니다. *backup_destination_directory* 는 **nvarchar (500)** 이며 NULL 일 수 없습니다.  
  
`[ @file_retention_period = ] 'file_retention_period'` 기록이 보존 되는 시간 (분)입니다. *history_retention_period* 은 **int**이며 기본값은 NULL입니다. 값이 지정되지 않으면 14420이 사용됩니다.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 모니터 서버에 연결 하는 데 사용 되는 보안 모드입니다.  
  
 1 = Windows 인증  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 *monitor_server_security_mode* 은 **bit** 이며 NULL 일 수 없습니다.  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 모니터 서버에 액세스 하는 데 사용 되는 계정의 사용자 이름입니다.  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 모니터 서버에 액세스 하는 데 사용 되는 계정의 암호입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_change_log_shipping_secondary_primary** 는 보조 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  필요에 따라 **log_shipping_secondary** 레코드의 설정을 변경 합니다.  
  
2.  모니터 서버가 보조 서버와 다른 경우 필요 하면 제공 된 인수를 사용 하 여 모니터 서버에서 **log_shipping_monitor_secondary** 의 모니터 레코드를 변경 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
