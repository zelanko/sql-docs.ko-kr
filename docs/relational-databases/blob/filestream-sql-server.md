---
title: FILESTREAM(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server]
- FILESTREAM [SQL Server], about
- FILESTREAM [SQL Server], overview
ms.assetid: 9a5a8166-bcbe-4680-916c-26276253eafa
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: c56f702b6946662657f35fd7e0c8e6b9bc791c36
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287287"
---
# <a name="filestream-sql-server"></a>FILESTREAM(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

FILESTREAM을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기반 애플리케이션에서 문서 및 이미지와 같은 구조화되지 않은 데이터를 파일 시스템에 저장할 수 있습니다. 애플리케이션은 풍부한 스트리밍 API 및 파일 시스템의 성능을 활용할 수 있고 동시에 구조화되지 않은 데이터와 해당되는 구조화된 데이터 간에 트랜잭션 일관성을 유지할 수 있습니다.  
  
FILESTREAM은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] varbinary(max) **BLOB(Binary Large Object) 데이터를 파일 시스템의 파일로 저장하여** 을 NTFS 및 ReFS 파일 시스템과 통합합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 FILESTREAM 데이터를 삽입, 업데이트, 쿼리, 검색 및 백업할 수 있습니다. Win32 파일 시스템 인터페이스에서는 데이터에 대한 스트리밍 액세스를 제공합니다.  
  
FILESTREAM은 파일 데이터를 캐시하기 위해 NT 시스템 캐시를 사용합니다. 이를 통해 FILESTREAM 데이터가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 성능에 미치는 영향을 줄일 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀이 사용되지 않으므로 이 메모리는 쿼리 처리용으로 사용할 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하거나 업그레이드할 때 FILESTREAM이 자동으로 사용하도록 설정되지는 않습니다. SQL Server 구성 관리자 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 FILESTREAM을 사용하도록 설정해야 합니다. FILESTREAM을 사용하려면 특수 파일 그룹 유형을 포함하도록 데이터베이스를 만들거나 수정해야 합니다. 그런 다음 FILESTREAM 특성이 있는 **varbinary(max)** 열을 포함하도록 테이블을 만들거나 수정합니다. 이러한 태스크를 완료한 후에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 Win32를 사용하여 FILESTREAM 데이터를 관리할 수 있습니다.  

## <a name="when-to-use-filestream"></a>FILESTREAM을 사용하는 경우

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 BLOB은 테이블에 데이터를 저장하는 표준 **varbinary(max)** 데이터 또는 파일 시스템에 데이터를 저장하는 FILESTREAM **varbinary(max)** 개체가 될 수 있습니다. 데이터베이스 스토리지를 사용해야 할지 또는 파일 시스템 스토리지를 사용해야 할지 여부는 데이터의 크기와 사용으로 결정됩니다. 다음 조건에 해당될 경우 FILESTREAM을 사용해야 합니다.  

- 저장되는 개체가 평균적으로 1MB를 초과할 경우  
- 신속한 읽기 액세스가 중요할 경우
- 중간 계층 애플리케이션 논리를 사용하는 애플리케이션을 개발할 경우  

크기가 작은 개체의 경우 데이터베이스에 **varbinary(max)** BLOB을 저장하면 스트리밍 성능이 더 좋아집니다.  

## <a name="filestream-storage"></a>FILESTREAM 스토리지

FILESTREAM 스토리지는 데이터가 파일 시스템에 BLOB으로 저장된 **varbinary(max)** 열로 구현됩니다. BLOB의 크기는 파일 시스템의 볼륨 크기로만 제한됩니다. 표준 **varbinary(max)** 제한은 2GB의 파일 크기로 파일 시스템에 저장된 BLOB에 적용되지 않습니다.  
  
파일 시스템에 열의 데이터를 저장하도록 지정하려면 **varbinary(max)** 열에 FILESTREAM 특성을 지정합니다. 이렇게 하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 해당 열의 모든 데이터를 데이터베이스 파일이 아닌 파일 시스템에 저장하게 됩니다.  
  
FILESTREAM 데이터는 FILESTREAM 파일 그룹에 저장되어야 합니다. FILESTREAM 파일 그룹은 파일 자체가 아닌 파일 시스템 디렉터리를 포함하는 특수한 파일 그룹입니다. 이러한 파일 시스템 디렉터리를 *데이터 컨테이너*라고 합니다. 데이터 컨테이너는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 스토리지와 파일 시스템 스토리지 사이의 인터페이스입니다. 

FILESTREAM 스토리지를 사용할 때 다음 사항을 고려하십시오.  

