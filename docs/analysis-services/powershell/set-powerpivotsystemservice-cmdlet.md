---
title: Set-powerpivotsystemservice cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: f6ef197b-3d74-4339-ae73-8a7c1eaf0e91
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6157a4fc3b43c1a7dad7805c3efa5677d85b4d66
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-powerpivotsystemservice-cmdlet"></a>Set-PowerPivotSystemService cmdlet
  
  [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]
  
  PowerPivotSystemService 개체의 팜 수준 전역 속성을 설정합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
Set-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [-UpdateAssemblyInformation <switch>] [-WorkbookUpgradeOnDataRefresh <boolean>] [-DirectTCPConnections <boolean>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Set-PowerPivotSystemService cmdlet은 팜에 있는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 부모 개체의 속성을 업데이트합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>Id \<PowerPivotMidTierServicePipeBind >  
 속성을 업데이트할 부모 개체를 지정합니다. 팜에서 개체를 고유하게 식별하는 유효한 GUID 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="-updateassemblyinformation-switch"></a>-UpdateAssemblyInformation \<전환 >  
 업그레이드 목적으로만 사용합니다. 팜에 배포된 어셈블리 버전이 SharePoint 구성 데이터베이스에 저장된 버전과 다를 경우 이 cmdlet을 실행하여 구성 데이터베이스에 있는 어셈블리 정보를 업데이트할 수 있습니다. 어셈블리 버전 정보는 전역 어셈블리에 저장된 Microsoft.AnalysisServices.SharePoint.Integration.dll의 파일 속성에서 찾을 수 있습니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-workbookupgradeondatarefresh-boolean"></a>-WorkbookUpgradeOnDataRefresh \<부울 >  
 서버에서 예약된 데이터 새로 고침이 시작될 때 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 통합 문서를 자동으로 업그레이드하는 데 사용합니다. 데이터 새로 고침은 현재 서버 버전과 일치하는 통합 문서에 대해서만 지원됩니다. 이 속성을 사용으로 설정하면 데이터 새로 고침이 계속될 수 있도록 통합 문서가 자동으로 업그레이드됩니다. 이 속성은 서버 인스턴스 수준에서 설정됩니다. 이 속성은 통합 문서, 라이브러리, 사이트 또는 사용자별로 다르게 설정할 수 없습니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|2|  
|기본값|false|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-directtcpconnections-boolean"></a>-실행 \<부울 >  
 Excel Services가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스로 전송되는 모든 쿼리 요청에 사용되는 MSOLAP 데이터 공급자와 채널 전송을 무시하고 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스를 로드한 SQL Server Analysis Services(POWERPIVOT) 인스턴스로 모든 쿼리를 직접 보내도록 지정합니다.  
  
 이 매개 변수를 설정하면 로드된 데이터베이스에 대한 연결 효율성이 개선되어 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 쿼리의 성능과 확장성이 향상됩니다. 이 매개 변수는 초기 로드 요청이 할당되는 방식은 변경하지 않습니다. –DirectTCPConnections는 데이터베이스가 로드된 후에 실행된 쿼리에만 적용되므로 데이터베이스 로드 요청을 팜의 여러 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스에 할당하는 데 사용되는 –RoundRobinAllocation 및 –HealthBasedAllocation 등의 다른 매개 변수는 영향을 받지 않습니다.  
  
 Excel Services 및 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 서로 다른 응용 프로그램 서버에서 실행되는 팜 토폴로지의 경우 요청이 SQL Server Analysis Services(POWERPIVOT) 인스턴스에 도달할 수 있도록 방화벽에서 포트를 열어야 합니다. Analysis Services의 명명된 인스턴스에 대해 인바운드 연결을 설정하는 방법은 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|3|  
|기본값|false|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-confirm-switch"></a>-확인 \<전환 >  
 명령을 실행하기 전 확인 메시지를 표시합니다. 이 값은 기본적으로 설정되어 있습니다. 명령에서 확인 응답을 무시하려면 명령에 Confirm:$false를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## <a name="example-1"></a>예 1  
  
```  
C:\PS>Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true  
```  
  
 예약된 데이터 새로 고침이 계속될 수 있도록 이전 버전 통합 문서를 자동 업그레이드하도록 설정합니다.  
  
  

