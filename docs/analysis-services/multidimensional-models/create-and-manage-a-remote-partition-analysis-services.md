---
title: "원격 파티션 (Analysis Services) 만들기 및 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [Analysis Services], remote
- remote partitions [Analysis Services]
ms.assetid: 4322b5cb-af07-4e79-8ecb-59e1121a9eb8
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f5c1dc173a2ea724f7542e5ca1f862b4d9df0dad
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-manage-a-remote-partition-analysis-services"></a>원격 파티션 만들기 및 관리(Analysis Services)
  측정값 그룹을 분할할 때 원격 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 보조 데이터베이스를 파티션 저장소로 구성할 수 있습니다.  
  
 master 데이터베이스라는 큐브의 원격 파티션은 보조 데이터베이스라는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 원격 인스턴스에 있는 전용 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 저장됩니다.  
  
 전용 보조 데이터베이스는 단 하나의 master 데이터베이스에 대한 원격 파티션을 저장할 수 있지만 모든 보조 데이터베이스가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 동일한 원격 인스턴스에 있는 경우 master 데이터베이스는 여러 보조 데이터베이스를 사용할 수 있습니다. 원격 파티션 전용 데이터베이스의 차원은 연결된 차원으로 생성됩니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 원격 파티션을 만들기 전에 다음 조건이 충족되어야 합니다.  
  
-   파티션을 저장하려면 두 번째 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 전용 데이터베이스가 있어야 합니다. 보조 데이터베이스는 master 데이터베이스에 원격 파티션 저장소를 제공하는 한 가지 용도로 사용됩니다.  
  
-   두 서버 인스턴스가 같은 버전이어야 합니다. 두 데이터베이스는 동일한 기능 수준이어야 합니다.  
  
-   두 인스턴스는 TCP 연결에 맞게 구성되어야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 HTTP 프로토콜을 사용하여 원격 파티션을 만드는 작업을 지원하지 않습니다.  
  
-   두 컴퓨터 모두 방화벽 설정이 외부 연결을 허용하도록 설정되어야 합니다. 방화벽을 설정하는 방법에 대한 자세한 내용은 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
-   master 데이터베이스를 실행하는 인스턴스의 서비스 계정은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 원격 인스턴스에 대한 관리 액세스 권한을 가져야 합니다. 서비스 계정이 변경되면 서버 및 데이터베이스에 대한 사용 권한을 업데이트해야 합니다.  
  
-   두 컴퓨터의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자여야 합니다.  
  
-   재해 복구 계획이 원격 파티션의 백업 및 복원에 적합한지 확인해야 합니다. 원격 파티션을 사용하면 백업 및 복원 작업이 복잡해질 수 있습니다. 필요한 데이터를 복원할 수 있도록 계획을 철저히 테스트해야 합니다.  
  
## <a name="configure-remote-partitions"></a>원격 파티션 구성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스를 실행하는 별도의 두 컴퓨터는 각각 한 컴퓨터는 마스터 서버로 지정하고 다른 컴퓨터는 하위 서버로 지정하는 원격 파티션 배열을 만드는 데 필요합니다.  
  
 다음 절차에서는 마스터 서버에 배포된 큐브 데이터베이스가 있는 두 개의 서버 인스턴스가 있다고 가정합니다. 이 절차에서는 큐브 데이터베이스를 db 마스터라고 합니다. 원격 파티션을 포함하는 저장소 데이터베이스는 db 저장소라고 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 이 절차를 완료합니다.  
  
> [!NOTE]  
>  원격 파티션은 다른 원격 파티션과만 병합할 수 있습니다. 로컬 파티션과 원격 파티션을 조합하여 사용하는 경우 다른 방법은 더 이상 사용하지 않는 파티션을 삭제하여 결합된 데이터를 포함하는 새 파티션을 만드는 것입니다.  
  
#### <a name="specify-valid-server-names-for-cube-deployment-in-ssdt"></a>SSDT의 큐브 배포에 대한 올바른 서버 이름 지정  
  
1.  마스터 서버: 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **속성** 대화 상자에서 **구성 속성**을 클릭한 다음 **배포**를 클릭하고 **서버** 를 클릭한 다음 마스터 서버 이름을 설정합니다.  
  
2.  종속 서버: 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **속성** 대화 상자에서 **구성 속성**을 클릭한 다음 **배포**를 클릭하고 **서버** 를 클릭한 다음 하위 서버 이름을 설정합니다.  
  
#### <a name="create-and-deploy-a-secondary-database-in-ssdt"></a>SSDT의 보조 데이터베이스 만들기 및 배포  
  
1.  종속 서버: 저장소 데이터베이스용으로 새 Analysis Services 프로젝트를 만듭니다.  
  
2.  종속 서버: 솔루션 탐색기에서 큐브 데이터베이스 db-master를 가리키는 새 데이터 원본을 만듭니다. **네이티브 OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0**공급자를 사용합니다.  
  
3.  종속 서버: 솔루션을 배포합니다.  
  
#### <a name="enable-features-in-ssms"></a>기능 활성화(SSMS)  
  