- 테이블에 FILESTREAM 열이 있을 경우 각 행에는 Null이 아닌 고유한 행 ID가 있어야 합니다.  
- FILESTREAM 파일 그룹에는 여러 개의 데이터 컨테이너를 추가할 수 있습니다.  
- FILESTREAM 데이터 컨테이너는 중첩될 수 없습니다.  
- 장애 조치(failover) 클러스터링을 사용할 경우 FILESTREAM 파일 그룹이 공유 디스크 리소스에 있어야 합니다.  
- FILESTREAM 파일 그룹은 압축된 볼륨에 있을 수 있습니다.

### <a name="integrated-management"></a>통합 관리

FILESTREAM이 **varbinary(max)** 열로 구현되어 [!INCLUDE[ssDE](../../includes/ssde-md.md)]으로 바로 통합되었으므로 대부분의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구 및 기능이 FILESTREAM 데이터를 수정하지 않고 수행됩니다. 예를 들어 FILESTREAM 데이터로 모든 백업 및 복구 모델을 사용할 수 있고 FILESTREAM 데이터는 구조화된 데이터와 함께 데이터베이스에 백업됩니다. FILESTREAM 데이터를 관계형 데이터와 함께 백업하지 않으려면 부분 백업을 사용하여 FILESTREAM 파일 그룹을 제외할 수 있습니다.  

### <a name="integrated-security"></a>Integrated Security

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 FILESTREAM 데이터는 다른 데이터와 마찬가지로 테이블 또는 열 수준에서 사용 권한을 부여하여 보안이 설정됩니다. 사용자가 테이블의 FILESTREAM 열에 대한 사용 권한이 있을 경우 이 사용자는 관련 파일을 열 수 있습니다.  

> [!NOTE]
> 암호화는 FILESTREAM 데이터에서 지원되지 않습니다.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 실행하는 계정에만 FILESTREAM 컨테이너에 대한 사용 권한이 부여됩니다. 다른 계정에는 데이터 컨테이너에 대한 사용 권한을 부여하지 않는 것이 좋습니다.

> [!NOTE]
> SQL 로그인은 FILESTREAM 컨테이너에서 작동하지 않습니다. NTFS 또는 ReFS 인증만 FILESTREAM 컨테이너에서 작동합니다.

## <a name="accessing-blob-data-with-transact-sql-and-file-system-streaming-access"></a><a name="dual"></a> TRANSACT-SQL 및 파일 시스템 스트리밍 액세스를 사용하여 BLOB 데이터 액세스

FILESTREAM 열에 데이터를 저장한 후 [!INCLUDE[tsql](../../includes/tsql-md.md)] 트랜잭션 또는 Win32 API를 사용하여 해당 파일에 액세스할 수 있습니다.  
  
### <a name="transact-sql-access"></a>Transact-SQL 액세스

