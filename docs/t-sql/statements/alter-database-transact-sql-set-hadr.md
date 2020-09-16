---
description: ALTER DATABASE SET HADR(Transact-SQL)
title: ALTER DATABASE SET HADR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET HADR
- SET_HADR_TSQL
- HADR_TSQL
- HADR
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE statement, AlwaysOn Availability Group
- ALTER DATABASE statement, SET HADR options
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
- Availability Groups [SQL Server], databases
ms.assetid: 20e6e803-d6d5-48d5-b626-d1e0a73d174c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2c8c60b6777165496dca1fc2c131cfe8798e6d72
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540747"
---
# <a name="alter-database-transact-sql-set-hadr"></a>ALTER DATABASE(Transact-SQL) SET HADR 
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 보조 데이터베이스에서 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 옵션 설정에 대해 ALTER DATABASE 구문을 제공합니다. ALTER DATABASE 문당 하나의 SET HADR 옵션만 허용됩니다. 이러한 옵션은 보조 복제본에만 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER DATABASE database_name  
   SET HADR   
   {  
        { AVAILABILITY GROUP = group_name | OFF }  
   | { SUSPEND | RESUME }  
   }  
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *database_name*  
 수정할 보조 데이터베이스의 이름입니다.  
  
 SET HADR  
 지정한 데이터베이스에 대해 지정한 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 명령을 실행합니다.  
  
 { AVAILABILITY GROUP **=** _group_name_ | OFF }  
 다음과 같이 지정한 데이터베이스를 지정한 가용성 그룹에 조인하거나 그룹에서 제거합니다.  
  
 *group_name*  
 명령을 실행한 서버 인스턴스에서 호스팅되는 보조 복제본의 지정한 데이터베이스를 group_name에 지정한 가용성 그룹에 조인합니다.  
  
 이 작업을 수행하려면 다음 선행 조건이 충족되어야 합니다.  
  
-   데이터베이스가 주 복제본의 가용성 그룹에 추가되어 있어야 합니다.  
  
