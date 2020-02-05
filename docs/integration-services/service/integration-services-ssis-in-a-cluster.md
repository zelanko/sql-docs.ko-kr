---
title: 클러스터의 Integration Services(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9203423267f68137e11203be60ffa4d0e0c3e41
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296892"
---
# <a name="integration-services-ssis-in-a-cluster"></a>클러스터의 Integration Services(SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 클러스터형 또는 클러스터 인식형 서비스가 아니며 클러스터 노드 간 장애 조치(failover) 기능을 지원하지 않으므로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 클러스터링이 권장되지 않습니다. 따라서 클러스터형 환경에서는 클러스터의 노드마다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치하고 독립 실행형 서비스로 시작해야 합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 클러스터형 서비스가 아니지만 클러스터의 각 노드에 별도로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치한 후 이러한 서비스가 클러스터 리소스로 작동하도록 수동으로 구성할 수 있습니다.  
  
 그러나 클러스터형 하드웨어 환경 설정의 목표가 고가용성인 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성하지 않고도 이러한 목표를 달성할 수 있습니다.  클러스터 노드의 패키지를 클러스터의 다른 노드에서 관리하려면 클러스터의 각 노드에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일을 수정합니다. 이러한 각 구성 파일을 수정하여 패키지가 저장되어 있는 모든 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 가리키도록 할 수 있습니다. 이렇게 하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성할 때 발생할 수 있는 문제를 방지하고 대부분의 고객이 원하는 고가용성을 제공할 수 있습니다. 구성 파일을 변경하는 방법에 대한 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)를 참조하세요.  
  
 클러스터형 환경에서 서비스를 구성하는 방법을 합리적으로 결정하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 역할을 이해하는 것이 중요합니다. 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)를 참조하세요.  
  
## <a name="disadvantages"></a>단점
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성할 경우 단점은 다음과 같습니다.  
  
