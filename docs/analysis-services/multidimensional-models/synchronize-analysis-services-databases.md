---
title: Analysis Services 데이터베이스 동기화 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1400d43f2736505e0b9ba2364909986d47923da
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145918"
---
# <a name="synchronize-analysis-services-databases"></a>Analysis Services 데이터베이스 동기화
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에는 원본 서버의 데이터베이스에 있는 데이터와 메타데이터를 대상 서버의 데이터베이스로 복사하여 두 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 동일하게 만드는 데이터베이스 동기화 기능이 포함되어 있습니다. 데이터베이스 동기화 기능을 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   준비 서버에서 프로덕션 서버로 데이터베이스를 배포합니다.  
  
-   준비 서버의 데이터베이스에 있는 데이터와 메타데이터의 변경 내용을 반영하도록 프로덕션 서버의 데이터베이스를 업데이트합니다.  
  
-   이후에 데이터베이스를 동기화할 때 실행할 수 있는 XMLA 스크립트를 생성합니다.  
  
-   큐브와 차원이 여러 서버에서 처리되는 분산된 작업에서 데이터베이스 동기화를 사용하여 변경 내용을 단일 데이터베이스에 병합합니다.  
  
 데이터베이스 동기화는 대상 서버에서 시작되어 데이터와 메타데이터를 원본 서버의 데이터베이스 복사본으로 끌어옵니다. 데이터베이스가 없으면 새로 만들어집니다. 동기화는 데이터베이스가 복사되면 종료되는 1회성 단방향 작업으로, 데이터베이스 간의 실시간 패리티를 제공하지 않습니다.  
  
 원본 및 대상 서버에 이미 있는 데이터베이스를 다시 동기화하여 최신 변경 내용을 준비 서버에서 프로덕션 데이터베이스로 끌어올 수 있습니다. 두 서버의 파일이 변경 내용에 대해 비교되고 변경 내용과 다른 파일은 업데이트됩니다. 대상 서버의 기존 데이터베이스는 동기화가 백그라운드에서 실행되는 동안 계속 사용할 수 있습니다. 동기화가 진행되는 동안 사용자가 계속해서 대상 데이터베이스를 쿼리할 수 있습니다. 동기화가 완료되면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 새로 복사된 데이터 및 메타데이터로 사용자를 자동으로 전환하고 대상 데이터베이스에서 이전 데이터를 삭제합니다.  
  
 데이터베이스를 동기화하려면 데이터베이스 동기화 마법사를 실행하여 데이터베이스를 즉시 동기화하거나, 데이터베이스 동기화 마법사를 사용하여 나중에 실행할 수 있는 동기화 스크립트를 생성합니다. 어느 방법이든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 및 큐브의 가용성과 확장성을 높이는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  이전 버전의 Analysis Services용으로 작성된 다음 백서는 SQL Server 2012를 사용하여 구축된 확장 가능한 다차원 솔루션에도 적용됩니다. 자세한 내용은 [Analysis Services의 쿼리 확장](http://go.microsoft.com/fwlink/?LinkId=253136) 및 [읽기 전용 데이터베이스로 Analysis Services의 쿼리 확장](http://go.microsoft.com/fwlink/?LinkId=253137.)을 참조하세요.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 데이터베이스 동기화를 시작하는 대상 서버에서 Analysis Services 서버 관리자 역할의 멤버여야 합니다. 원본 서버에서 Windows 사용자 계정에 원본 데이터베이스에 대한 모든 권한이 있어야 합니다. 데이터베이스를 대화형으로 동기화하는 경우 동기화가 Windows 사용자 ID의 보안 컨텍스트에서 실행됩니다. 특정 개체에 대한 계정의 액세스가 거부되는 경우 해당 개체가 작업에서 제외됩니다. 서버 관리자 역할 및 데이터베이스 권한에 대한 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 및 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)를 참조하세요.  
  
 TCP 포트 2383이 기본 인스턴스 간의 원격 연결을 허용하기 위해 두 서버에서 열려 있어야 합니다. Windows 방화벽에서 예외를 만드는 방법은 [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하십시오.  
  
 원본 및 대상 서버는 동일한 버전 및 서비스 팩 이어야 합니다. 모델 메타 데이터 동기화도 되어 있으므로 빌드 호환성을 위해 두 서버 모두에 대 한 번호 동일 해야 합니다. 각 설치 버전이 데이터베이스 동기화를 지원해야 합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 데이터베이스 동기화가 Enterprise, Developer 및 Business Intelligence 버전에서 지원됩니다. 각 버전의 기능에 대 한 자세한 내용은 참조 하세요. [버전 및 SQL Server 2016에 대 한 지원 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)합니다.  
  
 서버 배포 모드는 각 서버에서 동일해야 합니다. 동기화할 데이터베이스가 다차원인 경우 원본 서버와 대상 서버가 다차원 서버 모드에 대해 구성되어야 합니다. 배포 모드에 대한 자세한 내용은 [Determine the Server Mode of an Analysis Services Instance](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하십시오.  
  
 원본 서버에서 지연 집계 처리를 사용하는 경우 지연 집계 처리를 해제합니다. 백그라운드에서 처리되고 있는 집계는 데이터베이스 동기화에 방해가 될 수 있습니다. 이 서버 속성을 설정하는 방법은 [OLAP Properties](../../analysis-services/server-properties/olap-properties.md)을 참조하십시오.  
  
> [!NOTE]  
>  데이터베이스 크기는 동기화가 적합한 방식인지 결정하는 요소입니다. 까다로운 요구 사항은 없지만 동기화가 너무 느리면 [Analysis Services 동기화 모범 사례](http://go.microsoft.com/fwlink/?LinkID=253136)문서에 설명된 대로 여러 서버를 병렬로 동기화하는 것이 좋습니다.  
  
## <a name="synchronize-database-wizard"></a>데이터베이스 동기화 마법사  
 데이터베이스 동기화 마법사를 사용하여 원본 데이터베이스에서 대상 데이터베이스로 단방향 동기화를 수행하거나 데이터베이스 동기화 작업을 지정하는 스크립트를 생성할 수 있습니다. 동기화 프로세스 중에 로컬 및 원격 파티션을 둘 다 동기화하고 역할을 포함할지 여부를 선택할 수 있습니다.  
  
 데이터베이스 동기화 마법사는 다음 단계로 이루어져 있습니다.  
  
-   동기화할 원본 인스턴스 및 데이터베이스를 선택합니다.  
  
-   대상 인스턴스의 로컬 파티션에 대한 스토리지 위치를 선택합니다.  
  
-   다른 대상 인스턴스의 원격 파티션에 대한 스토리지 위치를 선택합니다.  
  
-   원본 인스턴스 및 데이터베이스에서 대상 인스턴스로 복사할 보안 수준 및 멤버 정보를 선택합니다.  
  
-   즉시 동기화할지, 아니면 나중에 동기화할 수 있도록 데이터베이스 동기화 마법사에서 생성한 XMLA(XML for Analysis) **동기화** 명령을 스크립트 파일에 저장할지를 선택합니다.  
  
 기본적으로 마법사는 기존 보안 그룹의 멤버 이외의 모든 데이터와 메타데이터를 동기화합니다. 또한 데이터와 메타데이터를 동기화할 때 모든 보안 설정을 복사하거나 모든 보안 설정을 무시할 수 있습니다.  
  
#### <a name="run-the-wizard"></a>마법사 실행  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 대상 데이터베이스를 실행할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다. 예를 들어 프로덕션 서버에 데이터베이스를 배포하는 경우 프로덕션 서버에서 마법사를 실행합니다.  
  
2.  개체 탐색기에서 **데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **동기화**를 클릭합니다.  
  
3.  원본 서버와 원본 데이터베이스를 지정합니다. 동기화할 데이터베이스 선택 페이지의 **원본 서버** 및 **원본 데이터베이스**에 원본 서버와 원본 데이터베이스의 이름을 입력합니다. 예를 들어 테스트 환경에서 프로덕션 서버로 배포하는 경우 원본은 준비 서버의 데이터베이스입니다.  
  
     **대상 서버** 에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 원본 데이터베이스 **에서 선택한 데이터베이스의 데이터 및 메타데이터와 동기화되는** 인스턴스의 이름이 표시됩니다.  
  
     이름이 같은 원본 및 대상 데이터베이스에 대해 동기화가 수행됩니다. 대상 서버에 원본 데이터베이스와 이름이 동일한 데이터베이스가 이미 있을 경우 대상 데이터베이스는 원본의 메타데이터와 데이터를 사용하여 업데이트됩니다. 데이터베이스가 존재하지 않을 경우 대상 서버에 생성됩니다.  
  
4.  (옵션) 로컬 파티션의 위치를 변경합니다. **로컬 파티션의 위치 지정** 페이지를 사용하여 로컬 파티션이 대상 서버에 저장될 위치를 나타냅니다.  
  
    > [!NOTE]  
    >  이 페이지는 지정한 데이터베이스에 하나 이상의 로컬 파티션이 있는 경우에만 나타납니다.  
  
     원본 서버의 C 드라이브에 일련의 파티션이 설치된 경우 마법사를 사용하여 이 일련의 파티션을 대상 서버의 다른 위치에 복사할 수 있습니다. 기본 위치를 변경하지 않으면 마법사가 원본 서버의 각 큐브 내에 있는 측정값 그룹 파티션을 대상 서버의 동일 위치에 배포합니다. 이와 비슷하게 원본 서버에서 원격 파티션이 사용되는 경우 대상 서버에서도 동일한 원격 파티션이 사용됩니다.  
  
     **위치** 옵션은 대상 인스턴스에 저장될 로컬 파티션의 원본 폴더, 대상 폴더, 예상 크기 등을 표 형태로 표시합니다. 표에는 다음 열이 있습니다.  
  
     **원본 폴더**  
     로컬 파티션을 포함하는 원본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 폴더 이름을 표시합니다. 열에 "(기본값)" 값이 있으면 원본 인스턴스의 기본 위치에 로컬 파티션이 포함됩니다.  
  
     **대상 폴더**  
     로컬 파티션을 동기화할 대상 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 폴더 이름을 표시합니다. 열에 "(기본값)" 값이 있으면 대상 인스턴스의 기본 위치에 로컬 파티션이 포함됩니다.  
  
     **원격 폴더 찾아보기**대화 상자를 표시하고 선택한 위치에 저장된 로컬 파티션을 동기화할 대상 인스턴스의 폴더를 지정하려면 줄임표( **...** ) 단추를 클릭합니다.  
  
    > [!NOTE]  
    >  원본 인스턴스의 기본 위치에 저장된 로컬 파티션에 대해서는 이 열을 변경할 수 없습니다.  
  
     **크기**  
     로컬 파티션의 예상 크기를 표시합니다.  
  
     **선택한 위치의 파티션** 옵션은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 위치 **에서 선택한 열의** 원본 폴더 **에서 지정한 원본**인스턴스의 위치에 저장된 로컬 파티션을 설명하는 표를 표시합니다.  
  
     **Cube**  
     파티션이 포함된 큐브의 이름을 표시합니다.  
  
     **측정값 그룹**  
     파티션이 포함된 큐브의 측정값 그룹 이름을 표시합니다.  
  
     **파티션 이름**  
     파티션 이름을 표시합니다.  
  
     **크기(MB)**  
     파티션의 크기(MB)를 표시합니다.  
  
5.  (옵션) 원격 파티션의 위치를 변경합니다. **원격 파티션 위치 지정** 페이지를 사용하여 원본 서버의 지정된 데이터베이스에서 관리하는 원격 파티션을 동기화할지 여부를 나타내고 선택한 원격 파티션을 저장할 대상 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 및 데이터베이스를 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  이 페이지는 원본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 지정된 데이터베이스에서 하나 이상의 원격 파티션을 관리하는 경우에만 표시됩니다.  
  
     **위치** 옵션은 선택한 데이터베이스에서 사용할 수 있는 원본 및 대상 정보와 각 위치에서 사용하는 저장소 크기를 포함하여 원본 데이터베이스의 원격 파티션이 저장된 위치와 관련한 세부 정보를 나열하는 표를 표시합니다. 표에는 다음 열이 있습니다.  
  
     **동기화**  
     원격 파티션이 있는 해당 위치를 동기화에 포함시키려면 선택합니다.  
  
    > [!NOTE]  
    >  위치에 대해 이 옵션을 선택하지 않은 경우 해당 위치에 포함된 원격 파티션은 동기화되지 않습니다.  
  
     **원본 서버**  
     원격 파티션을 포함하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 이름을 표시합니다.  
  
     **원본 폴더**  
     원격 파티션을 포함하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 폴더 이름을 표시합니다. 열에 "(기본값)"이 있으면 **원본 서버** 에 표시되는 인스턴스에 대한 기본 위치에 원격 파티션이 포함됩니다.  
  
     **대상 서버**  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 원본 서버 **및** 원본 폴더 **에서 지정한 위치에 저장된 원격 파티션이 동기화될** 인스턴스의 이름을 표시합니다.  
  
     **연결 관리자**대화 상자를 표시하고 선택한 위치에 저장된 원격 파티션을 동기화할 **인스턴스를 지정하려면 줄임표(** ... [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) 단추를 클릭합니다.  
  
     **대상 폴더**  
     원격 파티션을 동기화할 대상 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 폴더 이름을 표시합니다. 열에 "(기본값)"이 있으면 대상 인스턴스에 대한 기본 위치에 원격 파티션이 포함됩니다.  
  
     **원격 폴더 찾아보기**대화 상자를 표시하고 선택한 위치에 저장된 원격 파티션을 동기화할 대상 인스턴스의 폴더를 지정하려면 줄임표( **...** ) 단추를 클릭합니다.  
  
     **크기**  
     위치에 저장된 원격 파티션의 예상 크기를 표시합니다.  
  
     **선택한 위치의 파티션** 은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 위치 **에서 선택한 행의** 원본 폴더 **열에서 지정한 원본**인스턴스의 위치에 저장된 원격 파티션을 설명하는 표를 표시합니다. 표에는 다음 열이 있습니다.  
  
     **Cube**  
     파티션이 포함된 큐브의 이름을 표시합니다.  
  
     **측정값 그룹**  
     파티션이 포함된 큐브의 측정값 그룹 이름을 표시합니다.  
  
     **파티션 이름**  
     파티션 이름을 표시합니다.  
  
     **크기(MB)**  
     파티션의 크기(MB)를 표시합니다.  
  
6.  사용자 권한 정보가 포함되어야 할지 여부와 압축을 사용해야 할지 여부를 지정합니다. 기본적으로 마법사는 파일을 대상 서버에 복사하기 전에 모든 데이터 및 메타데이터를 압축합니다. 이 옵션을 사용하면 파일 전송이 빨라집니다. 파일이 대상 서버에 도달하면 파일의 압축이 해제됩니다.  
  
     **모두 복사**  
     동기화 중에 보안 정의 및 멤버 등록 정보를 포함하려면 선택합니다.  
  
     **멤버 등록 생략**  
     동기화 중에 멤버 등록 정보는 제외하고 보안 정의만 포함하려면 선택합니다.  
  
     **모두 무시**  
     원본 데이터베이스에 현재 있는 보안 정의 및 멤버 자격 정보를 무시하도록 선택합니다. 대상 데이터베이스가 동기화 중에 만들어진 경우 보안 정의나 멤버 자격 정보가 복사되지 않습니다. 대상 데이터베이스가 이미 존재하고 역할 및 멤버 자격이 있는 경우 해당 보안 정보가 유지됩니다.  
  
7.  동기화 방법을 선택합니다. 즉시 동기화하거나 파일에 저장된 스크립트를 생성할 수 있습니다. 기본적으로 파일은 .xmla 확장명으로 저장되고 Documents 폴더에 배치됩니다.  
  
8.  **마침** 을 클릭하여 동기화를 시작합니다. **마법사 완료** 페이지의 옵션을 확인하고 **마침** 을 다시 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 역할 또는 멤버 자격을 동기화하지 않은 경우 지금 대상 데이터베이스에 대한 사용자 액세스 권한을 지정해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Synchronize 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [XMLA를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [배포 마법사를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