-   주 복제본이 활성 상태여야 합니다. 비활성 주 복제본 문제를 해결하는 방법은 [AlwaysOn 가용성 그룹 구성 문제 해결(SQL Server)](https://go.microsoft.com/fwlink/?LinkId=225834)을 참조하십시오.  
  
-   주 복제본이 온라인 상태여야 하고 보조 복제본이 주 복제본에 연결되어 있어야 합니다.  
  
-   보조 데이터베이스가 주 데이터베이스를 따라잡을 수 있도록 WITH NORECOVERY를 사용하여 보조 데이터베이스를 최신 데이터베이스 및 주 데이터베이스의 로그 백업에서 복원해야 합니다.  
  
    > [!NOTE]  
    >  데이터베이스를 가용성 그룹에 추가하려면 주 복제본을 호스팅하는 서버 인스턴스에 연결한 후 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* ADD DATABASE *database_name* 문을 사용합니다.  
  
 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
 OFF  
 지정한 보조 데이터베이스를 가용성 그룹에서 제거합니다.  
  
 보조 데이터베이스가 주 데이터베이스보다 오래되었거나 보조 데이터베이스가 주 데이터베이스를 따라잡을 때까지 기다리고 싶지 않은 경우 보조 데이터베이스를 제거하면 유용합니다. 보조 데이터베이스를 제거한 후 최신 로그 백업으로 끝나는 백업 시퀀스를 복원하여 데이터베이스를 업데이트할 수 있습니다(RESTORE … WITH NORECOVERY 를 사용하여).  
  
> [!IMPORTANT]  
>  가용성 데이터베이스를 가용성 그룹에서 완전히 제거하려면 주 복제본을 호스팅하는 서버 인스턴스에 연결한 후 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* REMOVE DATABASE *availability_database_name* 문을 사용합니다. 자세한 내용은 [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)를 참조하세요.  
  
 SUSPEND  
 보조 데이터베이스에서 데이터 이동을 일시 중지합니다. SUSPEND 명령은 대상 데이터베이스를 호스팅하는 복제본에서 수락되는 즉시 반환하지만 실제로 데이터베이스 일시 중지는 비동기식으로 발생합니다.  
  
 영향을 받는 범위는 ALTER DATABASE 문을 실행하는 위치에 따라 달라집니다.  
  
-   보조 복제본에서 보조 데이터베이스를 일시 중지하는 경우 로컬 보조 데이터베이스만 일시 중지됩니다. 읽기 가능한 보조 복제본에 대한 기존 연결은 계속 사용할 수 있습니다. 읽기 가능한 보조 복제본의 일시 중단된 데이터베이스에 대한 새 연결은 데이터 이동이 다시 시작될 때까지 허용되지 않습니다.  
  
-   주 복제본에서 데이터베이스를 일시 중지하면 모든 보조 복제본에 있는 해당 보조 데이터베이스로의 데이터 이동이 일시 중지됩니다. 읽기 가능한 보조 복제본에서 기존 연결은 계속 사용 가능하며, 새 읽기 전용 연결은 읽기 가능한 보조 복제본에 연결되지 않습니다.  
  
-   강제 수동 장애 조치로 인해 데이터 이동이 일시 중단되면 데이터 이동이 일시 중단된 동안에는 새로운 보조 복제본에 대한 연결은 허용되지 않습니다.  
  
 보조 복제본의 데이터베이스를 일시 중지하면 데이터베이스와 복제본이 모두 동기화되지 않아 NOT SYNCHRONIZED로 표시됩니다.  
  
> [!IMPORTANT]  
>  보조 데이터베이스를 일시 중지하면 보내지 않은 트랜잭션 로그 레코드가 해당 주 데이터베이스의 Send Queue에 누적됩니다. 보조 복제본에 대한 연결은 데이터 이동이 일시 중단된 시간에 사용 가능했던 데이터를 반환합니다.  
  
> [!NOTE]  
>  AlwaysOn 보조 데이터베이스를 일시 중지한 후 재개해도 주 데이터베이스의 가용성에 직접 영향을 주지는 않습니다. 보조 데이터베이스를 일시 중지하면 일시 중지된 보조 데이터베이스를 재개할 때까지 주 데이터베이스의 중복 및 장애 조치(failover) 기능에 영향을 줄 수는 있습니다. 이것은 데이터베이스 미러링과는 대조적입니다. 데이터베이스 미러링의 경우에는 미러링을 재개할 때까지 미러 데이터베이스 및 주 데이터베이스에서 미러링 상태가 일시 중지됩니다. Always On 주 데이터베이스를 일시 중지하면 모든 해당 보조 데이터베이스에서 데이터 이동이 일시 중지되고 주 데이터베이스를 재개할 때까지 해당 데이터베이스에 대한 중복 및 장애 조치(failover) 기능이 중단됩니다.  
  
 자세한 내용은 이 항목 뒷부분에 나오는 [가용성 데이터베이스 일시 중단 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)을 참조합니다.  
  
 RESUME  
 지정한 보조 데이터베이스에서 일시 중지된 데이터 이동을 다시 시작합니다. RESUME 명령은 대상 데이터베이스를 호스팅하는 복제본에서 수락되는 즉시 반환하지만 실제로 데이터베이스 재개는 비동기식으로 발생합니다.  
  
 영향을 받는 범위는 ALTER DATABASE 문을 실행하는 위치에 따라 달라집니다.  
  
-   보조 복제본에서 보조 데이터베이스를 다시 시작하는 경우 로컬 보조 데이터베이스만 다시 시작됩니다. 주 복제본에서도 데이터베이스가 일시 중지된 경우가 아니면 데이터 이동이 다시 시작됩니다.  
  
-   주 복제본에서 데이터베이스를 다시 시작할 경우 해당 보조 데이터베이스가 로컬로 일시 중지되지 않은 모든 보조 복제본으로의 데이터 이동이 다시 시작됩니다. 보조 복제본에서 개별적으로 일시 중지한 보조 데이터베이스를 다시 시작하려면 보조 복제본을 호스팅하는 서버 인스턴스에 연결한 후 이 서버에서 데이터베이스를 다시 시작합니다.  
  
     동기-커밋 모드에서는 데이터베이스 상태가 SYNCHRONIZING으로 변경됩니다. 현재 일시 중지된 다른 데이터베이스가 없으면 복제본 상태도 SYNCHRONIZING으로 변경됩니다.  
  
     자세한 내용은 이 항목 뒷부분에 나오는 [가용성 데이터베이스 재개&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)에서 가용성 데이터베이스를 일시 중지할 수 있습니다.  
  
## <a name="database-states"></a>데이터베이스 상태  
 보조 데이터베이스를 가용성 그룹에 조인하면 로컬 보조 복제본은 해당 보조 데이터베이스의 상태를 RESTORING에서 ONLINE으로 변경합니다. 보조 데이터베이스를 가용성 그룹에서 제거하면 로컬 보조 복제본은 보조 데이터베이스를 다시 RESTORING 상태로 설정합니다. 따라서 주 데이터베이스의 후속 로그 백업을 해당 보조 데이터베이스에 적용할 수 있습니다.  
  
## <a name="restrictions"></a>제한  
 트랜잭션 및 일괄 처리 외부에서 ALTER DATABASE 문을 실행합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다. 데이터베이스를 가용성 그룹에 조인하려면 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `AccountsDb1`이라는 보조 데이터베이스를 `AccountsAG` 가용성 그룹의 로컬 보조 복제본에 조인합니다.  
  
```  
ALTER DATABASE AccountsDb1 SET HADR AVAILABILITY GROUP = AccountsAG;  
```  
  
> [!NOTE]  
>  컨텍스트에서 사용되는 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 보려면 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [AlwaysOn 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) [AlwaysOn 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md) 
  
  
