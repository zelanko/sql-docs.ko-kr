---
title: 보안 역할 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], roles
- Analysis Services objects, roles
- security [Analysis Services], roles
- roles [Analysis Services], about roles
- server roles [Analysis Services]
- database roles [Analysis Services]
- roles [Analysis Services]
- storing data [Analysis Services], roles
- access rights [Analysis Services], roles
ms.assetid: 5b7e9cef-ff68-4d8e-99bc-e0094ced1baa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4400755b5a117b16f56fe191cf0e2c80da03261c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164653"
---
# <a name="security-roles--analysis-services---multidimensional-data"></a>보안 역할(Analysis Services - 다차원 데이터)
  역할에 사용 됩니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 대 한 보안을 관리할 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체 및 데이터입니다. 역할 기본 측면에서 특정 액세스 권한과의 인스턴스에 의해 관리 되는 개체에 대해 정의 된 사용 권한이 있는 Microsoft Windows 사용자 및 그룹의 보안 식별자 (Sid)를 연결 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 두 가지 유형의 역할에 제공 됩니다 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:  
  
-   서버 역할 - 관리자에게 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]인스턴스에 대한 액세스 권한을 제공하는 고정 역할  
  
-   데이터베이스 역할 - 관리자가 아닌 사용자의 개체와 데이터에 대한 액세스 권한을 제어하기 위해 관리자가 정의하는 역할  
  
 보안 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 역할 및 권한을 사용 하 여 보안을 관리 합니다. 역할은 사용자 그룹이고 멤버라고도 하는 사용자는 역할에 추가하거나 역할에서 제거할 수 있습니다. 개체에 대한 사용 권한은 역할로 지정되며 역할에 있는 모든 멤버는 해당 역할에 사용 권한이 지정된 개체를 사용할 수 있습니다. 역할에 있는 모든 멤버는 개체에 대해 동일한 사용 권한을 갖습니다. 사용 권한은 개체에 따라 다를 수 있습니다. 각 개체에는 해당 개체에 부여된 권한으로 구성된 권한 컬렉션이 있으며, 개체에는 여러 권한 집합을 부여할 수 있습니다. 개체의 권한 컬렉션에 있는 각 사용 권한에는 단일 역할이 할당되어 있습니다.  
  
## <a name="role-and-role-member-objects"></a>역할 및 역할 멤버 개체  
 역할은 사용자(멤버) 컬렉션을 포함하는 개체입니다. 역할 정의에서 사용자의 멤버 자격 설정 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 역할에 의해 사용 권한이 할당되므로 사용자는 역할의 멤버여야 개체에 액세스할 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.Role> 개체는 이름, ID 및 멤버 매개 변수로 구성되어 있습니다. 멤버는 문자열 컬렉션입니다. 각 멤버에는 사용자 이름이 "domain\username" 형식으로 포함되어 있습니다. 이름은 역할 이름이 포함된 문자열이고 ID는 역할의 고유 식별자가 포함된 문자열입니다.  
  
### <a name="server-role"></a>서버 역할  
 합니다 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버 역할의 인스턴스를 Windows 사용자 및 그룹의 관리 액세스 권한을 정의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 이 역할의 멤버가 모두에 액세스할 수 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스 및 개체 인스턴스에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 다음 작업을 수행할 수 있습니다.  
  
-   SQL Server Management Studio 또는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]를 사용하여 데이터베이스 생성과 서버 수준 속성 설정과 같은 서버 수준 관리 작업을 수행합니다.  
  
-   AMO(Analysis Management Objects)를 사용하여 프로그래밍 방식으로 관리 작업을 수행합니다.  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스 역할을 유지 관리합니다.  
  
-   추적(Process 권한을 가진 데이터베이스 역할이 수행할 수 있는 이벤트 처리에 대한 추적은 제외)을 시작합니다.  
  
 모든 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에는 해당 인스턴스를 관리할 수 있는 사용자를 정의하는 서버 역할이 있습니다. 이 역할의 이름과 ID는 Administrators입니다. 데이터베이스 역할과는 달리 서버 역할은 삭제하거나 역할에 사용 권한을 추가 또는 제거할 수 없습니다. 즉, 사용자가 또는 인스턴스에 대 한 관리자가 아닌 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]자기 자신만의 해당 인스턴스에 대 한 서버 역할에 포함 되는지 여부에 따라 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
### <a name="database-roles"></a>데이터베이스 역할  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체와 데이터에 대 한 사용자 액세스를 정의 하는 데이터베이스 역할을 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스입니다. 데이터베이스 역할은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스에서 별개의 개체로 생성되고, 해당 역할이 생성된 데이터베이스에만 적용됩니다. Windows 사용자 및 그룹을 역할에 포함하는 작업은 관리자가 수행하며, 관리자는 해당 역할에 사용 권한을 정의하는 작업도 수행합니다.  
  
 역할의 사용 권한을 통해 멤버는 데이터베이스와 데이터베이스 내의 개체 및 데이터에 액세스하고 이를 관리할 수 있습니다. 각 사용 권한에는 하나 이상의 액세스 권한이 연결되어 있어서 이를 통해 데이터베이스의 특정 개체에 대한 액세스를 보다 세밀하게 제어할 수 있습니다.  
  
