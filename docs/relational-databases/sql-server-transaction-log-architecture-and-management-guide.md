---
title: SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드 | Microsoft 문서
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction log architecture guide
- guide, transaction log architecture
- vlf
- transaction log guidance
- vlfs
- virtual log files
- virtual log size
- vlf size
- transaction log internals
ms.assetid: 88b22f65-ee01-459c-8800-bcf052df958a
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7444659676f6f8270b5cc8013c872e492e0cd8c8
ms.sourcegitcommit: e7c3c4877798c264a98ae8d51d51cb678baf5ee9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916064"
---
# <a name="sql-server-transaction-log-architecture-and-management-guide"></a>SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  각 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에는 각 트랜잭션에 의해 적용된 모든 트랜잭션 및 데이터베이스 수정 내용을 기록하는 트랜잭션 로그가 있습니다. 트랜잭션 로그는 데이터베이스의 주요 구성 요소이며 시스템 오류가 발생할 경우 데이터베이스를 다시 일관된 상태로 만들려면 트랜잭션 로그가 필요할 수 있습니다. 이 지침에서는 트랜잭션 로그의 물리적 및 논리적 아키텍처에 대한 정보를 제공합니다. 아키텍처를 이해하면 트랜잭션 로그를 보다 효율적으로 관리할 수 있습니다.  

  
##  <a name="Logical_Arch"></a> 트랜잭션 로그 논리 아키텍처  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 트랜잭션 로그는 로그 레코드 문자열처럼 논리적으로 작동합니다. 각 로그 레코드는 LSN(로그 시퀀스 번호)으로 식별됩니다. 각 새 로그 레코드는 LSN과 함께 로그의 논리적 끝에 작성되며 이때 LSN은 오름차순입니다. 로그 레코드는 만들어진 순서에 따라 순차적으로 저장됩니다. 예를 들어 LSN2가 LSN1보다 큰 경우 로그 레코드 LSN1에 해당하는 변경이 먼저 발생하고 로그 레코드 LSN2에 해당하는 변경이 이후에 발생한 것입니다. 각 로그 레코드에는 자신이 속한 트랜잭션의 ID가 포함됩니다. 각 트랜잭션에서 트랜잭션과 관련된 모든 로그 레코드는 트랜잭션의 롤백 속도를 높이는 후방 포인터로 체인에 개별적으로 연결되어 있습니다.  
  
 데이터 수정에 대한 로그 레코드는 수행된 논리적 연산이나 수정된 데이터의 이전 이미지와 이후 이미지를 기록합니다. 이전 이미지는 연산이 수행되기 전의 데이터 복사본이고 이후 이미지는 연산이 수행된 후의 데이터 복사본입니다.  
  
연산을 복구하는 단계는 다음과 같이 로그 레코드의 유형에 따라 다릅니다.  
  
-   기록된 논리적 연산  
  
    -   논리적 연산을 롤포워드하기 위해 해당 연산이 다시 수행됩니다.  
  
    -   논리적 연산을 롤백하기 위해 역 논리적 연산이 수행됩니다.  
  
-   기록된 이전 및 이후 이미지  
  
    -   연산을 롤포워드하기 위해 이후 이미지가 적용됩니다.  
  
    -   연산을 롤백하기 위해 이전 이미지가 적용됩니다.  
  
많은 유형의 작업이 트랜잭션 로그에 기록됩니다. 다음과 같은 작업이 여기에 포함됩니다.  
  
-   각 트랜잭션의 시작과 끝  
  
-   모든 데이터 수정 내용(삽입, 업데이트 또는 삭제). 여기에는 시스템 테이블을 비롯하여 모든 테이블에 대해 시스템 저장 프로시저 또는 DDL(데이터 정의 언어) 문에서 수행한 변경 내용이 포함됩니다.  
  
-   모든 익스텐트 및 페이지 할당 또는 할당 취소  
  
-   테이블이나 인덱스 만들기 또는 삭제  
  
 롤백 작업도 기록됩니다. 각 트랜잭션은 트랜잭션 로그에 공간을 예약하여 명시적 롤백 문이나 오류로 인해 발생한 롤백을 지원하기에 충분한 로그 공간을 확보합니다. 예약된 공간의 크기는 트랜잭션에서 수행되는 작업에 따라 다르지만 일반적으로 각 작업을 기록하는 데 사용되는 공간의 크기와 같습니다. 이렇게 예약된 공간은 트랜잭션 완료 시 해제됩니다.  
  
