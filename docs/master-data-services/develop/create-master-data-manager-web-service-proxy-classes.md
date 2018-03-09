---
title: "마스터 데이터 관리자 웹 서비스에 대한 프록시 클래스 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: develop
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6810bec24c6070e1336dc653206d6d0757ae687
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2018
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>마스터 데이터 관리자 웹 서비스에 대한 프록시 클래스 만들기
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 서비스를 사용하면 사용자의 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 사이트에 액세스할 수 있는 모든 컴퓨터에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]의 기능을 프로그래밍 방식으로 사용할 수 있습니다. 웹 서비스에 액세스하기 위한 코드를 작성하려면 먼저 프록시 클래스를 생성해야 합니다. 웹 서비스 작업을 수행하는 데 사용되는 주요 프록시 클래스는 <xref:Microsoft.MasterDataServices.ServiceClient> 인터페이스를 구현하는 <xref:Microsoft.MasterDataServices.IService> 클래스입니다.  
  
## <a name="enable-web-service-metadata-publishing"></a>웹 서비스 메타데이터 게시 활성화  
 프록시 클래스를 생성하려면 먼저 웹 서비스 메타데이터 게시를 활성화해야 합니다. 이렇게 하려면 다음 단계를 수행하십시오.  
  
1.  텍스트 편집기에서 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.config 파일을 엽니다. 이 파일은 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 설치 경로의 WebApplication 폴더에 있습니다.  
  
2.  **\<serviceBehaviors>** 아래에서 **mdsWsHttpBehavior** 섹션을 찾습니다. **\<serviceMetadata>** 요소의 경우 **httpGetEnabled**를 **true**로 설정합니다.  
  
    > [!NOTE]  
    >  SSL(Secure Sockets Layer)을 통해 웹 서비스를 사용하도록 설정하려면 web.config 파일의 **mdsWsHttpBehavior** 섹션에서 **httpsGetEnabled**를 **true**로 설정합니다. 또한 **mdsWsHTTPBinding**을 SSL에 대해 구성되도록 변경하고 SSL 이외의 섹션을 주석으로 처리해야 합니다.  
  
3.  파일의 변경 내용을 저장합니다.  
  
4.  다음과 같은 서비스 URL로 이동하여 메타데이터 게시를 테스트합니다(예: `http://yourserver/MDS/service/service.svc`). 메타데이터 게시가 활성화된 경우 "서비스를 만들었습니다."로   
    시작하는 페이지가 표시됩니다.  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Visual Studio를 사용하여 프록시 클래스 만들기  
 Visual Studio 2010이 설치된 경우 프로젝트에 **서비스 참조**를 추가하면 가장 간단하게 프록시 클래스를 생성할 수 있습니다. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램의 URL에 /service/service.svc를 추가하면 서비스 참조의 주소가 됩니다. 예를 들어 `http://yourserver/MDS/service/service.svc`을 참조하십시오. 자세한 내용은 [방법: 서비스 참조 추가, 업데이트 또는 제거](http://go.microsoft.com/fwlink/?LinkId=221167)를 참조하십시오.  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Svcutil.exe를 사용하여 프록시 클래스 만들기  
 컴퓨터에서 Svcutil.exe를 사용하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK가 설치되어 있어야 합니다. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 사용하는 경우에는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 명령 프롬프트를 사용하여 명령을 실행해야 합니다. 자세한 내용은 [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027) 및 [서비스 메타데이터에서 WCF 클라이언트 생성](http://go.microsoft.com/fwlink/?LinkId=164821)을 참조하십시오.  
  
 Svcutil.exe를 사용하여 C# 프록시 클래스 집합을 만들려면 다음과 같은 명령을 사용하십시오.  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
-   *servername*:*port*는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]를 호스팅하는 컴퓨터의 이름과 포트 번호입니다.  
  
-   *virtual_path*는 인터넷 정보 서비스(IIS)에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]의 가상 경로입니다.  
  
-   *proxy_name*은 생성된 프록시 파일의 이름입니다.  
  
## <a name="see-also"></a>참고 항목  
 [범주별로 분류한 웹 서비스 작업&#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