[!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 FILESTREAM 데이터를 삽입, 업데이트 및 삭제할 수 있습니다.  

- 삽입 작업을 통해 FILESTREAM 필드를 Null 값, 비어 있는 값 또는 상대적으로 짧은 인라인 데이터로 미리 채울 수 있습니다. 그러나 크기가 큰 데이터는 Win32 인터페이스를 사용하는 파일로 좀 더 효율적으로 스트리밍됩니다.  
- FILESTREAM 필드를 업데이트할 때 파일 시스템의 기본 BLOB 데이터를 수정합니다. FILESTREAM 필드를 NULL로 설정하면 이 필드와 연결된 BLOB 데이터가 삭제됩니다. 데이터의 부분 업데이트를 수행하기 위해 UPDATE [!INCLUDE[tsql](../../includes/tsql-md.md)] .**Write()로 구현된**청크 업데이트를 사용할 수 없습니다. 
- 행을 삭제하거나 FILESTREAM 데이터가 들어 있는 테이블을 삭제하거나 잘라내면 파일 시스템의 기본 BLOB 데이터가 삭제됩니다.

### <a name="file-system-streaming-access"></a>파일 시스템 스트리밍 액세스

Win32 스트리밍은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션 컨텍스트의 작업을 지원합니다. 트랜잭션 내에서 FILESTREAM 기능을 사용하여 파일의 논리 UNC 파일 시스템 경로를 얻을 수 있습니다. 그런 다음 OpenSqlFilestream API를 사용하여 파일 핸들을 얻습니다. 이 핸들은 파일 시스템의 방식에 따라 파일에 액세스하여 업데이트하기 위해 ReadFile() 및 WriteFile() 같은 Win32 파일 스트리밍 인터페이스에서 사용될 수 있습니다.  

파일 작업이 트랜잭션이므로 파일 시스템을 통해 FILESTREAM 파일을 삭제하거나 이 파일의 이름을 바꿀 수 없습니다.  

**문 모델**

FILESTREAM 파일 시스템 액세스는 파일 열기 및 닫기를 통해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 모델로 합니다. 파일 핸들이 열릴 때 문이 시작되고 파일 핸들이 닫힐 때 문이 종료됩니다. 예를 들어 쓰기 핸들이 닫히면 UPDATE 문이 완료된 경우와 같이 테이블에 등록된 가능한 모든 AFTER 트리거가 실행됩니다.

**스토리지 네임스페이스**

FILESTREAM에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 BLOB 물리적 파일 시스템 네임스페이스를 제어합니다. 새 내장 함수인 [PathName](../../relational-databases/system-functions/pathname-transact-sql.md)에서는 테이블의 각 FILESTREAM 셀에 해당하는 BLOB의 논리 UNC 경로를 제공합니다. 애플리케이션에서는 이 논리 경로를 사용하여 Win32 핸들을 얻고 일반적인 Win32 파일 시스템 인터페이스를 사용하여 BLOB 데이터에 대한 작업을 수행합니다. FILESTREAM 열의 값이 NULL인 경우 함수는 NULL을 반환합니다.  

**트랜잭션된 파일 시스템 액세스**

새 내장 함수인 [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)에서는 세션에 연결된 현재 트랜잭션을 나타내는 토큰을 제공합니다. 트랜잭션이 시작되었지만 아직 중단되거나 커밋되지 않았습니다. 토큰을 가져와서 애플리케이션은 FILESTREAM 파일 시스템 스트리밍 작업을 시작된 트랜잭션과 바인딩합니다. 명시적으로 시작된 트랜잭션이 없을 경우에는 함수는 NULL을 반환합니다.  

트랜잭션이 커밋되거나 중단되기 전에는 모든 파일 핸들이 닫혀 있어야 합니다. 핸들이 트랜잭션 범위 이상으로 열려 있으면 핸들에 대한 추가 읽기가 실패하고 이 핸들에 대한 추가 쓰기는 성공하지만 실제 데이터가 디스크에 작성되지 않습니다. 비슷하게 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 데이터베이스나 인스턴스가 종료되면 열려 있는 모든 핸들이 무효화됩니다.  

**트랜잭션 내구성**

트랜잭션 커밋에 FILESTREAM을 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 파일 시스템 스트리밍 액세스에서 수정된 FILESTREAM BLOB 데이터에 트랜잭션 유지 기능을 사용할 수 있습니다.  

**격리 의미 체계**

격리 의미 체계는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 트랜잭션 격리 수준에 따라 결정됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 파일 시스템 액세스에는 커밋된 읽기 격리 수준이 지원됩니다. 반복 읽기 작업과 직렬화 가능 및 스냅샷 격리도 지원됩니다. 커밋되지 않은 읽기는 지원되지 않습니다.  

파일 시스템 액세스 열기 작업은 잠금을 기다리지 않습니다. 대신 트랜잭션 격리로 인해 데이터에 액세스할 수 없을 경우 즉시 열기 작업에 실패합니다. 격리 위반으로 인해 열기 작업을 계속 진행할 수 없을 경우 ERROR_SHARING_VIOLATION이 발생하며 스트리밍 API 호출에 실패합니다.  

부분 업데이트가 수행되도록 허용하려면 애플리케이션이 디바이스 FS 컨트롤(FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT)을 실행하여 이전 내용을 열려 있는 핸들이 참조하는 파일로 인출할 수 있습니다. 이 작업으로 인해 서버 쪽의 오래된 내용 복사가 트리거됩니다. 애플리케이션 성능을 더 향상시키고 큰 파일로 작업 시 제한 시간이 초과되는 것을 방지하려면 비동기 I/O를 사용하는 것이 좋습니다.  

핸들이 작성된 후 FSCTL이 실행되면 마지막 쓰기 작업이 유지되고 핸들에 기록된 이전의 쓰기 작업은 손실됩니다.

**파일 시스템 API 및 지원되는 격리 수준**

격리 위반으로 인해 파일 시스템 API에서 파일을 열 수 없는 경우 ERROR_SHARING_VIOLATION 예외가 반환됩니다. 두 트랜잭션에서 동일한 파일에 액세스를 시도하면 이 격리 위반이 발생합니다. 액세스 작업의 결과는 파일이 열릴 때의 모드와 트랜잭션이 실행되고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 버전에 따라 달라집니다. 다음 표에서는 두 트랜잭션에서 동일한 파일에 액세스할 때 발생할 수 있는 결과를 간략하게 설명합니다.

|트랜잭션 1|트랜잭션 2|SQL Server 2008에서의 결과|SQL Server 2008 R2 이상에서의 결과|  
|-------------------|-------------------|--------------------------------|------------------------------------------------------|  
|읽기를 위해 열기|읽기를 위해 열기|모두 성공|모두 성공|  
|읽기를 위해 열기|쓰기를 위해 열기|모두 성공 트랜잭션 2에서 수행되는 쓰기 작업이 트랜잭션 1에서 수행되는 읽기 작업에 영향을 주지 않습니다.|모두 성공 트랜잭션 2에서 수행되는 쓰기 작업이 트랜잭션 1에서 수행되는 읽기 작업에 영향을 주지 않습니다.|  
|쓰기를 위해 열기|읽기를 위해 열기|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|모두 성공|  
|쓰기를 위해 열기|쓰기를 위해 열기|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|  
|읽기를 위해 열기|선택을 위해 열기|모두 성공|모두 성공|  
|읽기를 위해 열기|업데이트 또는 삭제를 위해 열기|모두 성공 트랜잭션 2에서 수행되는 쓰기 작업이 트랜잭션 1에서 수행되는 읽기 작업에 영향을 주지 않습니다.|모두 성공 트랜잭션 2에서 수행되는 쓰기 작업이 트랜잭션 1에서 수행되는 읽기 작업에 영향을 주지 않습니다.|  
|쓰기를 위해 열기|선택을 위해 열기|트랜잭션 1이 트랜잭션을 커밋 또는 종료하거나 트랜잭션 잠금 시간이 초과될 때까지 트랜잭션 2가 차단됩니다.|모두 성공|  
|쓰기를 위해 열기|업데이트 또는 삭제를 위해 열기|트랜잭션 1이 트랜잭션을 커밋 또는 종료하거나 트랜잭션 잠금 시간이 초과될 때까지 트랜잭션 2가 차단됩니다.|트랜잭션 1이 트랜잭션을 커밋 또는 종료하거나 트랜잭션 잠금 시간이 초과될 때까지 트랜잭션 2가 차단됩니다.|  
|선택을 위해 열기|읽기를 위해 열기|모두 성공|모두 성공|  
|선택을 위해 열기|쓰기를 위해 열기|모두 성공 트랜잭션 2의 쓰기 작업이 트랜잭션 1에 영향을 주지 않습니다.|모두 성공 트랜잭션 2의 쓰기 작업이 트랜잭션 1에 영향을 주지 않습니다.|  
|업데이트 또는 삭제를 위해 열기|읽기를 위해 열기|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|모두 성공|  
|업데이트 또는 삭제를 위해 열기|쓰기를 위해 열기|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|  
|선택을 위해 열기(반복 읽기 사용)|읽기를 위해 열기|모두 성공|모두 성공|  
|선택을 위해 열기(반복 읽기 사용)|쓰기를 위해 열기|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|트랜잭션 2의 열기 작업이 실패하고 ERROR_SHARING_VIOLATION 예외가 발생합니다.|

**원격 클라이언트를 통한 쓰기**

FILESTREAM 데이터에 대한 원격 파일 시스템 액세스는 SMB(서버 메시지 블록) 프로토콜을 통해 사용할 수 있습니다. 클라이언트가 원격일 경우 클라이언트 쪽에서 캐시하는 쓰기 작업이 없습니다. 쓰기 작업은 항상 서버로 전송되고, 데이터는 서버 쪽에서 캐시합니다. 원격 클라이언트에서 실행 중인 애플리케이션은 작은 쓰기 작업을 통합하여 더 큰 크기의 데이터를 사용하는 쓰기 작업이 적어집니다.  

FILESTREAM 핸들을 사용하여 메모리 매핑된 뷰(메모리 매핑된 I/O)를 만들 수는 없습니다. 메모리 매핑을 FILESTREAM 데이터에 사용할 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 데이터의 일관성과 지속성 또는 데이터베이스의 무결성을 보장할 수 없습니다.  

## <a name="related-tasks"></a>관련 작업

[Enable and Configure FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
[FILESTREAM 사용 데이터베이스 만들기](../../relational-databases/blob/create-a-filestream-enabled-database.md)  
[FILESTREAM 데이터 저장용 테이블 만들기](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)  
[Transact-SQL을 사용하여 FILESTREAM 데이터 액세스](../../relational-databases/blob/access-filestream-data-with-transact-sql.md) [FILESTREAM 데이터용 클라이언트 애플리케이션 만들기](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
[OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
[FILESTREAM 데이터 부분 업데이트](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
[FILESTREAM 애플리케이션에서 데이터베이스 작업과의 충돌 방지](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
[FILESTREAM 사용 데이터베이스 이동](../../relational-databases/blob/move-a-filestream-enabled-database.md)  
[장애 조치(Failover) 클러스터에서 FILESTREAM 설정](../../relational-databases/blob/set-up-filestream-on-a-failover-cluster.md)  
[FILESTREAM 액세스를 위한 방화벽 구성](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)

## <a name="related-content"></a>관련 내용

[FILESTREAM과 기타 SQL Server 기능 간 호환성](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)
<br>[Filestream 및 FileTable 동적 관리 뷰(Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 및 FileTable 카탈로그 뷰(Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream 및 FileTable 시스템 저장 프로시저(Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)