## <a name="permission-objects"></a>Permission 개체  
 사용 권한은 특정 역할을 수행하는 개체(큐브, 차원 등)와 관련이 있으며 멤버가 해당 개체에서 수행할 수 있는 작업을 지정합니다.  
  
 <xref:Microsoft.AnalysisServices.Permission> 클래스는 추상 클래스입니다. 따라서 해당 개체에 대한 사용 권한을 정의하려면 추상 클래스를 사용해야 합니다. 각 개체에는 권한 파생 클래스가 정의되어 있습니다.  
  
|Object|클래스|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 다음 목록에서는 권한에 의해 가능한 동작을 보여 줍니다.  
  
|작업|값|설명|  
|------------|------------|-----------------|  
|처리|{`true`, `false`}<br /><br /> 기본값은 `false`입니다.|`true`이면 멤버가 개체와 해당 개체에 포함된 모든 개체를 처리할 수 있습니다.<br /><br /> 처리 권한은 마이닝 모델에 적용되지 않습니다. <xref:Microsoft.AnalysisServices.MiningModel> 권한은 항상에서 상속 됩니다 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.|  
|ReadDefinition|{`None`, `Basic`, `Allowed`}<br /><br /> 기본값은 `None`입니다.|멤버가 개체와 연관된 데이터 정의(ASSL)를 읽을 수 있는지 여부를 지정합니다.<br /><br /> `Allowed`이면 멤버가 개체와 연관된 ASSL을 읽을 수 있습니다.<br /><br /> `Basic` 및 `Allowed` 개체에 포함 된 개체에 의해 상속 됩니다. `Allowed` 재정의 `Basic` 고 `None`입니다.<br /><br /> `Allowed`는 개체의 DISCOVER_XML_METADATA에 필요하고 `Basic` 연결 된 개체와 로컬 큐브를 만드는 필요 합니다.|  
|읽기|{`None`, `Allowed`}<br /><br /> 기본 =`None` (dimensionpermission, 기본값 =`Allowed`)|멤버가 스키마 행 집합과 데이터 콘텐츠를 읽을 수 있는 권한을 가지고 있는지 여부를 지정합니다.<br /><br /> `Allowed` 데이터베이스를 검색할 수 있도록 하는 데이터베이스에 대 한 읽기 액세스를 제공 합니다.<br /><br /> 큐브에 대한 `Allowed`는 스키마 행 집합에 대한 읽기 액세스 권한과 큐브 콘텐츠에 대한 액세스 권한을 부여합니다(<xref:Microsoft.AnalysisServices.CellPermission> 및 <xref:Microsoft.AnalysisServices.CubeDimensionPermission>에 의해 제한되지 않는 경우에 한해).<br /><br /> 차원에 대한 `Allowed`는 차원에 있는 모든 특성을 읽을 수 있는 권한을 부여합니다(<xref:Microsoft.AnalysisServices.CubeDimensionPermission>에 의해 제한되지 않는 경우에 한해). 읽기 권한은 <xref:Microsoft.AnalysisServices.CubeDimensionPermission>에 대한 정적 상속에만 사용됩니다. 차원에 대한 `None`은 차원을 숨기고 집계할 수 있는 특성의 기본 멤버에만 액세스 권한을 부여합니다. 따라서 차원에 집계할 수 없는 특성이 포함되어 있으면 오류가 발생합니다.<br /><br /> <xref:Microsoft.AnalysisServices.MiningModelPermission>에 대한 `Allowed`는 행 집합에 있는 개체를 보고 예측 조인을 수행할 수 있는 사용 권한을 부여합니다.<br /><br /> **NoteAllowed** 읽기 또는 쓰기 데이터베이스의 모든 개체에 필요 합니다.|  
|쓰기|{`None`, `Allowed`}<br /><br /> 기본값은 `None`입니다.|멤버가 부모 개체의 데이터에 대한 쓰기 액세스 권한을 가지고 있는지 여부를 지정합니다.<br /><br /> 액세스 권한은 <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube> 및 <xref:Microsoft.AnalysisServices.MiningModel> 하위 클래스에 적용되고 데이터베이스에 적용 되지 않습니다 <xref:Microsoft.AnalysisServices.MiningStructure> 유효성 검사 오류를 생성 하는 하위 클래스입니다.<br /><br /> <xref:Microsoft.AnalysisServices.Dimension>에 대한 `Allowed`는 차원에 있는 모든 특성에 대한 쓰기 권한을 부여합니다.<br /><br /> <xref:Microsoft.AnalysisServices.Cube>에 대한 `Allowed`는 Type=writeback으로 정의된 파티션의 큐브 셀에 대한 쓰기 권한을 부여합니다.<br /><br /> <xref:Microsoft.AnalysisServices.MiningModel>에 대한 `Allowed`는 모델 콘텐츠를 수정할 수 있는 사용 권한을 부여합니다.<br /><br /> `Allowed` 에 <xref:Microsoft.AnalysisServices.MiningStructure> 특별 한 의미가 없습니다에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]입니다. **참고:** 쓰기로 설정할 수 없습니다 `Allowed` 읽기도 설정 되지 않은 경우 `Allowed`|  
|관리할 **참고:** 데이터베이스 사용 권한 에서만|{`true`, `false`}<br /><br /> 기본값은 `false`입니다.|멤버가 데이터베이스를 관리할 수 있는지 여부를 지정합니다.<br /><br /> `true` 멤버 데이터베이스의 모든 개체에 대 한 액세스 권한을 부여합니다.<br /><br /> 멤버는 특정 데이터베이스에 대해서만 관리 권한을 가질 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [개체 및 작업에 대 한 액세스 권한 부여 &#40;Analysis Services&#41;](../authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
