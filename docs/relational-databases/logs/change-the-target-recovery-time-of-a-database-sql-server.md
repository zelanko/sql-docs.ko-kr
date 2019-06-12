---
title: 데이터베이스의 대상 복구 시간 변경(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f47d33179fb382472def9950a928be137e1f6583
ms.sourcegitcommit: 36c5f28d9fc8d2ddd02deb237937c9968d971926
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354386"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>데이터베이스의 대상 복구 시간 변경(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]데이터베이스의 대상 복구 시간을 설정하거나 변경하는 방법에 대해 설명합니다. 기본적으로 대상 복구 시간은 60초이고, 데이터베이스에서는 *간접 검사점*을 사용합니다. 대상 복구 시간에서는 이 데이터베이스에 대한 복구 시간의 상한이 설정됩니다.  
  
> [!NOTE]  
>  장기 실행 트랜잭션으로 인해 UNDO 시간이 과도하게 길어지는 경우 주어진 데이터베이스에 대해 대상 복구 시간 설정에 지정된 상한이 초과될 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Restrictions), [보안](#Security)  
  
-   **대상 복구 시간을 변경하려면 다음을 사용합니다.**  [SQL Server Management Studio](#SSMSProcedure) 또는 [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항 
  
> [!CAUTION]  
>  간접 검사점이 구성된 데이터베이스의 온라인 트랜잭션 작업으로 인해 성능이 저하될 수 있습니다. 간접 검사점은 데이터베이스 복구가 대상 복구 시간 내에 완료되도록 더티 페이지 수가 특정 임계값보다 적은지 확인합니다. 복구 간격 구성 옵션은 더티 페이지 수를 사용하는 간접 검사점과 달리 트랜잭션 수를 사용하여 복구 시간을 결정합니다. 많은 수의 DML 작업을 수신하는 데이터베이스에서 간접 검사점을 사용하도록 설정하는 경우 복구 수행에 필요한 시간이 데이터베이스의 대상 복구 시간 설정 내로 유지되도록 백그라운드 기록기가 더티 버퍼를 디스크로 적극적으로 플러시하기 시작할 수 있습니다. 이로 인해 특정 시스템에서 추가 I/O 작업이 발생할 수 있으므로 디스크 하위 시스템이 I/O 임계값 위에서 또는 근처에서 작동하는 경우 성능 병목 현상에 영향을 줄 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **대상 복구 시간을 변경하려면**  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스** 컨테이너를 펼친 다음, 변경할 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성** 명령을 클릭합니다.  
  
3.  **데이터베이스 속성** 대화 상자에서 **옵션** 페이지를 클릭합니다.  
  
4.  **복구** 패널의 **대상 복구 시간(초)** 필드에서 이 데이터베이스에 대한 복구 시간의 상한으로 사용할 시간(초)을 지정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **대상 복구 시간을 변경하려면**  
  
1.  데이터베이스가 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  다음 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 문을 다음과 같이 사용합니다.  
  
     TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]부터 기본값은 1분입니다. 0(이전 버전 기본값)보다 큰 경우 충돌 시 지정된 데이터베이스에 대한 복구 시간의 상한을 지정합니다.  
  
     SECONDS  
     *target_recovery_time* 이 초 단위로 표현됨을 나타냅니다.  
  
     MINUTES  
     *target_recovery_time* 이 분 단위로 표현됨을 나타냅니다.  
  
     다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 대상 복구 시간을 `60` 초로 설정합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
