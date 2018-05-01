---
title: 분산 트랜잭션에 대한 가용성 그룹 구성 | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: ''
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b6812a199583fee5cff0ce90c0a0e7f72f9b7645
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="configure-availability-group-for-distributed-transactions"></a>분산 트랜잭션에 대한 가용성 그룹 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)]은 가용성 그룹의 데이터베이스를 포함하여 모든 분산 트랜잭션을 지원합니다. 이 문서에서는 분산 트랜잭션에 대한 가용성 그룹을 구성하는 방법에 대해 설명합니다.  

분산 트랜잭션을 보장하려면 데이터베이스를 분산 트랜잭션 리소스 관리자로 등록하도록 가용성 그룹을 구성해야 합니다.  

>[!NOTE]
>[!INCLUDE[SQL2016](../../../includes/sssql15-md.md)]은 분산 트랜잭션도 지원하지만 [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)]의 지원은 제한적입니다. [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)]에서 동일한 서버에 둘 이상의 데이터베이스가 포함되어 있으면 가용성 그룹의 데이터베이스가 있는 분산 트랜잭션이 지원되지 않습니다. [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)]에는 이러한 제한이 없습니다. 
>
>[!INCLUDE[SQL2016](../../../includes/sssql15-md.md)]에서 구성하는 단계는 [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)]과 동일합니다.

분산 트랜잭션에서 클라이언트 응용 프로그램은 Microsoft Distributed Transaction Coordinator(MS DTC 또는 DTC)를 통해 여러 데이터 원본 간에 트랜잭션 일관성을 보장합니다. DTC는 지원되는 Windows Server 기반 운영 체제에서 사용할 수 있는 서비스입니다. 분산 트랜잭션의 경우 DTC는 *트랜잭션 코디네이터*입니다. 일반적으로 SQL Server 인스턴스는 *리소스 관리자*입니다. 데이터베이스가 가용성 그룹에 있는 경우 각 데이터베이스는 고유한 리소스 관리자여야 합니다. 

가용성 그룹이 분산 트랜잭션에 대해 구성되지 않은 경우에도 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)]는 가용성 그룹의 데이터베이스에 대한 분산 트랜잭션을 방지하지 않습니다. 그러나 가용성 그룹이 분산 트랜잭션에 대해 구성되지 않으면 일부 상황에서 장애 조치가 실패할 수 있습니다. 특히 새 주 복제본 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스는 DTC에서 트랜잭션 결과를 가져올 수 없습니다. 장애 조치 후 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스가 DTC에서 미결 트랜잭션의 결과를 얻도록 하려면 분산 트랜잭션에 대한 가용성 그룹을 구성합니다. 

## <a name="prerequisites"></a>사전 요구 사항

가용성 그룹에서 분산 트랜잭션을 지원하도록 구성하려면 먼저 다음 필수 조건을 충족해야 합니다.

* 분산 트랜잭션에 참여하는 모든 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스는 [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)] 이상이어야 합니다.

* Windows Server 2016 또는 Windows Server 2012 R2에서 가용성 그룹을 실행해야 합니다. Windows Server 2012 R2의 경우 [https://support.microsoft.com/en-us/kb/3090973](https://support.microsoft.com/en-us/kb/3090973)에서 제공되는 KB3090973의 업데이트를 설치해야 합니다.  

## <a name="create-an-availability-group-for-distributed-transactions"></a>분산 트랜잭션에 대한 가용성 그룹 만들기

분산 트랜잭션을 지원하도록 가용성 그룹을 구성합니다. 각 데이터베이스가 리소스 관리자로 등록할 수 있도록 가용성 그룹을 설정합니다. 이 문서에서는 각 데이터베이스가 DTC의 리소스 관리자가 될 수 있도록 가용성 그룹을 구성하는 방법에 대해 설명합니다.

[!INCLUDE[SQL2016](../../../includes/sssql15-md.md)] 이상에서 분산 트랜잭션에 대한 가용성 그룹을 만들 수 있습니다. 분산 트랜잭션에 대한 가용성 그룹을 만들려면 가용성 그룹 정의에 `DTC_SUPPORT = PER_DB`를 포함시킵니다. 다음 스크립트에서는 분산 트랜잭션에 대한 가용성 그룹을 만듭니다. 

```transact-sql
CREATE AVAILABILITY GROUP MyAG
   WITH (
      DTC_SUPPORT = PER_DB  
      )
   FOR DATABASE DB1, DB2
   REPLICA ON
      Server1 WITH (
         ENDPOINT_URL = 'TCP://SERVER1.corp.com:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         )
      Server2 WITH (
         ENDPOINT_URL = 'TCP://SERVER2.corp.com:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         )
```

>[!NOTE]
>앞의 스크립트는 가용성 그룹에 대한 간단한 예제이며 특정 프로덕션 환경을 위해 설계되지는 않았습니다. 

## <a name="alter-an-availability-group-for-distributed-transactions"></a>분산 트랜잭션에 대한 가용성 그룹 변경

[!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)] 이상에서 분산 트랜잭션의 가용성 그룹을 변경할 수 있습니다. 분산 트랜잭션의 가용성 그룹을 변경하려면 `ALTER AVAILABILITY GROUP` 스크립트에 `DTC_SUPPORT = PER_DB`를 포함시킵니다. 다음 예제 스크립트에서는 분산 트랜잭션을 지원하도록 가용성 그룹을 변경합니다. 

