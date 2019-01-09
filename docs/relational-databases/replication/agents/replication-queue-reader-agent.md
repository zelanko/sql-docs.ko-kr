---
title: 복제 큐 판독기 에이전트 | Microsoft 문서
ms.custom: ''
ms.date: 10/29/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], Queue Reader Agent
- command prompt [SQL Server replication]
- Queue Reader Agent, parameter reference
- Queue Reader Agent, executables
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f794ccc0191454bc900b039af16cd31258821c61
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591167"
---
# <a name="replication-queue-reader-agent"></a>복제 큐 판독기 에이전트
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  복제 큐 판독기 에이전트는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 큐 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 메시지 큐에 저장된 메시지를 읽고 해당 메시지를 게시자에 적용하는 실행 파일입니다. 큐 판독기 에이전트는 지연 업데이트를 허용하는 스냅숏 및 트랜잭션 게시와 함께 사용됩니다.  
  
> [!NOTE]  
>  매개 변수는 지정되는 순서에 제한을 받지 않습니다. 선택적 매개 변수가 지정되지 않은 경우 기본 에이전트 프로필을 기반으로 하여 미리 정의된 값이 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
qrdrsvc [-?]  
[-Continuous]  
[-DefinitionFile definition_file]  
[-Distributor server_name[\instance_name]]  
[-DistributionDB distribution_database]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-LoginTimeOut login_time_out_seconds]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PollingInterval polling_interval]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-ProfileName agent_profile_name]  
[-QueryTimeOut query_time_out_seconds]  
[-ResolverState [1|2|3]]  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 사용법 정보를 표시합니다.  
  
 **-Continuous**  
 에이전트에서 지연된 트랜잭션의 처리를 계속 시도할지 여부를 지정합니다. 이 인수가 지정된 경우 에이전트는 구독자에서 보류 중인 지연 트랜잭션이 없는 경우에도 실행을 계속합니다.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 에이전트 정의 파일의 경로입니다. 에이전트 정의 파일에는 에이전트의 명령줄 인수가 들어 있습니다. 파일 내용은 실행 파일로 구문 분석됩니다. 임의 문자가 있는 인수 값을 지정하려면 큰따옴표(")를 사용합니다.  
  
 **-Distributor** _server_name_[**\\**_instance_name_]  
 배포자 이름입니다. 해당 서버에 있는 기본 *인스턴스에 대해* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정하고, 해당 서버에 있는 기본 *server_name*\\*instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 지정하고, 이 인수가 지정되지 않은 경우 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름이 기본 이름이 됩니다.  
  
 **-DistributionDB** _distribution_database_  
 배포 데이터베이스입니다.  
  
 **-DistributorLogin** _distributor_login_  
 배포자의 로그인 이름입니다.  
  
 **-DistributorPassword** _distributor_password_  
 배포자 암호입니다.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 배포자의 보안 모드를 지정합니다. 값 **0** 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 모드(기본값)를 나타내며 값 **1** 은 Windows 인증 모드를 나타냅니다.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 연결을 만들 때 큐 판독기 에이전트에서 사용하는 SSL(Secure Sockets Layer) 암호화의 수준입니다.  
  
|EncryptionLevel 값|설명|  
|---------------------------|-----------------|  
|**0**|SSL이 사용되지 않음을 지정합니다.|  
|**1**|SSL이 사용되지만 에이전트에서 SSL 서버 인증서가 트러스트된 발급자에 의해 서명된 것인지 확인하지 않음을 지정합니다.|  
|**2**|SSL이 사용되고 인증서가 확인됨을 지정합니다.|  

 > [!NOTE]  
 >  유효한 SSL 인증서는 SQL Server의 정규화된 도메인 이름으로 정의됩니다. -EncryptionLevel을 2로 설정할 때 에이전트가 성공적으로 연결되도록 하려면 로컬 SQL Server에서 별칭을 만듭니다. '별칭 이름' 매개 변수는 서버 이름이어야 하며 '서버' 매개 변수는 SQL Server의 정규화된 이름으로 설정되어야 합니다.
  
 자세한 내용은 [보안 개요&#40;복제&#41;](../../../relational-databases/replication/security/security-overview-replication.md)를 참조하세요.  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 큐 판독기 작업을 수행하는 동안 기록에 추가되는 양을 지정합니다. **1**을 선택하여 성능에서 기록 로깅의 영향을 최소화할 수 있습니다.  
  
|HistoryVerboseLevel 값|설명|  
|-------------------------------|-----------------|  
|**0**|기록 로깅을 사용하지 않습니다(권장되지 않음).|  
|**1**|기본. 시작, 진행, 성공 등과 같이 상태가 동일한 이전 기록 메시지를 항상 업데이트합니다. 상태가 같은 이전 레코드가 없으면 새 레코드를 삽입합니다.|  
|**2**|유휴 메시지 또는 장기 실행 작업 메시지를 포함하여 새 기록 레코드를 삽입합니다.|  
|**3**|문제 해결에 유용한 추가 정보를 포함하는 새 기록 레코드를 삽입합니다.|  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 로그인 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 15초입니다.  
  
 **-Output** _output_path_and_file_name_  
 에이전트 출력 파일의 경로입니다. 파일 이름을 지정하지 않으면 출력이 콘솔로 전달됩니다. 지정된 파일 이름이 존재하면 출력이 파일에 추가됩니다.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 출력이 자세해야 하는지 여부를 지정합니다. 정보 표시 수준이 **0**이면 오류 메시지만 출력됩니다. 정보 표시 수준이 **1**이면 모든 진행률 보고 메시지가 출력됩니다. 정보 표시 수준이 **2** (기본값)이면 디버깅에 유용한 오류 메시지와 진행률 보고 메시지가 모두 출력됩니다.  
  
 **-PollingInterval** _polling_interval_  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기반 큐를 사용하는 구독 업데이트에만 해당됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 큐가 보류 중인 지연 트랜잭션에 대해 폴링되는 빈도(초)를 지정합니다. 이 값은 0초에서 240초 사이일 수 있습니다. 기본값은 5초입니다.  
  
 **-PublisherFailoverPartner** _server_name_[**\\**_instance_name_]  
 게시 데이터베이스와 함께 데이터베이스 미러링 세션에 참여하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 장애 조치 파트너 인스턴스를 지정합니다. 자세한 내용은 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)를 참조하세요.  
  
 **-ProfileName** _agent_profile_name_  
 에이전트에 대한 기본값 집합을 제공하는 데 사용되는 에이전트 프로필의 이름입니다. 자세한 내용은 [복제 에이전트 프로필](../../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하세요.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 쿼리 시간이 초과될 때까지 걸리는 시간(초)입니다. 기본값은 1800초입니다.  
  
 **-ResolverState** [ **1**| **2**| **3**]  
 지연 업데이트 충돌의 해결 방법을 지정합니다. 값 **1** 은 충돌 시 게시자의 내용이 적용되고, 현재 충돌하는 지연 트랜잭션이 게시자 및 원래 업데이트 구독자에서 다시 롤백되며, 이후 지연 트랜잭션의 처리가 계속됨을 나타냅니다. 값 **2** 는 충돌 시 구독자의 내용이 적용되고 지연 트랜잭션이 게시자의 값을 재정의함을 나타냅니다. 값 **3** 은 충돌이 발생할 경우 구독자가 다시 초기화되고, 게시자의 내용이 적용되고, 이후 지연 트랜잭션의 처리가 종료되며, 구독이 다시 초기화됨을 나타냅니다. 기본 설정은 트랜잭션 게시의 경우 **1** 이고 스냅숏 게시의 경우 **3** 입니다.  
  
## <a name="remarks"></a>Remarks  
 큐 판독기 에이전트를 시작하려면 명령 프롬프트에서 **qrdrsvc.exe** 를 실행합니다. 자세한 내용은 [복제 에이전트 실행 파일](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 관리](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