<a name="minlsn"></a>마지막으로 작성된 로그 레코드로의 성공적인 데이터베이스 차원의 롤백에 필요한 첫 번째 로그 레코드의 로그 파일 섹션을 로그의 활성 부분, *활성 로그* 또는 *비상 로그*라고 합니다. 로그의 이 섹션은 데이터베이스의 전체 [복구](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)를 수행하는 데 필요합니다. 활성 로그는 어떤 부분도 잘라낼 수 없습니다. 이 첫 번째 로그 레코드의 LSN(로그 시퀀스 번호)은 **최소 복구 LSN(*MinLSN*)** 이라고 합니다. 트랜잭션 로그에서 지원되는 작업에 대한 자세한 내용은 [트랜잭션 로그(SQL Server)](../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.  

차등 및 로그 백업의 경우 데이터베이스는 보다 나중의 것으로 복원되며 이는 더 높은 LSN에 해당합니다. 
  
##  <a name="physical_arch"></a> 트랜잭션 로그 물리 아키텍처  
데이터베이스의 트랜잭션 로그는 하나 이상의 물리 파일에 매핑됩니다. 개념상으로 로그 파일은 로그 레코드의 문자열입니다. 실제로 로그 레코드의 시퀀스는 트랜잭션 로그를 구현하는 물리적 파일 집합에 효율적으로 저장됩니다. 데이터베이스마다 최소한 하나의 로그 파일이 있어야 합니다.  
  
[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 내부적으로 각 물리적 로그 파일을 여러 개의 VLF(가상 로그 파일)로 나눕니다. 가상 로그 파일의 크기는 고정되어 있지 않으며 물리 로그 파일에 대해 고정된 수의 가상 로그 파일이 있는 것도 아닙니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 로그 파일을 만들거나 확장할 때 동적으로 가상 로그 파일의 크기를 선택합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 적은 수의 가상 파일을 유지하려고 합니다. 로그 파일 확장 후 가상 파일 크기는 기존 로그 크기와 새 파일 증가 크기를 합한 크기입니다. 관리자가 가상 로그 파일의 크기 또는 수를 구성하거나 설정할 수 없습니다.  

> [!NOTE]
> 가상 로그 파일(VLF) 생성은 이 메서드를 따릅니다.
> - 다음 증가가 현재 로그의 물리적 크기의 1/8보다 작은 경우 증가 크기에 충분한 VLF를 하나 만듭니다([!INCLUDE[ssSQL14](../includes/sssql14-md.md)]로 시작).
> - 다음 증가 현재 로그 크기의 1/8보다 많을 경우 pre-2014 메서드를 사용합니다.
>    -  증가가 64MB보다 작은 경우 증가 크기에 충분한 4개의 VLF를 만듭니다(예: 1MB 증가의 경우 256KB VLF 4개 생성).
>    -  증가가 64MB에서 최대 1GB인 경우 증가 크기에 충분한 8개의 VLF를 만듭니다(예: 512MB 증가의 경우 64MB VLF 8개 생성).
>    -  증가가 1GB보다 큰 경우 증가 크기에 충분한 16개의 VLF를 만듭니다(예: 8GB 증가의 경우 512MB VLF 16개 생성).

수많은 작은 증가값에서 로그 파일이 크게 증가하는 경우 가상 로그 파일이 많이 생성됩니다. **이로 인해 데이터베이스 시작뿐 아니라 로그 백업 및 복원 작업이 느려질 수 있습니다.** 반대로 로그 파일이 적거나 하나의 증분인 큰 크기로 설정된 경우 적은 수의 매우 큰 가상 로그 파일이 포함됩니다. 트랜잭션 로그의 **필수 크기** 및 **자동 증가** 설정을 올바르게 예측하는 방법에 대한 자세한 내용은 [트랜잭션 로그 파일의 크기 관리](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations) 중 *권장 사항* 섹션을 참조하세요.

최적의 VLF 배포를 수행하기 위한 필수 증분을 사용하여 필요한 최종 크기에 가까운 *크기* 값을 로그 파일에 할당하고 *growth_increment* 값을 비교적 크게 지정하는 것이 좋습니다. 현재 트랜잭션 로그 크기에 대해 최적의 VLF 분포를 결정하려면 아래 팁을 참조하세요. 
 - `ALTER DATABASE`의 `SIZE` 인수로 설정된 *크기* 값은 로그 파일의 초기 크기입니다.
 - *growth_increment* 값(자동 증가 값이라고도 함)은 `ALTER DATABASE`의 `FILEGROWTH` 인수로 설정된 대로 새로운 공간이 필요할 때마다 파일에 추가되는 공간입니다. 
 
`ALTER DATABASE`의 `FILEGROWTH` 및 `SIZE` 인수에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41; 파일 및 파일 그룹 옵션](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.

> [!TIP]
> 주어진 인스턴스의 모든 데이터베이스의 현재 트랜잭션 로그 크기에 대한 최적의 VLF 분포 및 필수 크기를 수행할 필수 성장 증분을 결정하려면 이 [스크립트](https://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)를 참조하세요.
  
 트랜잭션 로그는 순환 파일입니다. 예를 들어 데이터베이스에 4개의 VLF로 나뉜 물리 로그 파일이 한 개 있다고 가정합니다. 이 데이터베이스가 생성될 때 물리 로그 파일의 시작 부분에서 논리 로그 파일이 시작됩니다. 새 로그 레코드는 논리 로그의 끝 부분에 추가되며 물리 로그의 끝 방향으로 확장됩니다. 로그 잘림을 수행하면 모든 레코드가 MinLSN(최소 복구 로그 시퀀스 번호) 앞에 있는 가상 로그에 대한 공간이 확보됩니다. *MinLSN* 은 성공적인 데이터베이스 차원의 롤백에 필요한 가장 오래된 로그 레코드의 로그 시퀀스 번호입니다. 예제 데이터베이스의 트랜잭션 로그는 다음 그림의 로그와 유사합니다.  
  
 ![tranlog3](../relational-databases/media/tranlog3.gif)  
  
 논리 로그의 끝 부분이 물리 로그 파일의 끝 부분에 도달하면 새 로그 레코드는 물리 로그 파일의 시작 부분으로 순환됩니다.  
  
![tranlog4](../relational-databases/media/tranlog4.gif)   
  
 이러한 순환은 논리 로그 끝 부분이 논리 로그의 시작 부분에 도달하지 않는 한 계속 반복됩니다. 다음 검사점까지 생성되는 모든 새 로그 레코드를 위해 항상 충분한 공간이 남을 만큼 기존 로그 레코드가 자주 잘리면 로그는 가득 차지 않습니다. 그러나 논리 로그의 끝 부분이 논리 로그의 시작 부분에 도달하면 다음 두 가지 상황 중 하나가 발생합니다.  
  
-   로그에 대해 `FILEGROWTH` 설정이 사용하도록 설정되어 있고 디스크에 사용할 수 있는 공간이 있으면 파일은 *growth_increment* 매개 변수에 지정된 크기만큼 확장되며 새 로그 레코드가 확장 부분에 추가됩니다. `FILEGROWTH` 설정에 대한 자세한 내용은 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.  
  
-   `FILEGROWTH` 설정이 사용하도록 설정되어 있지 않거나 로그 파일이 있는 디스크의 사용 가능한 공간이 *growth_increment*에 지정된 크기보다 적으면 9002 오류가 발생합니다. 자세한 정보는 [전체 트랜잭션 로그 문제 해결](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)을 참조하세요.  
  
 로그에 물리 로그 파일이 여러 개 있으면 논리 로그는 모든 물리 로그 파일을 거친 후 첫 번째 물리 로그 파일의 시작 부분으로 순환됩니다. 
 
> [!IMPORTANT]
> 트랜잭션 로그 크기 관리에 대한 자세한 내용은 [트랜잭션 로그 파일의 크기 관리](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)를 참조하세요.
  
### <a name="log-truncation"></a>로그 잘림  
 로그가 가득 차지 않도록 하기 위해 로그 잘림은 필수적입니다. 로그 잘림은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 논리 트랜잭션 로그에서 비활성 가상 로그 파일을 삭제하여 물리적 트랜잭션 로그에서 다시 사용할 수 있도록 논리 로그의 공간을 확보합니다. 트랜잭션 로그가 잘리지 않으면 물리적 로그 파일에 할당된 디스크 공간이 모두 트랜잭션 로그로 채워지게 됩니다. 단, 로그를 자르기 전에 검사점 작업을 수행해야 합니다. 검사점은 현재 메모리 내의 수정된 페이지(더티 페이지라고 함)와 메모리의 트랜잭션 로그 정보를 디스크에 기록합니다. 검사점을 수행하면 트랜잭션 로그의 비활성 부분은 재사용 가능으로 표시됩니다. 그런 후에는 로그 잘림으로 비활성 부분에 대한 공간을 확보할 수 있습니다. 검사점에 대한 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.  
  
 다음 그림에서는 잘림 전과 후의 트랜잭션 로그를 보여 줍니다. 첫 번째 그림은 잘림이 수행되지 않은 트랜잭션 로그를 보여 줍니다. 현재 논리 로그에서 4개의 가상 로그 파일을 사용하고 있습니다. 논리 로그는 첫 번째 가상 로그 파일의 앞에서 시작하고 가상 로그 4에서 끝납니다. MinLSN 레코드는 가상 로그 3에 있습니다. 가상 로그 1과 가상 로그 2에는 비활성 로그 레코드만 포함되어 있습니다. 이러한 레코드는 자를 수 있습니다. 가상 로그 5는 사용하지 않았으며 현재 논리 로그에 포함되지 않습니다.  
  
![tranlog2](../relational-databases/media/tranlog2.gif)  
  
 두 번째 그림은 잘림 후의 로그 모습을 보여 줍니다. 가상 로그 1과 가상 로그 2는 다시 사용할 수 있도록 공간이 확보되었습니다. 이제 논리 로그는 가상 로그 3의 시작 부분에서 시작됩니다. 가상 로그 5는 아직 사용되지 않았으며 현재 논리 로그에 포함되지 않습니다.  
  
![tranlog3](../relational-databases/media/tranlog3.gif)  
  
 여타의 이유로 지연된 경우를 제외하고 로그 잘림은 다음과 같이 자동으로 발생합니다.  
  
-   단순 복구 모델에서는 검사점 이후 잘림이 수행됩니다.  
-   전체 복구 모델 또는 대량 로그 복구 모델에서 로그 백업 후(이전 백업 이후에 발생한 검사점이 있는 경우).  
  
 여러 요소로 인해 로그 잘림이 지연될 수 있습니다. 로그 잘림이 장시간 지연될 경우 트랜잭션 로그가 꽉 찰 수 있습니다. 자세한 내용은 [로그 잘림을 지연시킬 수 있는 요소](../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation) 및 [꽉 찬 트랜잭션 로그 문제 해결&#40;SQL Server 오류 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)을 참조하세요.  
  
##  <a name="WAL"></a> 미리 쓰기 트랜잭션 로그  
 이 섹션에서는 데이터 수정 내용을 디스크에 기록할 때 미리 쓰기 트랜잭션 로그의 역할에 대해 설명합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 WAL(미리 쓰기 로그)을 사용하여 연결된 로그 레코드가 디스크에 기록되기 전에는 어떠한 데이터 수정 내용도 디스크에 기록되지 않도록 합니다. 따라서 트랜잭션의 ACID 속성이 유지 관리됩니다.  
  
 미리 쓰기 로그 작동 방식을 이해하려면 수정된 데이터가 디스크에 기록되는 방법을 알아야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 데이터를 검색해야 할 때 데이터 페이지를 읽어오는 버퍼 캐시를 유지 관리합니다. 페이지가 버퍼 캐시에서 수정될 때 페이지는 디스크에 바로 다시 기록되지 않고 대신 *더티*로 표시됩니다. 데이터 페이지는 물리적으로 디스크에 기록되기 전에 두 개 이상의 논리적 쓰기를 수행할 수 있습니다. 각 논리적 쓰기의 경우 트랜잭션 로그 레코드는 수정 사항을 기록하는 로그 캐시에 삽입됩니다. 로그 레코드는 관련된 더티 페이지가 버퍼 캐시에서 디스크로 제거되기 전에 디스크에 기록되어야 합니다. 검사점 프로세스는 주기적으로 버퍼 캐시에서 지정된 특정 데이터베이스의 페이지를 포함하는 버퍼를 검색한 다음 모든 더티 페이지를 디스크에 기록합니다. 검사점은 모든 더티 페이지가 디스크에 기록되었음을 확인하는 지점을 만들어 나중에 복구하는 동안 시간을 절약할 수 있습니다.  
  
 버퍼 캐시에 있는 수정된 데이터 페이지를 디스크에 쓰는 작업을 페이지 플러시라고 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에는 연결된 로그 레코드가 기록되기 전에 더티 페이지가 플러시되지 않도록 하는 논리가 있습니다. 로그 레코드는 로그 버퍼가 플러시되면 디스크에 기록됩니다.  이는 트랜잭션이 커밋되거나 로그 버퍼가 가득 찰 때마다 발생합니다.  
  
##  <a name="Backups"></a> 트랜잭션 로그 백업  
 이 섹션에서는 트랜잭션 로그를 백업 및 복원하거나 적용하는 방법에 대한 개념을 설명합니다. 전체 및 대량 로그 복원 모델에서 데이터를 복구하려면 트랜잭션 로그를 정기적으로 백업(*로그 백업*)해야 합니다. 전체 백업이 실행되는 동안 로그를 백업할 수 있습니다. 복구 모델에 대한 자세한 내용은 [SQL Server 데이터베이스 백업 및 복원](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하세요.  
  
 첫 번째 로그 백업을 만들기 전에 데이터베이스 백업 또는 파일 백업 집합의 첫 번째 집합과 같은 전체 백업을 만들어야 합니다. 파일 백업만 사용하여 데이터베이스를 복원하면 복잡해질 수 있습니다. 따라서 가능하면 처음에 전체 데이터베이스 백업을 수행하는 것이 좋습니다. 그런 후에 트랜잭션 로그를 정기적으로 백업할 수 있습니다. 이렇게 하면 작업 손실 위험이 최소화될 뿐만 아니라 트랜잭션 로그가 잘립니다. 일반적으로 기존 로그 백업 후에도 트랜잭션 로그가 잘리지만  
  
> [!IMPORTANT]
> 비즈니스 요구 사항, 특히 손상된 로그 스토리지에 의해 발생될 수 있는 작업 손실에 대한 허용 범위를 지원하기 위해 로그 백업을 충분히 자주 수행하는 것이 좋습니다. 로그 백업의 적절한 수행 빈도는 저장 및 관리는 물론 복원까지 가능할 수 있는 로그 백업의 횟수에 의해 조정되는 작업 손실 위험에 대한 허용 범위에 따라 달라집니다. 복구 전략을 구현할 때 필요한 [RTO](https://wikipedia.org/wiki/Recovery_time_objective) 및 [RPO](https://wikipedia.org/wiki/Recovery_point_objective), 특히 로그 백업 케이던스에 대해 생각해보세요.
> 로그 백업에 걸리는 시간은 매 15분에서 30분이면 충분합니다. 비즈니스에서 작업 손실 위험을 최소화하려는 경우에는 로그 백업을 더 자주 수행해야 합니다. 로그 백업 횟수가 많아지면 로그 잘림이 더 자주 발생하여 로그 파일의 크기가 작아지는 이점이 있습니다.  
  
> [!IMPORTANT]
> 복원해야 하는 로그 백업의 수를 제한하려면 데이터를 정기적으로 백업해야 합니다. 예를 들어 주별 전체 데이터베이스 백업과 일별 차등 데이터베이스 백업을 예약할 수 있습니다.  
> 또 복구 전략을 구현할 때 필요한 [RTO](https://wikipedia.org/wiki/Recovery_time_objective) 및 [RPO](https://wikipedia.org/wiki/Recovery_point_objective), 특히 전체 및 차등 데이터베이스 백업 케이던스에 대해 생각해보세요.

트랜잭션 로그 백업에 대한 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md)을 참조하세요.
  
### <a name="the-log-chain"></a>로그 체인  
 로그 백업의 연속 시퀀스를 *로그 체인*이라고 합니다. 로그 체인은 데이터베이스의 전체 백업으로 시작합니다. 일반적으로 데이터베이스를 처음 백업할 때나 단순 복구 모델에서 전체 또는 대량 로그 복구 모델로 전환한 후에만 새 로그 체인이 시작됩니다. 전체 데이터베이스 백업을 만들 때 기존 백업 집합을 덮어쓰도록 선택하지 않으면 기존 로그 체인이 그대로 유지됩니다. 로그 체인이 그대로 유지되면 미디어 세트의 전체 데이터베이스 백업에서 데이터베이스를 복원한 후 모든 후속 로그 백업을 복구 지점까지 복원할 수 있습니다. 복구 지점은 마지막 로그 백업의 끝이나 로그 백업의 특정 복구 지점일 수 있습니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md)을 참조하세요.  
  
 데이터베이스를 오류 발생 시점까지 복원하려면 로그 체인이 온전해야 합니다. 즉 트랜잭션 로그 백업의 연속적인 시퀀스가 오류 발생 지점까지 이어져야 합니다. 이 로그 시퀀스가 시작되는 위치는 복원 중인 데이터 백업의 유형인 데이터베이스, 부분 또는 파일에 따라 달라집니다. 데이터베이스 또는 부분 백업의 경우 로그 백업의 시퀀스는 데이터베이스 또는 부분 백업의 끝 지점에서 이어져야 합니다. 파일 백업 집합의 경우 로그 백업의 시퀀스는 전체 파일 백업 집합의 시작 지점에서 이어져야 합니다. 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
### <a name="restore-log-backups"></a>로그 백업을 복원하려면  
 로그 백업을 복원하면 현재 데이터베이스를 로그 백업 작업이 시작된 시점의 데이터베이스 상태와 정확히 일치하도록 다시 만들기 위해 트랜잭션 로그에 기록된 변경 내용을 롤포워드합니다. 데이터베이스를 복원하는 경우 복원하는 전체 데이터베이스 백업 이후 또는 복원하는 첫 번째 파일 백업의 시작 부분에서 만든 로그 백업을 복원해야 합니다. 일반적으로 가장 최근의 데이터나 차등 백업을 복원하고 나면 복구 지점에 이를 때까지 일련의 로그 백업을 복원한 다음 데이터베이스를 복구해야 합니다. 이때까지 완료되지 않은 트랜잭션은 모두 롤백되며 복구가 완료되면 데이터베이스는 온라인 상태가 됩니다. 데이터베이스가 복구된 후에는 더 이상의 백업을 복원할 수 없습니다. 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  

## <a name="checkpoints-and-the-active-portion-of-the-log"></a>검사점 및 로그의 활성 부분  

검사점은 현재 데이터베이스의 버퍼 캐시에 있는 커밋되지 않은 데이터 페이지를 디스크로 플러시합니다. 따라서 데이터베이스의 전체 복구 중에 처리되어야 하는 로그의 활성 부분이 최소화됩니다. 전체 복구 동안 다음 유형의 동작이 수행됩니다.

* 시스템이 중지되기 전에 디스크로 플러시되지 않은 로그의 수정 레코드가 롤포워드됩니다.
* 커밋 또는 롤백 로그 레코드가 없는 불완전한 트랜잭션과 관련된 모든 수정 내용이 롤백됩니다.

### <a name="checkpoint-operation"></a>검사점 작업

데이터베이스에서 검사점이 수행하는 프로세스는 다음과 같습니다.

* 검사점의 시작을 표시하는 레코드를 로그 파일에 기록합니다.
* 검사점 로그 레코드의 체인에 검사점에 대해 기록된 정보를 저장합니다.  
 
    검사점에 기록되는 한 가지 정보는 성공적인 데이터베이스 차원의 롤백을 위해 반드시 있어야 하는 첫 번째 로그 레코드의 LSN(로그 시퀀스 번호)입니다. 이 LSN을 최소 복구 LSN(MinLSN)이라고 합니다. MinLSN은 다음의 최소값입니다. 

    * 검사점 시작의 LSN
    * 가장 오래된 활성 트랜잭션 시작의 LSN
    * 아직 배포 데이터베이스로 전달되지 않은 가장 오래된 복제 트랜잭션 시작의 LSN 

    또한 검사점 레코드에는 데이터베이스를 수정한 모든 활성 트랜잭션 목록이 포함됩니다.

* 데이터베이스에서 단순 복구 모델을 사용하는 경우 MinLSN 앞에 나오는 공간을 재사용 가능으로 표시합니다. 
* 커밋되지 않은 모든 로그와 데이터 페이지를 디스크에 씁니다.
* 검사점의 끝을 표시하는 레코드를 로그 파일에 씁니다.
* 이 체인의 시작 LSN을 데이터베이스 부팅 페이지에 씁니다.

#### <a name="activities-that-cause-a-checkpoint"></a>검사점을 발생시키는 작업

검사점은 다음과 같은 상황에서 발생합니다.

* CHECKPOINT 문이 명시적으로 실행된 경우. 현재 연결된 데이터베이스에서 검사점이 발생합니다.
* 데이터베이스에서 최소 로그 작업이 수행된 경우(예: 대량 로그 복구 모델을 사용하는 데이터베이스에서 대량 복사 작업이 수행된 경우) 
* ALTER DATABASE를 사용하여 데이터베이스 파일을 추가 또는 제거한 경우
* SHUTDOWN 문을 사용하거나 SQL Server(MSSQLSERVER) 서비스를 중지하여 SQL Server 인스턴스를 중지한 경우. 두 동작은 모두 SQL Server 인스턴스의 각 데이터베이스에 검사점을 설정합니다.
* SQL Server 인스턴스가 데이터베이스를 복구하는 데 걸리는 시간을 줄이기 위해 각 데이터베이스에서 자동 검사점을 주기적으로 생성하는 경우
* 데이터베이스를 백업한 경우
* 데이터베이스를 종료해야 하는 작업을 수행한 경우. AUTO_CLOSE가 ON이고 데이터베이스에 대한 마지막 사용자 연결이 닫힌 경우 또는 데이터베이스를 다시 시작해야 하는 데이터베이스 옵션 변경을 수행한 경우를 예로 들 수 있습니다.

### <a name="automatic-checkpoints"></a>자동 검사점

SQL Server 데이터베이스 엔진은 자동 검사점을 생성합니다. 자동 검사점 간의 간격은 마지막 검사점 이후 경과된 시간과 사용된 로그 공간에 따라 결정됩니다. 데이터베이스가 거의 수정되지 않을 경우에는 자동 검사점 간의 시간 간격이 가변적이고 길어질 수 있습니다. 또한 많은 데이터를 수정할 경우에는 자동 검사점이 자주 발생할 수 있습니다.

**복구 간격** 서버 구성 옵션을 사용하여 서버 인스턴스의 모든 데이터베이스에 대한 자동 검사점 간 간격을 계산할 수 있습니다. 이 옵션은 시스템을 다시 시작하는 동안 데이터베이스 엔진이 데이터베이스를 복구하는 데 사용하는 최대 시간을 지정합니다. 데이터베에스 엔진은 복구 작업 중에 해당 **복구 간격** 동안 처리할 수 있는 로그 레코드의 수를 예상합니다. 

자동 검사점 간의 간격은 복구 모델에 따라서도 달라집니다.

* 전체 또는 대량 로그 복구 모델을 사용하는 데이터베이스의 경우 로그 레코드의 수가 데이터베이스 엔진에서 복구 간격 옵션에 지정된 시간 동안 처리할 수 있다고 예상한 레코드의 수에 도달할 때마다 자동 검사점이 생성됩니다.
* 단순 복구 모델을 사용하는 데이터베이스의 경우 로그 레코드의 수가 다음의 두 값 중에서 작은 값에 도달할 때마다 자동 검사점이 생성됩니다. 

    * 로그의 70%가 찼을 때
    * 로그 레코드의 수가 데이터베이스 엔진에서 복구 간격 옵션에 지정된 시간 동안 처리할 수 있다고 예상한 수에 도달했을 때

복구 간격 설정에 대한 자세한 내용은 [복구 간격 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)을 참조하세요.

> [!TIP]  
> 데이터베이스 관리자는 일부 유형의 검사점에 대해 -k SQL Server 고급 설정 옵션을 사용하여 I/O 하위 시스템의 처리량에 따라 검사점 I/O 동작을 제한할 수 있습니다. -k 설정 옵션은 자동 검사점과 그 밖의 제한되지 않는 모든 검사점에 적용됩니다. 
 
자동 검사점은 데이터베이스가 단순 복구 모델을 사용하고 있을 때 트랜잭션 로그의 사용되지 않는 부분을 자릅니다. 그러나 데이터베이스가 전체 또는 대량 로그 복구 모델을 사용하고 있을 때는 자동 검사점에서 이러한 로그를 자르지 않습니다. 자세한 내용은 [트랜잭션 로그](../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요. 

이제 CHECKPOINT 문에서는 검사점을 완료하는 요청 시간(초)을 지정하는 선택적 checkpoint_duration 인수를 제공합니다. 자세한 내용은 [CHECKPOINT](../t-sql/language-elements/checkpoint-transact-sql.md)를 참조하세요.

### <a name="active-log"></a>활성 로그

MinLSN에서 마지막으로 쓰여진 로그 레코드까지의 로그 파일 섹션을 로그의 활성 부분 또는 활성 로그라고 합니다. 로그의 이 섹션은 데이터베이스의 전체 복구를 수행하는 데 필요합니다. 활성 로그는 어떤 부분도 잘라낼 수 없습니다. 모든 로그 레코드는 로그의 MinLSN 앞에서 잘라야 합니다.

다음 그림에서는 두 개의 활성 트랜잭션이 있는 트랜잭션 로그 끝의 단순화된 버전을 보여 줍니다. 검사점 레코드는 단일 레코드로 압축되었습니다.

![active_log](../relational-databases/media/active-log.gif) 

LSN 148은 트랜잭션 로그의 마지막 레코드입니다. LSN 147에 기록된 검사점이 처리되면 Tran 1이 커밋되고 Tran 2만 유일한 활성 트랜잭션이 됩니다. 이 경우 Tran 2에 대한 첫 번째 로그 레코드가 마지막 검사점에서 활성 상태인 트랜잭션에 대한 가장 오래된 로그 레코드가 됩니다. 따라서 Tran 2에 대한 Begin Transaction 레코드인 LSN 142가 MinLSN이 됩니다.

### <a name="long-running-transactions"></a>장기 실행 트랜잭션
활성 로그에는 커밋되지 않은 모든 트랜잭션의 모든 부분이 포함되어야 합니다. 트랜잭션을 시작했으나 커밋하거나 롤백하지 않은 애플리케이션이 있으면 [!INCLUDE[ssde_md](../includes/ssde_md.md)]이 MinLSN을 앞당기지 못하게 됩니다. 이로 인해 다음 두 가지 유형의 문제가 발생할 수 있습니다.

* 트랜잭션이 커밋되지 않은 많은 수정 작업을 수행한 후에 시스템이 종료되면 시스템이 다시 시작된 후의 복구 단계 수행 시 **복구 간격** 옵션에 지정된 시간보다 훨씬 더 오래 걸릴 수 있습니다.
* 로그가 MinLSN을 통과하여 잘릴 수 없으므로 너무 커질 수 있습니다. 이러한 문제는 트랜잭션 로그가 각 자동 검사점에서 일반적으로 잘리게 되는 단순 복구 모델을 데이터베이스에서 사용하는 경우에도 발생합니다.

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]부터 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]에서 [가속 데이터베이스 복구](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)를 사용하여 장기 실행 트랜잭션의 복구와 위에 설명된 문제를 방지할 수 있습니다.  

### <a name="replication-transactions"></a>복제 트랜잭션
로그 판독기 에이전트는 트랜잭션 복제를 위해 구성한 각 데이터베이스의 트랜잭션 로그를 모니터링하고 복제 표시된 트랜잭션을 트랜잭션 로그에서 배포 데이터베이스로 복사합니다. 활성 로그에는 복제용으로 표시되었지만 아직 배포 데이터베이스로 전달되지 않은 모든 트랜잭션이 포함되어야 합니다. 이러한 트랜잭션이 제때에 복제되지 않으면 로그 잘라내기가 수행되지 않을 수 있습니다. 자세한 내용은 [트랜잭션 복제](../relational-databases/replication/transactional/transactional-replication.md)를 참조하세요.

## <a name="see-also"></a>관련 항목: 
트랜잭션 로그 및 로그 관리 모범 사례에 대한 자세한 내용은 다음 문서 및 서적을 참조하세요.  
  
[트랜잭션 로그&#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md)    
[트랜잭션 로그 파일의 크기 관리](../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
[트랜잭션 로그 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
[데이터베이스 검사점&#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md)   
[recovery interval 서버 구성 옵션 구성](../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)    
[가속 데이터베이스 복구](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)       
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
[Paul Randall, “SQL Server의 로깅 및 복구 이해”](https://technet.microsoft.com/magazine/2009.02.logging.aspx)    
[Tony Davis 및 Gail Shaw 공저, "SQL Server 트랜잭션 로그 관리"](https://www.simple-talk.com/books/sql-books/sql-server-transaction-log-management-by-tony-davis-and-gail-shaw/)  
  
  