```transact-sql
ALTER AVAILABILITY GROUP MyaAG
   SET (
      DTC_SUPPORT = PER_DB  
      );
```

>[!NOTE]
>[!INCLUDE[SQL2016](../../../includes/sssql15-md.md)]에서는 분산 트랜잭션의 가용성 그룹을 변경할 수 없습니다. 설정을 변경하려면 해당 설정을 삭제하고 `DTC_SUPPORT = PER_DB` 설정으로 가용성 그룹을 다시 만듭니다. 

## <a name="a-namedisttrandistributed-transactions---technical-concepts"></a><a name="distTran"/> 분산 트랜잭션 - 기술 개념

분산 트랜잭션은 둘 이상의 데이터베이스에 걸쳐 있습니다. 트랜잭션 관리자로서 DTC는 SQL Server 인스턴스와 다른 데이터 원본 간의 트랜잭션을 조정합니다. [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 데이터베이스 엔진의 각 인스턴스는 리소스 관리자로 작동할 수 있습니다. 가용성 그룹이 `DTC_SUPPORT = PER_DB`로 구성되면 데이터베이스가 리소스 관리자로 작동할 수 있습니다. 자세한 내용은 MS DTC 설명서를 참조하십시오.

데이터베이스 엔진의 단일 인스턴스에서 둘 이상의 데이터베이스를 사용하는 트랜잭션은 실제로 분산 트랜잭션이 됩니다. 인스턴스는 분산 트랜잭션을 내부적으로 관리하므로 사용자에게는 로컬 트랜잭션처럼 작동합니다. 데이터베이스가 `DTC_SUPPORT = PER_DB`로 구성된 가용성 그룹에 있는 경우 [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)]은 SQL Server의 단일 인스턴스 내에서도 모든 데이터베이스 간 트랜잭션을 DTC로 승격합니다. 

응용 프로그램에서의 분산 트랜잭션 관리 방법은 로컬 트랜잭션과 많은 부분이 동일합니다. 트랜잭션이 끝나면 응용 프로그램이 트랜잭션을 커밋 또는 롤백하도록 요청합니다. 트랜잭션 관리자는 분산 커밋을 다른 방법으로 관리하여 일부 리소스 관리자는 성공적으로 커밋하고 일부는 트랜잭션을 롤백하는 네트워크 오류의 발생 가능성을 최소화해야 합니다. 이렇게 하려면 두 가지(준비 단계와 커밋 단계)에서 커밋 프로세스를 관리함으로써 달성됩니다. 이를 2단계 커밋이라고 합니다.

- **준비 단계**
   
   트랜잭션 관리자가 커밋 요청을 수신하면 트랜잭션과 관련된 모든 리소스 관리자에게 준비 명령을 보냅니다. 그런 다음 각 리소스 관리자는 트랜잭션을 지속적으로 만들고 트랜잭션에 대한 로그 이미지를 갖고 있는 버퍼를 디스크로 플러시하는 데 필요한 모든 작업을 수행합니다. 각 리소스 관리자가 준비 단계를 완료하면 준비 성공 또는 실패 여부를 트랜잭션 관리자에게 반환합니다.

