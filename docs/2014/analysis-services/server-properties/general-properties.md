---
title: 일반 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- IdleConnectionTimeout property
- InstanceVisible property
- TempDir property
- AdminTimeout property
- MinIdleSessionTimeout property
- MaxIdleSessionTimeout property
- IdleOrphanSessionTimeout property
- BackupDir property
- CommitTimeout property
- ExternalCommandTimeout property
- Enabled property
- ForceCommitTimeout property
- Port property
- CoordinatorShutdownMode property
- ServerTimeout property
- AllowedBrowsingFolders property
- CoordinatorCancelCount property
- DataDir property
- CoordinatorQueryMaxThreads property
- CoordinatorExecutionMode property
- ExternalConnectionTimeout property
- CollationName property
- EnableFast1033Locale property
- CoordinatorBuildMaxThreads property
- Language property
- StatisticsStoreSize property
- RepositoryConnectionString property
ms.assetid: 88a8117c-396a-469f-a62d-c6f262504021
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b833fe2710ce04cb4a0c8b08fedc9a882c19add
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069026"
---
# <a name="general-properties"></a>일반 속성
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 서버 속성을 사용할 수 있습니다. 이 항목에서는 msmdsrv.ini 파일의 서버 속성 중 보안, 네트워크, ThreadPool 등 특정 섹션에 포함되지 않은 속성에 대해 설명됩니다. 추가 서버 속성 및 해당 속성 설정 방법은 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 및 테이블 형식 서버 모드 (다르게 표시 되지 않은 경우)  
  
