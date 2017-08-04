---
title: "검사점을 사용 하 여 패키지 다시 시작 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 5207ffe29852aa5ed10144a3184917704682c49e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="restart-packages-by-using-checkpoints"></a>검사점을 사용하여 패키지 다시 시작
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 전체 패키지를 다시 실행하지 않고 오류 발생 시점에서 실패한 패키지를 다시 시작할 수 있습니다. 패키지가 검사점을 사용하도록 구성된 경우 패키지 실행에 대한 정보는 검사점 파일에 기록됩니다. 실패한 패키지가 다시 실행될 때 검사점 파일은 오류 발생 지점에서 패키지를 다시 시작하는 데 사용됩니다. 패키지가 성공적으로 실행된 경우 검사점 파일은 삭제되고 다음에 패키지가 실행될 때 다시 만들어집니다.  
  
 패키지에서 검사점을 사용하면 다음과 같은 이점이 있습니다.  
  
-   큰 파일의 반복적인 다운로드 및 업로드를 피할 수 있습니다. 예를 들어 각 다운로드에 FTP 태스크를 사용하여 여러 큰 파일을 다운로드하는 패키지의 경우, 특정 파일에 대한 다운로드가 실패하면 패키지를 다시 시작하여 해당 파일만 다운로드할 수 있습니다.  
  
-   대용량 데이터의 반복적인 로드를 피할 수 있습니다. 예를 들어 차원마다 다른 대량 삽입 태스크를 사용하여 데이터 웨어하우스의 차원 테이블로 대량 삽입을 수행하는 패키지의 경우, 특정 차원 테이블에 대한 삽입이 실패하면 패키지를 다시 시작할 수 있으며 해당 차원만 다시 로드됩니다.  
  
-   반복적인 값 집계를 피할 수 있습니다. 예를 들어 각 집계를 수행하기 위해 별도의 데이터 흐름 태스크를 사용하여 평균 및 합계와 같은 많은 집계를 계산하는 패키지의 경우 특정 집계 계산이 실패하면 패키지를 다시 시작할 수 있으며 해당 집계만 다시 계산됩니다.  
  
 패키지가 검사점을 사용하도록 구성된 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 검사점 파일에서 다시 시작 지점을 캡처합니다. 실패한 컨테이너 유형 및 트랜잭션과 같은 기능의 구현은 검사점 파일에 기록된 다시 시작 지점에 영향을 미칩니다. 변수의 현재 값도 검사점 파일에 캡처됩니다. 그러나 **Object** 데이터 형식의 변수 값은 검사점 파일에 저장되지 않습니다.  
  
## <a name="defining-restart-points"></a>다시 시작 지점 정의  
 단일 태스크를 캡슐화하는 태스크 호스트 컨테이너는 다시 시작할 수 있는 가장 작은 단위입니다. 또한 Foreach Loop 컨테이너 및 트랜잭션이 적용된 컨테이너도 작업의 최소 단위로 간주됩니다.  
  
 트랜잭션이 적용된 컨테이너가 실행 중인 동안 패키지가 중지된 경우 트랜잭션은 중단되고 컨테이너에 의해 수행된 모든 작업은 롤백됩니다. 실패한 컨테이너는 패키지를 다시 시작할 때 다시 실행됩니다. 트랜잭션이 적용된 컨테이너의 모든 자식 컨테이너에 대한 작업 완료는 검사점 파일에 기록되지 않습니다. 그러므로 패키지를 다시 시작하면 트랜잭션이 적용된 컨테이너와 그 자식 컨테이너가 다시 실행됩니다.  
  