- **커밋 단계**
   
   트랜잭션 관리자가 모든 리소스 관리자로부터 준비 성공 알림을 받으면 각 리소스 관리자에게 커밋 명령을 보냅니다. 그런 다음에는 리소스 관리자가 커밋을 완료할 수 있습니다. 모든 리소스 관리자가 성공적인 커밋을 보고하면 트랜잭션 관리자가 응용 프로그램에 성공을 알립니다. 준비 실패를 보고한 리소스 관리자가 있으면 트랜잭션 관리자가 각 리소스 관리자에게 롤백 명령을 보내서 응용 프로그램에게 커밋 실패를 알립니다.

### <a name="detailed-steps"></a>자세한 단계

다음 목록에서는 응용 프로그램이 DTC와 함께 작동하여 분산 트랜잭션을 완료하는 방법을 설명합니다.

1. SQL Server 인스턴스가 DTC 트랜잭션에 참여합니다. 이는 트랜잭션에 둘 이상의 리소스 관리자가 있거나 클라이언트에서 트랜잭션을 DTC 트랜잭션으로 승격하도록 요청한 경우에 발생할 수 있습니다.
2. 클라이언트는 DTC 트랜잭션 내에서 SQL Server 인스턴스의 일부 작업을 수행합니다.
3. 클라이언트에서 DTC 트랜잭션에 대한 커밋 또는 중단을 발급합니다.
    - 클라이언트에서 중단을 발급하면 트랜잭션이 즉시 중단됩니다.
    - 클라이언트에서 커밋을 발급하면 DTC에서는 트랜잭션의 모든 리소스 관리자에 트랜잭션을 준비하도록 요청하여 2단계 커밋 프로토콜을 시작합니다.
4. DTC는 모든 리소스 관리자가 준비 단계를 성공적으로 승인한 후에 트랜잭션을 커밋하도록 모든 리소스 관리자에 알립니다. 어떤 것이라도 성공적인 승인을 방해하는 경우 DTC에서 트랜잭션을 중단합니다. 

### <a name="effects-of-configuring-an-availability-group-for-distributed-transactions"></a>분산 트랜잭션에 대한 가용성 그룹 구성의 영향

분산 트랜잭션에 참여하는 각 엔터티를 리소스 관리자라고 합니다. 리소스 관리자의 예는 다음과 같습니다.

* [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스입니다. 
* 분산 트랜잭션에 대해 구성된 가용성 그룹의 데이터베이스
* DTC 서비스 - 트랜잭션 관리자일 수도 있습니다.
* 다른 데이터 원본 

분산 트랜잭션에 참여하기 위해 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스가 DTC에 등록됩니다. 일반적으로 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스는 로컬 서버의 DTC에 등록됩니다. 각 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스는 RMID(고유 리소스 관리자 식별자)가 있는 리소스 관리자를 만들고 이를 DTC에 등록합니다. 기본 구성에서 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스에 있는 모든 데이터베이스는 동일한 RMID를 사용합니다. 

데이터베이스가 가용성 그룹에 있으면 데이터베이스(또는 주 복제본)의 읽기-쓰기 복사본이 다른 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스로 이동할 수 있습니다. 이러한 이동 중에 분산 트랜잭션을 지원하려면 각 데이터베이스가 별도의 리소스 관리자로 작동해야 하며 고유한 RMID가 있어야 합니다. 가용성 그룹에 `DTC_SUPPORT = PER_DB`가 있으면 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)]에서 각 데이터베이스에 대한 리소스 관리자를 만들고 고유한 RMID를 사용하여 DTC에 등록합니다. 이 구성에서 데이터베이스는 DTC 트랜잭션에 대한 리소스 관리자입니다.