## <a name="non-specific-category"></a>일반 범주  
 `AdminTimeout`  
 관리자 제한 시간(초)을 정의하는 부호 있는 32비트 정수 속성입니다. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 이 고급 속성을 변경하면 안 됩니다.  
  
 이 속성의 기본값은 0으로 제한 시간이 없음을 나타냅니다.  
  
 `AllowedBrowsingFolders`  
 Analysis Services 대화 상자에서 파일을 저장하고 열고 찾을 때 검색할 수 있는 폴더를 쉼표로 구분된 목록으로 지정하는 문자열 속성입니다. Analysis Services 서비스 계정은 목록에 추가되는 모든 폴더에 대해 읽기 및 쓰기 권한을 가지고 있어야 합니다.  
  
 `BackupDir`  
 백업 명령의 일부로 경로가 지정 되지 않은 경우 기본적으로 백업 파일이 저장 되는 디렉터리의 이름을 식별 하는 문자열 속성입니다.  
  
 `CollationName`  
 서버 데이터 정렬을 식별하는 문자열 속성입니다. 자세한 내용은 [언어 및 데이터 정렬&#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)을 참조하세요.  
  
 `CommitTimeout`  
 서버가 트랜잭션을 커밋하기 위해 쓰기 잠금을 획득할 때까지 대기하는 시간(밀리초)을 지정하는 정수 속성입니다. 서버에서는 트랜잭션을 커밋하는 쓰기 잠금을 적용하기 전에 다른 잠금이 해제될 때까지 기다려야 하므로 대기 기간이 필요할 수 있습니다.  
  
 이 속성의 기본값은 0으로 서버에서 무기한 대기함을 나타냅니다. 잠금 관련 속성에 대한 자세한 내용은 [SQL Server 2008 R2 Analysis Services Operations Guide](https://go.microsoft.com/fwlink/?LinkID=225539)(SQL Server 2008 R2 Analysis Services 작업 가이드)를 참조하세요.  
  
 `CoordinatorBuildMaxThreads`  
 파티션 인덱스를 작성하도록 할당된 최대 스레드 수를 정의하는 부호 있는 32비트 정수 속성입니다. 메모리 사용을 늘리는 대신 파티션 인덱싱 속도를 높이려면 이 값을 늘리십시오. 이 속성에 대한 자세한 내용은 [SQL Server 2008 R2 Analysis Services 작업 가이드](https://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오.  
  
 `CoordinatorCancelCount`  
 내부 반복 횟수에 따라 Cancel 이벤트가 발생했는지 여부를 서버에서 검사하는 빈도를 정의하는 부호 있는 32비트 정수 속성입니다. 일반 성능 대신 Cancel 이벤트를 보다 자주 검사하려면 이 값을 줄이십시오.  
  
 테이블 형식 서버 모드에서는 `CoordinatorCancelCount`가 무시됩니다.  
  
 `CoordinatorExecutionMode`  
 서버에서 시도하는 작업 처리 및 쿼리를 포함한 최대 병렬 작업 수를 정의하는 부호 있는 32비트 정수 속성입니다. 0으로 설정하면 내부 알고리즘에 따라 서버에서 작업 수를 결정합니다. 양수 값은 최대 작업 수의 합계를 나타냅니다. 음수 값은 부호를 반대로 하여 프로세서당 최대 작업 수를 나타냅니다.  
  
 테이블 형식 서버 모드에서는 `CoordinatorExecutionMode`가 무시됩니다.  
  
 이 속성의 기본값은 -4로 프로세서당 4개의 병렬 작업으로 서버가 제한됩니다. 이 속성에 대한 자세한 내용은 [SQL Server 2008 R2 Analysis Services 작업 가이드](https://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오.  
  
 `CoordinatorQueryMaxThreads`  
 쿼리 해결 중 파티션 세그먼트당 최대 스레드 수를 정의하는 부호 있는 32비트 정수 속성입니다. 동시 사용자 수가 적을수록 메모리 사용량이 높은 대신 이 값을 높일 수 있습니다. 반대로 동시 사용자 수가 많으면 값을 줄여야 합니다.  
  
 `CoordinatorShutdownMode`  
 코디네이터 종료 모드를 정의하는 부울 속성입니다. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 이 고급 속성을 변경하면 안 됩니다.  
  
 `DataDir`  
 데이터가 저장되는 디렉터리의 이름을 식별하는 문자열 속성입니다.  
  
 `DeploymentMode`  
 Analysis Services 서버 인스턴스의 작업 컨텍스트를 결정합니다. 대화 상자, 메시지 및 설명서에서는이 속성을 ' 서버 모드 ' 라고 합니다. 이 속성은 Analysis Services를 설치할 때 선택한 서버 모드를 기준으로 SQLServer 설치 프로그램이 구성합니다. 이 속성을 내부 값으로만 간주하여 항상 설치 프로그램에서 지정한 값을 사용해야 합니다.  
  
 이 속성에 유효한 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|이것은 기본값입니다. 이 설정은 MOLAP, HOLAP 및 ROLAP 스토리지를 사용하는 다차원 데이터베이스와 데이터 마이닝 모델에 서비스를 제공하는 데 사용되는 다차원 모드를 지정합니다.|  
|1|SharePoint용 PowerPivot 배포의 일부로 설치된 Analysis Services 인스턴스를 지정합니다. SharePoint용 PowerPivot 설치의 일부인 Analysis Services 인스턴스의 배포 모드 속성은 변경하지 마십시오. 모드를 변경하면 PowerPivot 데이터가 서버에서 더 이상 실행되지 않습니다.|  
|2|메모리 내 스토리지나 DirectQuery 스토리지를 사용하는 테이블 형식 model 데이터베이스를 호스팅하는 데 사용되는 테이블 형식 모드를 지정합니다.|  
  
 각 모드는 다른 모드와 함께 사용할 수 없습니다. 테이블 형식 모드용으로 구성된 서버는 큐브 및 차원이 포함된 기본 Analysis Services 데이터베이스를 실행할 수 없습니다. 기본 컴퓨터 하드웨어에서 지원하는 경우 같은 컴퓨터에 Analysis Services 인스턴스를 여러 개 설치하고 각 인스턴스가 다른 배포 모드를 사용하도록 구성할 수 있습니다. Analysis Services는 리소스를 많이 사용하는 애플리케이션이므로 고성능 서버인 경우에만 한 시스템에 여러 개의 인스턴스를 배포하는 것이 좋습니다.  
  
 `EnableFast1033Locale`  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `ExternalCommandTimeout`  
 관계형 데이터 원본 및 외부 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 포함하여 외부 서버에 실행된 명령의 제한 시간(초)을 정의하는 정수 속성입니다.  
  
 이 속성의 기본값은 3600(초)입니다.  
  
 `ExternalConnectionTimeout`  
 관계형 데이터 원본 및 외부 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 포함하여 외부 서버에 대한 연결을 만들기 위한 제한 시간(초)을 정의하는 정수 속성입니다. 연결 제한 시간이 연결 문자열에 지정된 경우 이 속성은 무시됩니다.  
  
 이 속성의 기본값은 60(초)입니다.  
  
 `ForceCommitTimeout`  
 진행 중인 쿼리를 포함하여 현재 명령 이전의 다른 명령을 취소하기 전에 쓰기 커밋 작업이 대기해야 하는 시간(밀리초)을 지정하는 정수 속성입니다. 이 속성을 사용하면 쿼리와 같이 우선 순위가 낮은 작업을 취소하여 커밋 트랜잭션을 처리할 수 있습니다.  
  
 이 속성의 기본값은 30초(30000밀리초)로, 커밋 트랜잭션이 30초 동안 대기한 후에만 다른 명령이 강제로 시간 초과됨을 나타냅니다.  
  
> [!NOTE]  
>  이 이벤트에 의해 취소된 쿼리와 프로세스는 "`Server: The operation has been cancelled`"라는 오류 메시지를 보고합니다.  
  
 이 속성에 대한 자세한 내용은 [SQL Server 2008 R2 Analysis Services 작업 가이드](https://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오.  
  
> [!IMPORTANT]  
>  
  `ForceCommitTimeout`은 큐브 처리 명령과 쓰기 저장 작업에 적용됩니다.  
  
 `IdleConnectionTimeout`  
 비활성 상태의 연결에 대한 제한 시간(초)을 지정하는 정수 속성입니다.  
  
 이 속성의 기본값은 0으로 유휴 연결이 시간 초과되지 않음을 나타냅니다.  
  
 `IdleOrphanSessionTimeout`  
 서버 메모리에서 분리된 세션이 유지되는 시간(초)을 정의하는 정수 속성입니다. 분리된 세션은 더 이상 관련 연결이 없는 세션입니다. 기본값은 120초입니다.  
  
 `InstanceVisible`  
 서버 인스턴스가 SQL Server Browser 서비스에서 인스턴스 요청을 검색하도록 표시되는지 여부를 나타내는 부울 속성입니다. 기본값은 true입니다. 이 속성을 false로 설정하면 인스턴스가 SQL Server Browser에 표시되지 않습니다.  
  
 `Language`  
 오류 메시지 및 번호 서식 지정을 포함하여 언어를 정의하는 문자열 속성입니다. 이 속성은 CollationName 속성을 무시합니다.  
  
 이 속성의 기본값은 빈 문자열로 CollationName 속성이 언어를 정의함을 나타냅니다.  
  
 `LogDir`  
 서버 로그가 포함된 디렉터리 이름을 식별하는 문자열 속성입니다. 이 속성은 데이터베이스 테이블과는 달리 디스크 파일이 로깅용으로 사용되는 경우에만 적용됩니다(기본 동작).  
  
 `MaxIdleSessionTimeout`  
 최대 유휴 세션 제한 시간(초)을 정의하는 정수 속성입니다. 기본값은 0 이며,이는 세션이 시간 초과 되지 않음을 나타냅니다. 그러나 서버에서 리소스 제약 조건을 적용 하는 경우에도 유휴 세션이 제거 됩니다.  
  
 `MinIdleSessionTimeout`  
 유휴 세션이 시간 초과되는 최소 시간(초)을 정의하는 정수 속성입니다. 기본값은 2700초입니다. 이 시간이 만료되면 서버에서 유휴 세션을 종료할 수 있지만 이를 위한 메모리가 필요한 경우에만 세션을 종료합니다.  
  
 `Port`  
 서버에서 클라이언트 연결을 수신할 포트 번호를 정의하는 정수 속성입니다. 설정하지 않으면 서버가 사용되지 않은 첫 번째 포트를 동적으로 검색합니다.  
  
 이 속성의 기본값은 0으로 이후 포트 2383이 기본값이 됩니다. 포트 구성에 대한 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하십시오.  
  
 `ServerTimeout`  
 쿼리에 대한 제한 시간(초)을 정의하는 정수입니다. 기본값은 3600초(또는 60분)입니다. 0을 지정하면 쿼리가 시간 초과되지 않습니다.  
  
 `TempDir`  
 처리, 복원 및 기타 작업 중에 사용되는 임시 파일을 정의하기 위한 위치를 지정하는 문자열 속성입니다. 이 속성의 기본값은 설치 프로그램에 의해 결정됩니다. 지정하지 않는 경우의 기본값은 Data 디렉터리입니다.  
  
## <a name="requestprioritization-category"></a>RequestPrioritization 범주  
 `Enabled`  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `StatisticsStoreSize`  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services에서 서버 속성 구성](server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
