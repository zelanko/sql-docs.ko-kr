---
title: 웹 구성 참조(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cdc430e3e74043896df8b25993dc78cf8d8ed70e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979445"
---
# <a name="web-configuration-reference-master-data-services"></a>웹 구성 참조(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서는 IIS(인터넷 정보 서비스)가 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 및 웹 서비스를 호스트할 수 있도록 하는 구성 설정이 Web.config 파일에 포함됩니다. 이 Web.config 파일은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 설치 경로의 WebApplication 폴더에 있습니다. 경로 및 사용 권한에 대한 자세한 내용은 [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)을 참조하세요.  
  
## <a name="webconfig-elements"></a>Web.Config 요소  
 Web.config 파일에는 표준 IIS, .NET Framework, ASP.NET 및 WCF(Windows Communication Foundation) 구성 요소 외에도 사용자 지정 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 요소인 **\<masterDataServices>** 가 포함되어 있습니다. 다음 표에서는 Web.config 파일에 포함된 요소에 대해 설명합니다.  
  
|구성 요소|설명|  
|---------------------------|-----------------|  
|**masterDataServices**|사용자 지정 요소. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 서비스를 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 연결합니다.|  
|**connectionStrings**|ASP.NET 요소. 자세한 내용은 MSDN Library에서 [connectionStrings 요소(ASP.NET 설정 스키마)](http://go.microsoft.com/fwlink/?LinkId=178347) 를 참조하세요.|  
|**system.web**|ASP.NET 요소. 자세한 내용은 MSDN Library에서 [system.web 요소(ASP.NET 설정 스키마)](http://go.microsoft.com/fwlink/?LinkId=178348) 를 참조하세요.|  
|**startup**|.NET Framework 요소. 자세한 내용은 MSDN Library에서 [\<startup> 요소](http://go.microsoft.com/fwlink/?LinkId=178349)를 참조하세요.|  
|**런타임**|.NET Framework 요소. 자세한 내용은 MSDN Library에서 [\<runtime> 요소](http://go.microsoft.com/fwlink/?LinkId=178350)를 참조하세요.|  
|**system.codedom**|.NET Framework 요소. 자세한 내용은 MSDN Library에서 [\<system.codedom> 요소](http://go.microsoft.com/fwlink/?LinkId=178351)를 참조하세요.|  
|**system.web.extensions**|ASP.NET 요소. 자세한 내용은 MSDN Library에서 [system.web.extensions 요소(ASP.NET 설정 스키마)](http://go.microsoft.com/fwlink/?LinkId=178352) 를 참조하세요.|  
|**system.webServer**|IIS 요소를 포함하는 섹션 그룹. 자세한 내용은 MSDN Library에서 [system.webServer 섹션 그룹 \[IIS 7 설정 스키마\]](http://go.microsoft.com/fwlink/?LinkId=178353)을 참조하세요.|  
|**system.serviceModel**|WCF 요소. 자세한 내용은 MSDN Library에서 [\<system.serviceModel>](http://go.microsoft.com/fwlink/?LinkId=178354)을 참조하세요.|  
|**system.diagnostics**|.NET Framework 요소. 자세한 내용은 MSDN Library에서 [\<system.diagnostics> 요소](http://go.microsoft.com/fwlink/?LinkId=178355)를 참조하세요.|  
|**appSettings**|ASP.NET 요소. 자세한 내용은 MSDN Library에서 [appSettings 요소(일반 설정 스키마)](http://go.microsoft.com/fwlink/?LinkId=178356) 를 참조하세요.|  
  
## <a name="masterdataservices-element"></a>masterDataServices 요소  
 **\<masterDataServices>** 요소는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 서비스를 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 연결하는 데 사용되는 사용자 지정 요소입니다.  
  
### <a name="syntax"></a>구문  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>요소 및 특성  
  
|항목|설명|  
|----------|-----------------|  
|**instance**|자식 요소. 웹 서비스와 데이터베이스 연결 문자열에 대한 정보를 지정하는 특성을 포함합니다.|  
|**virtualPath**|특성. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 및 서비스의 가상 경로를 지정합니다. 이 값은 IIS ApplicationHost.config 파일에서 **\<site>** 요소 아래에 있는 **\<application>** 요소의 **path** 특성에 해당합니다.|  
|**siteName**|특성. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램과 서비스를 호스트하는 사이트의 이름을 지정합니다. 이 값은 IIS ApplicationHost.config 파일에서 **\<sites>** 아래에 있는 **\<site>** 요소의 **name** 특성에 해당합니다.|  
|**connectionName**|특성. 사용할 연결 이름을 지정합니다. 이 값은 Web.config에서 **\<connectionStrings>** 요소 아래에 있는 **\<add>** 요소의 **name** 특성에 해당합니다.|  
|**serviceName**|특성. 웹 서비스의 이름을 지정합니다. 이 값은 Web.config에서 **\<services>** 요소 아래에 있는 **\<service>** 요소의 **name** 특성에 해당합니다.|  
  
### <a name="example"></a>예제  
 다음 예에서는 MDSDB를 통해 지정된 연결 문자열을 사용하는 /MDS 경로와 Contoso 사이트의 MDS1이라는 서비스를 보여 줍니다.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