-   **장애 조치(failover)가 수행될 경우 실행 중인 패키지가 다시 시작되지 않습니다.**
    
    검사점에서 패키지를 다시 시작하면 패키지 오류를 복구할 수 있습니다. 서비스를 클러스터 리소스로 구성하지 않고 검사점부터 다시 시작할 수 있습니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](../../integration-services/packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 리소스 그룹에 구성하는 경우 클라이언트 컴퓨터에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 msdb 데이터베이스에 저장된 패키지를 관리할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 이러한 이중 홉 시나리오에서 자격 증명을 위임할 수 없습니다.  
  
-   클러스터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 포함된 여러 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 리소스 그룹이 있는 경우 장애 조치(failover)로 인해 예기치 않은 결과가 발생할 수 있습니다. 다음과 같은 시나리오를 고려해 보세요. 그룹1은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 포함하며 노드 A에서 실행 중입니다. 그룹2도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 포함하며 노드 B에서 실행 중입니다. 그룹2는 노드 A로 장애 조치(failover)됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 단일 인스턴스 서비스이므로 노드 A에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 다른 인스턴스를 시작하려고 하면 오류가 발생합니다. 노드 A로 장애 조치(failover)를 시도하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 실패 여부는 그룹 2의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 구성에 따라 달라집니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 리소스 그룹의 다른 서비스에 영향을 주도록 구성되어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 실패로 인해 장애 조치(failover)를 시도하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스도 실패하게 됩니다. 서비스가 리소스 그룹 내의 다른 서비스에 영향을 주지 않도록 구성된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 노드 A로 장애 조치(failover)할 수 있습니다. 그룹2의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 리소스 그룹의 다른 서비스에 영향을 주지 않도록 구성되지 않았다면 장애 조치(failover) 중인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 실패로 인해 장애 조치(failover) 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스까지 실패할 수 있습니다.  

## <a name="configure-the-service-as-a-cluster-resource"></a>서비스를 클러스터 리소스로 구성
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성할 때 얻는 장점이 단점보다 많다고 생각하는 사용자를 위해 이 섹션에서는 필요한 구성 방법을 설명합니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 서비스를 클러스터 리소스로 구성하지 않는 것이 좋습니다( [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 권장).  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성하려면 다음 태스크를 완료해야 합니다.  
  
-   클러스터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치합니다.  
  
     클러스터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치하려면 클러스터의 각 노드에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치해야 합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 클러스터 리소스로 구성합니다.  
  
     클러스터의 각 노드에 Integration Services를 설치한 상태에서 Integration Services를 클러스터 리소스로 구성해야 합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 동일한 리소스 그룹이나 다른 그룹에 서비스를 추가할 수 있습니다. 다음 표에서는 리소스 그룹 선택에 따른 장단점을 설명합니다.  
  
    |Integration Services 및 SQL Server가 동일한 리소스 그룹에 있는 경우|Integration Services 및 SQL Server가 다른 리소스 그룹에 있는 경우|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스가 동일한 가상 서버에서 실행 중이므로 클라이언트 컴퓨터가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 사용하여 msdb 데이터베이스에 저장된 패키지를 관리할 수 있습니다. 이렇게 하면 이중 홉 시나리오의 위임 문제를 피할 수 있습니다.|클라이언트 컴퓨터가 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 msdb 데이터베이스에 저장된 패키지를 관리할 수 없습니다. 클라이언트는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 실행 중인 가상 서버에 연결할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 가상 서버에 사용자의 자격 증명을 위임할 수 없습니다. 이를 이중 홉 시나리오라고 합니다.|  
    |[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 CPU 및 다른 컴퓨터 리소스를 확보하기 위해 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 경합합니다.|여러 노드에 여러 리소스 그룹이 구성되어 있으므로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 CPU 및 다른 컴퓨터 리소스를 확보하기 위해 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 경합하지 않습니다.|  
    |두 서비스가 동일한 컴퓨터에서 실행되므로 패키지를 msdb 데이터베이스에 로드하고 저장할 때 속도가 빨라지고 네트워크 트래픽이 줄어듭니다.|msdb 데이터베이스에 패키지를 로드하고 저장할 때 속도가 느려지고 네트워크 트래픽이 증가할 수 있습니다.|  
    |두 서비스가 동시에 온라인 또는 오프라인 상태가 됩니다.|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 은 오프라인 상태이지만 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스는 온라인 상태일 수 있습니다. 따라서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 msdb 데이터베이스에 저장된 패키지를 사용할 수 없습니다.|  
    |필요에 따라 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 다른 노드로 신속하게 이동할 수 없습니다.|필요에 따라 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 다른 노드로 보다 신속하게 이동할 수 있습니다.|  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 추가할 리소스 그룹을 결정한 후에는 해당 그룹에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 클러스터 리소스로 구성해야 합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 및 패키지 저장소를 구성합니다.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 클러스터 리소스로 구성했으면 클러스터의 각 노드에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 구성 파일의 위치 및 내용을 수정해야 합니다. 이렇게 하면 장애 조치(failover) 시 모든 노드에서 구성 파일과 패키지 저장소를 모두 사용할 수 있습니다. 구성 파일의 위치 및 내용을 수정한 후에는 서비스를 온라인 상태로 만들어야 합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 클러스터 리소스로 온라인 상태가 되게 합니다.  
  
 클러스터 또는 서버에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 구성한 후에는 DCOM 권한을 구성해야 클라이언트 컴퓨터에서 서비스에 연결할 수 있습니다. 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 자격 증명을 위임할 수 없습니다. 따라서 다음 조건에 해당하는 경우 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 msdb 데이터베이스에 저장된 패키지를 관리할 수 없습니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 별개의 서버 또는 가상 서버에서 실행 중입니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 실행하는 클라이언트가 세 번째 컴퓨터입니다.  
  
 클라이언트는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 실행 중인 가상 서버에 연결할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 가상 서버에 사용자의 자격 증명을 위임할 수 없습니다. 이를 이중 홉 시나리오라고 합니다.  
  
### <a name="to-install-integration-services-on-a-cluster"></a>클러스터에 Integration Services를 설치하려면  
  
1.  하나 이상의 노드를 사용하여 클러스터를 설치 및 구성합니다.  
  
2.  (옵션) [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 같은 클러스터형 서비스를 설치합니다.  
  
3.  클러스터의 각 노드에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치합니다.  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>Integration Services를 클러스터 리소스로 구성하려면  
  
1.  **클러스터 관리자**를 엽니다.  
  
2.  콘솔 트리에서 그룹 폴더를 선택합니다.  
  
3.  결과 창에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 추가하려는 그룹을 선택합니다.  
  
    -   Integrations Services를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 동일한 리소스 그룹에 클러스터 리소스로 추가하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 속한 그룹을 선택합니다.  
  
    -   Integrations Services를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 그룹에 클러스터 리소스로 추가하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 속한 그룹과 다른 그룹을 선택합니다.  
  
4.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **리소스**를 클릭합니다.  
  
5.  리소스 마법사의 **새 리소스** 페이지에서 이름을 입력하고 **서비스 유형**으로 **"일반 서비스"** 를 선택합니다. **그룹**값을 변경하지 마십시오. **다음**을 클릭합니다.  
  
6.  **가능한 소유자** 페이지에서 클러스터의 노드를 리소스의 가능한 소유자로 추가하거나 제거합니다. **다음**을 클릭합니다.  
  
7.  종속성을 추가하려면 **종속성** 페이지의 **사용 가능한 리소스**에서 리소스를 선택한 다음 **추가**를 클릭합니다. 장애 조치(failover)의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 저장하는 공유 디스크는 모두 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 온라인 상태가 되기 전에 온라인 상태가 되어야 합니다. 종속성을 선택한 후 **다음**을 클릭합니다.  
  
     자세한 내용은 [Add Dependencies to a SQL Server Resource](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)을(를) 참조하세요.  
  
8.  **일반 서비스 매개 변수** 페이지에서 **MsDtsServer** 를 서비스 이름으로 입력합니다. **다음**을 클릭합니다.  
  
9. **레지스트리 복제** 페이지에서 **추가** 를 클릭하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 구성 파일의 위치를 식별하는 레지스트리 키를 추가합니다. 이 파일은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스와 동일한 리소스 그룹에 있는 공유 디스크에 있어야 합니다.  
  
10. **레지스트리 키** 대화 상자에서 **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**을 입력합니다. **확인**을 클릭한 다음 **마침**을 클릭합니다.  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 클러스터 리소스로 추가됩니다.  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>Integration Services 서비스 및 패키지 저장소를 구성하려면  
  
1.  %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml에서 구성 파일을 찾아 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 추가한 그룹의 공유 디스크에 복사합니다.  
  
2.  공유 디스크에서 패키지 저장소로 사용할 **Packages** 라는 새 폴더를 만듭니다. 해당 사용자 및 그룹에 새 폴더에 대한 폴더 보기 및 쓰기 권한을 부여합니다.  
  
3.  공유 디스크에서 텍스트 편집기나 XML 편집기로 구성 파일을 엽니다. **ServerName** 요소의 값을 같은 리소스 그룹에 있는 가상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이름으로 변경합니다.  
  
4.  **StorePath** 요소의 값을 앞 단계에서 공유 디스크에 만든 **Packages** 폴더의 정규화된 경로로 변경합니다.  
  
5.  레지스트리의 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** 값을 공유 디스크의 정규화된 경로 및 서비스 구성 파일의 파일 이름에 업데이트합니다.  
  
### <a name="to-bring-the-integration-services-service-online"></a>Integration Services 서비스를 온라인 상태로 만들려면  
  
-   **클러스터 관리자**에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 선택하고 마우스 오른쪽 단추로 클릭한 다음 팝업 메뉴에서 **온라인 상태로 만들기** 를 선택합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 클러스터 리소스로 온라인 상태가 됩니다.  
  
  