1.  종속 서버: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 연결된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **Feature\LinkToOtherInstanceEnabled** 및 **Feature\LinkFromOtherInstanceEnabled** 를 **True**로 설정합니다.  
  
2.  종속 서버: 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 선택하여 서버를 다시 시작합니다.  
  
3.  마스터 서버: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 연결된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **Feature\LinkToOtherInstanceEnabled** 및 **Feature\LinkFromOtherInstanceEnabled** 를 **True**로 설정합니다.  
  
4.  마스터 서버: 서버를 다시 시작하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 선택합니다.  
  
#### <a name="set-the-masterdatasourceid-database-property-on-the-remote-server-in-ssms"></a>원격 서버에서 MasterDataSourceID 데이터베이스 속성 설정(SSMS)  
  
1.  종속 서버: 저장소 데이터베이스 db-storage를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 스크립팅** | **ALTER** | **새 쿼리 편집기 창**을 가리킵니다.  
  
2.  XMLA에 **MasterDataSourceID** 를 추가한 다음 큐브 데이터베이스(db 마스터) ID를 값으로 지정합니다. XMLA는 다음과 비슷해야 합니다.  
  
    ```  
    <Alter ObjectExpansion="ExpandFull" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
       <DatabaseID>DB-Storage</DatabaseID>  
    </Object>  
    <ObjectDefinition>  
       <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" 400"   
          <ID>DB-Storage</ID>  
          <Name>DB-StorageB</Name>  
          <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
          <Language>1033</Language>  
          <Collation>Latin1_General_CI_AS</Collation>  
          <DataSourceImpersonationInfo>  
    <ImpersonationMode>ImpersonateAccount</ImpersonationMode>  
             <Account>*********</Account>  
          </DataSourceImpersonationInfo>  
          <MasterDataSourceID>DB-Master</MasterDataSourceID>  
       </Database>  
    </ObjectDefinition>  
    </Alter>  
    ```  
  
3.  F5 키를 눌러 스크립트를 실행합니다.  
  
#### <a name="set-up-the-remote-partition-in-ssdt"></a>원격 파티션 설정(SSDT)  
  
1.  마스터 서버: 큐브 디자이너에서 큐브를 열고 **파티션** 탭을 클릭합니다. 측정값 그룹을 확장합니다. 측정값 그룹이 이미 여러 파티션에 맞게 구성되어 있는 경우 **새 파티션** 을 클릭하거나 원본 열에서 찾아보기(. 의 동일한 원격 인스턴스에 있는 경우 master 데이터베이스는 여러 보조 데이터베이스를 사용할 수 있습니다. ) 단추를 클릭하여 기존 파티션을 편집합니다.  
  
2.  파티션 마법사의 **원본 정보 지정**에서 원래 데이터 원본 뷰 및 팩트 테이블을 선택합니다.  
  
3.  쿼리 바인딩을 사용하는 경우 만드는 새 파티션의 데이터를 분할하는 WHERE 절을 제공합니다.  
  
4.  **처리 및 저장소 위치**의 **처리 위치**에서 **원격 Analysis Services 데이터 원본** 을 선택하고 **새로 만들기** 를 클릭하여 하위 데이터베이스(db 저장소)를 가리키는 새 데이터 원본을 만듭니다.  
  
    > [!NOTE]  
    >  컬렉션에 데이터 원본이 없음을 나타내는 오류가 표시되면 저장소 데이터베이스(db 저장소)의 프로젝트를 열고 master 데이터베이스(db 마스터)를 가리키는 데이터 원본을 만듭니다.  
  
5.  마스터 서버: 솔루션 탐색기에서 큐브 이름을 마우스 오른쪽 단추로 클릭하고 **처리** 를 선택하여 큐브를 전체 처리합니다.  
  
## <a name="administering-remote-partitions"></a>원격 파티션 관리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 원격 파티션의 병렬 및 순차적 처리를 지원합니다. 파티션이 정의된 master 데이터베이스는 큐브의 파티션 처리에 참여하는 모든 인스턴스 간의 트랜잭션을 조정합니다. 그런 다음 파티션을 처리한 모든 인스턴스에 처리 보고서가 전송됩니다.  
  
 원격 파티션을 포함하는 큐브는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 단일 인스턴스에 있는 해당 파티션과 함께 관리할 수 있습니다. 하지만 원격 파티션에 대한 메타데이터는 파티션과 부모 큐브가 정의된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스에서만 보고 업데이트할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 원격 인스턴스에서 원격 파티션을 보거나 업데이트할 수 없습니다.  
  
> [!NOTE]  
>  원격 파티션 저장에 전용되는 데이터베이스는 스키마 행 집합에 노출되지 않지만, AMO(Analysis Management Objects)를 사용하는 응용 프로그램은 Analysis Discover 명령에 대한 XML을 사용하여 전용 데이터베이스를 검색할 수 있습니다. TCP 또는 HTTP 클라이언트를 사용하여 전용 데이터베이스에 직접 전송되는 CREATE 또는 DELETE 명령은 성공하지만, 이 동작을 수행하면 면밀하게 관리되는 이 데이터베이스가 손상될 수 있음을 알리는 경고가 서버에서 반환됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [파티션&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  