[!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)]의 분산 트랜잭션에 대한 자세한 내용은 [분산 트랜잭션](#distTran)을 참조하세요.

## <a name="manage-unresolved-transactions"></a>해결되지 않은 트랜잭션 관리

RMID 변경 중에 존재하는 활성 트랜잭션의 결과는 장애 조치 후에 복구할 수 없습니다. 이는 등록하는 데 사용된 RMID SQL Server와 복구하는 데 사용된 RMID가 다르기 때문입니다. 다음과 같은 경우에 RMID 변경이 발생할 수 있습니다.

* 가용성 그룹에 대해 `DTC_SUPPORT`를 변경합니다. 
* 가용성 그룹에서 데이터베이스를 추가 또는 제거합니다. 
* 가용성 그룹을 삭제합니다.

이러한 경우 주 복제본에서 새 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스로 장애 조치를 수행하면 인스턴스에서 DTC에 연결하여 트랜잭션 결과를 확인하려고 시도합니다. 복구 중에 미결 트랜잭션에 대한 결과를 얻기 위해 데이터베이스에서 사용하고 있는 RMID가 이전에 등록되지 않았기 때문에 DTC에서 결과를 반환할 수 없습니다. 따라서 데이터베이스가 SUSPECT(주의 대상) 상태가 됩니다.

새로운 [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 오류 로그에는 다음 예제와 같은 항목이 있습니다.

```
Microsoft Distributed Transaction Coordinator (MS DTC) 
failed to reenlist citing that the database RMID does 
not match the RMID [xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx] 
associated with the transaction.  Please manually resolve
the transaction.
    
SQL Server detected a DTC/KTM in-doubt transaction with UOW 
{yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy}.Please resolve it 
following the guideline for Troubleshooting DTC Transactions.
```

앞의 예제에서는 DTC가 장애 조치 후에 만들어진 트랜잭션의 새 주 복제본에서 데이터베이스를 다시 등록할 수 없음을 보여 줍니다. [!INCLUDE[SQLServer](../../../includes/ssnoversion_md.md)] 인스턴스는 분산 트랜잭션의 결과를 확인할 수 없으므로 데이터베이스를 주의 대상으로 표시합니다. 트랜잭션은 UOW(작업 단위)로 표시되고 GUID로 참조됩니다. 데이터베이스를 복구하려면 수동으로 트랜잭션을 커밋하거나 롤백합니다. 

>[!WARNING]
>트랜잭션을 수동으로 커밋하거나 롤백하면 응용 프로그램에 영향을 줄 수 있습니다. 커밋 또는 롤백 동작이 응용 프로그램 요구 사항과 일치하는지 확인합니다. 

다음 스크립트 중 하나만 실행합니다.

   * 트랜잭션을 커밋하려면 다음 스크립트를 업데이트하고 실행합니다. `yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy`를 이전 오류 메시지의 미결 트랜잭션 UOW로 바꾸고 다음을 실행합니다.

      ```transact-sql
      KILL 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy' WITH COMMIT
      ```

   * 트랜잭션을 롤백하려면 다음 스크립트를 갱신하고 실행합니다. `yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy`를 이전 오류 메시지의 미결 트랜잭션 UOW로 바꾸고 다음을 실행합니다.

      ```transact-sql
      KILL 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy' WITH ROLLBACK
     ```

트랜잭션을 커밋하거나 롤백한 후에는 `ALTER DATABASE`를 사용하여 데이터베이스를 온라인으로 설정할 수 있습니다. 다음 스크립트를 업데이트하고 실행합니다. - 주의 상태 데이터베이스의 이름에 대한 데이터베이스 이름을 설정합니다.

   ```transact-sql
   ALTER DATABASE [DB1] SET ONLINE
   ```

미결 트랜잭션을 해결하는 방법에 대한 자세한 내용은 [수동으로 트랜잭션 해결(영문)](http://technet.microsoft.com/library/cc754134.aspx)을 참조하세요.

## <a name="next-steps"></a>Next Steps  

[분산 트랜잭션](http://docs.microsoft.com/dotnet/framework/data/adonet/distributed-transactions)

[Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
[트랜잭션 - Always On 가용성 그룹 및 데이터베이스 미러링](transactions-always-on-availability-and-database-mirroring.md)  

[XA 트랜잭션 지원(영문)](http://technet.microsoft.com/library/cc753563(v=ws.10).aspx)

[작동 방법: DTC 트랜잭션에 대한 세션/SPID (-2)(영문)](http://blogs.msdn.microsoft.com/bobsql/2016/08/04/how-it-works-sessionspid-2-for-dtc-transactions/)
