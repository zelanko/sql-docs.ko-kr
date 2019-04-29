---
title: sp_change_log_shipping_secondary_primary (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a84ed0105558772752f4d9871ad28a5bffde6bec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997129"
---
# <a name="spchangelogshippingsecondaryprimary-transact-sql"></a>sp_change_log_shipping_secondary_primary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보조 데이터베이스 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @primary_server = ] 'primary_server'` 기본 인스턴스 이름을 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 로그 전달 구성에서 합니다. *primary_server* 됩니다 **sysname** NULL 일 수 없습니다.  
  
`[ @primary_database = ] 'primary_database'` 주 서버에서 데이터베이스의 이름이입니다. *primary_database* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @backup_source_directory = ] 'backup_source_directory'` 주 서버에서 트랜잭션 로그 백업 파일을 저장할 디렉터리입니다. *backup_source_directory* 됩니다 **nvarchar(500)** NULL 일 수 없습니다.  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` 백업 파일이 복사 되는 보조 서버의 디렉터리입니다. *backup_destination_directory* 됩니다 **nvarchar(500)** NULL 일 수 없습니다.  
  
`[ @file_retention_period = ] 'file_retention_period'` 기록이 보존 되는 몇 분 안에 시간의 길이입니다. *history_retention_period* 됩니다 **int**, 기본값은 NULL입니다. 값이 지정되지 않으면 14420이 사용됩니다.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 모니터 서버에 연결할 때 사용할 보안 모드입니다.  
  
 1 = Windows 인증  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. *monitor_server_security_mode* 됩니다 **비트** NULL 일 수 없습니다.  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 모니터 서버에 액세스 하는 데 사용 하는 계정의 사용자 이름이입니다.  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 모니터 서버에 액세스 하는 데 사용 하는 계정의 암호가입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_change_log_shipping_secondary_primary** 에서 실행 해야 합니다 **마스터** 보조 서버의 데이터베이스. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  설정을 변경 합니다 **log_shipping_secondary** 필요에 따라 기록 합니다.  
  
2.  모니터 서버가 보조 서버에서 다른 경우 변경의 모니터 레코드 **log_shipping_monitor_secondary** 모니터 서버를 사용 하 여 제공 된 인수를 필요한 경우.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