> [!NOTE]  
>  같은 패키지에서 검사점 및 트랜잭션을 사용하면 예기치 않은 결과가 발생할 수 있습니다. 예를 들어 패키지가 실패하고 검사점에서 다시 시작되면 패키지에서 이미 성공적으로 커밋한 트랜잭션을 반복할 수 있습니다.  
  
 For Loop 및 Foreach Loop 컨테이너에 대한 검사점 데이터는 저장되지 않습니다. 패키지를 다시 시작할 때 For Loop 및 Foreach Loop 컨테이너와 그 자식 컨테이너는 다시 실행됩니다. 루프에 있는 자식 컨테이너가 성공적으로 실행되면 검사점 파일에 기록되지 않고 다시 실행됩니다. 자세한 내용 및 해결 방법은 [SSIS 검사점이 For Loop 또는 Foreach Loop 컨테이너 항목에 대해 허용되지 않습니다.](http://go.microsoft.com/fwlink/?LinkId=241633)를 참조하십시오.  
  
 패키지를 다시 시작하면 패키지는 구성을 다시 로드하는 대신 검사점 파일에 기록된 구성 정보를 사용합니다. 이렇게 하면 패키지가 실패한 시점과 동일한 구성으로 다시 실행될 수 있습니다.  
  
 패키지는 제어 흐름 수준에서만 다시 시작할 수 있습니다. 데이터 흐름 도중에 패키지를 다시 시작할 수 없습니다. 전체 데이터 흐름을 다시 실행하지 않으려면 패키지가 여러 데이터 흐름으로 구성되도록 디자인하고 각 데이터 흐름이 서로 다른 데이터 흐름 태스크를 사용하도록 해야 합니다. 이 방법으로 하나의 데이터 흐름 태스크만 다시 실행하여 패키지를 다시 시작할 수 있습니다.  
  
## <a name="configuring-a-package-to-restart"></a>다시 시작하도록 패키지 구성  
 검사점 파일에는 모든 완료된 컨테이너의 실행 결과, 시스템 및 사용자 정의 변수의 현재 값 및 패키지 구성 정보가 포함되어 있습니다. 또한 패키지의 고유 식별자도 검사점 파일에 포함됩니다. 패키지를 성공적으로 다시 시작하려면 검사점 파일에 있는 패키지 식별자가 패키지와 일치해야 하며, 그렇지 않으면 다시 시작할 수 없습니다. 이렇게 하면 패키지가 다른 패키지 버전에 의해 기록된 검사점 파일을 사용하는 것을 막을 수 있습니다. 패키지가 성공적으로 실행되면 다시 시작한 후 검사점 파일이 삭제됩니다.  
  
 다음 표에서는 검사점을 구현하기 위해 설정하는 패키지 속성을 나열합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|CheckpointFileName|검사점 파일의 이름을 지정합니다.|  
|CheckpointUsage|검사점 사용 여부를 지정합니다.|  
|SaveCheckpoints|패키지의 검사점 저장 여부를 나타냅니다. 오류 발생 시점에서 패키지를 다시 시작하려면 이 속성을 True로 설정해야 합니다.|  
  
 이 밖에도 다시 시작 지점으로 식별할 패키지 내의 모든 컨테이너에 대해 FailPackageOnFailure 속성을 **true** 로 설정해야 합니다.  
  
 ForceExecutionResult 속성을 사용하여 패키지에 있는 검사점의 사용을 테스트할 수 있습니다. 태스크 또는 컨테이너의 ForceExecutionResult를 Failure로 설정하면 실시간 오류와 동일한 오류를 만들 수 있습니다. 패키지를 다시 실행하면 실패한 태스크와 컨테이너가 다시 실행됩니다.  
  
### <a name="checkpoint-usage"></a>검사점 사용  
 CheckpointUsage 속성은 다음 값으로 설정할 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**안 함**|검사점 파일을 사용하지 않고 패키지가 패키지 워크플로의 처음부터 시작되도록 지정합니다.|  
|**항상**|검사점 파일을 항상 사용하고 패키지가 이전의 실행 오류 지점부터 다시 시작하도록 지정합니다. 검사점 파일을 찾을 수 없는 경우 패키지는 실패합니다.|  
|**IfExists**|검사점 파일이 있는 경우 이를 사용하도록 지정합니다. 검사점 파일이 있으면 패키지는 이전 실행 오류 지점부터 다시 시작하고, 그렇지 않으면 패키지 워크플로의 처음부터 실행됩니다.|  
  
> [!NOTE]  
>  dtexec의 **/CheckPointing on** 옵션은 패키지의 **SaveCheckpoints** 속성을 **True**로 설정하고 **CheckpointUsage** 속성을 Always로 설정하는 것과 같습니다. 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
## <a name="securing-checkpoint-files"></a>검사점 파일 보안 설정  
 패키지 수준 보호에는 검사점 파일 보호가 포함되지 않으므로 이러한 파일에 대해 보안을 별도로 설정해야 합니다. 검사점 데이터는 파일 시스템에만 저장할 수 있으므로 운영 체제의 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더를 보호해야 합니다. 검사점 파일에는 현재 변수 값을 비롯하여 패키지 상태에 대한 정보가 들어 있으므로 검사점 파일에 대해 보안을 설정하는 것은 중요합니다. 예를 들어 변수에 전화 번호와 같은 개인 데이터 행이 여러 개 있는 레코드 집합이 포함될 수 있습니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  

## <a name="configure-checkpoints-for-restarting-a-failed-package"></a>실패한 패키지를 다시 시작하는 검사점 구성
  검사점에 적용되는 속성을 설정하여 전체 패키지를 다시 실행하는 대신 장애 지점에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 다시 시작하도록 구성합니다.  
  
### <a name="to-configure-a-package-to-restart"></a>패키지를 다시 시작하도록 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 구성할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  제어 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
5.  SaveCheckpoints 속성을 **True**로 설정합니다.  
  
6.  CheckpointFileName 속성에 검사점 파일의 이름을 입력합니다.  
  
7.  CheckpointUsage 속성을 다음 두 값 중 하나로 설정합니다.  
  
    -   패키지를 항상 검사점에서 다시 시작하려면 **Always** 를 선택합니다.  
  
        > [!IMPORTANT]  
        >  검사점 파일을 사용할 수 없으면 오류가 발생합니다.  
  
    -   검사점 파일이 있는 경우에만 패키지를 검사점에서 다시 시작하려면 **IfExists** 를 선택합니다.  
  
8.  패키지가 다시 시작될 수 있는 태스크 및 컨테이너를 구성합니다.  
  
    -   태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
    -   선택한 각 태스크 및 컨테이너에 대해 FailPackageOnFailure 속성을 **True** 로 설정합니다.  
    
## <a name="external-resources"></a>외부 리소스  
  
-   social.technet.microsoft.com의 기술 문서 - [장애 조치(Failover) 또는 실패 이후 SSIS 패키지 자동 다시 시작](http://go.microsoft.com/fwlink/?LinkId=200407)  
  
-   support.microsoft.com의 고객 지원 문서 - [SSIS 검사점이 For Loop 또는 Foreach Loop 컨테이너 항목에 대해 허용되지 않습니다.](http://go.microsoft.com/fwlink/?LinkId=241633)  

