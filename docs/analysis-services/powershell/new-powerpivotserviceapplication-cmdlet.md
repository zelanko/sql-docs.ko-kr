---
title: New-powerpivotserviceapplication cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7bb2a2d2-04c8-43d4-a0fc-e8339ea22138
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ca76f83816a3936f07e58e2f70990aeed221c262
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="new-powerpivotserviceapplication-cmdlet"></a>New-PowerPivotServiceApplication cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]원본 또는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램입니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 New-PowerPivotServiceApplication cmdlet은 팜에 새 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 만듭니다. 서비스 응용 프로그램을 적어도 하나 이상 정의하고 기본 프록시 서비스 그룹의 멤버로 추가해야 합니다. 필요에 따라 속성 또는 구성 설정을 다르게 해야 할 경우 추가 서비스 응용 프로그램을 만들 수 있습니다. 추가 서비스 응용 프로그램은 사용자 지정 서비스 연결 그룹의 멤버로 할당해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 하나만 기본 프록시 그룹의 멤버가 될 수 있습니다.  
  
 새 서비스 응용 프로그램은 기본 구성을 사용하여 만들어집니다. 구성 속성을 사용자 지정하려면 Set-PowerPivotServiceApplication cmdlet을 사용합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-serviceapplicationname-string"></a>-ServiceApplicationName \<문자열 >  
 서비스 응용 프로그램의 표시 이름을 설정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-databaseservername-string"></a>-DatabaseServerName \<문자열 >  
 응용 프로그램 데이터베이스를 호스팅하는 SQL Server 관계형 데이터베이스 엔진 인스턴스를 지정합니다. 기본적으로 팜의 데이터베이스 서버를 사용하거나, 데이터베이스 권한을 만들 다른 데이터베이스 서버를 선택할 수 있습니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-databasename-string"></a>-DatabaseName \<문자열 >  
 응용 프로그램 데이터를 저장하는 SQL Server 관계형 데이터베이스의 이름을 지정합니다. 응용 프로그램의 용도를 쉽게 알아볼 수 있도록 응용 프로그램에 적합한 이름을 지정해야 합니다. 새로 만드는 응용 프로그램에 대해 새 데이터베이스를 만들거나 기존 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스를 지정할 수 있습니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-addtodefaultproxygroup-switch"></a>-AddToDefaultProxyGroup \<전환 >  
 기본 서비스 연결 그룹에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 연결을 만듭니다. 웹 응용 프로그램과 서비스 응용 프로그램 간의 연결은 이 그룹의 멤버인지 여부에 따라 결정됩니다. 기본 서비스 연결 그룹을 구독하는 모든 웹 응용 프로그램은 그룹에 추가된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 사용할 수 있습니다. 팜에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 여러 개 포함할 수는 있지만 그 중 하나만 기본 서비스 연결 그룹의 멤버로 지정할 수 있습니다.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 하나가 이미 기본 프록시 그룹의 멤버라면 새로 만드는 응용 프로그램에 대해서는 AddToDefautlProxyGroup:$false를 설정해야 합니다. 새 서비스 응용 프로그램을 사용자 지정 서비스 연결 그룹에 추가해야 합니다.  이 작업에 기본 제공 SharePoint cmdlet을 사용할 수 있습니다.  Get-SPServiceApplicationProxyGroup은 팜에 정의되어 있는 서비스 연결 그룹 목록을 반환합니다.  
  
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
  
## <a name="example-1"></a>예제 1  
  
```  
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 이 예에서는 새 서비스 응용 프로그램을 만듭니다. 서비스 응용 프로그램 데이터베이스는 AdvWorks-SRV01이라는 데이터베이스 서버에 만들어집니다. 이 데이터베이스 서버는 대부분의 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치에 대한 일반 구성인 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 명명된 인스턴스로 설치되었습니다. 데이터베이스를 만들려면 SQL Server 인스턴스에 대한 dbcreator 권한이 있어야 합니다. SharePoint 구성 데이터베이스에서 db_owner여야 합니다. 이 응용 프로그램은 팜의 첫 번째 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램이므로 기본 프록시 그룹의 멤버여야 합니다.  
  
  
