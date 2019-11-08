---
title: 마스터 데이터 관리자 웹 애플리케이션의 보안 설정
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0442f63413c3fd0213fb5b63151208fb10b55351
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729174"
---
# <a name="secure-a-master-data-manager-web-application"></a>마스터 데이터 관리자 웹 애플리케이션의 보안 설정

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  HTTPS를 사용하여 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션의 보안을 설정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션은 HTTP 또는 HTTPS 중 하나를 사용할 수 있지만 둘 다 사용할 수는 없습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   사용자가 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 가 설치된 웹 서버의 관리자여야 합니다.  
  
-   MDS가 웹 서버에 설치되어 있으며 웹 애플리케이션이 있어야 합니다. 자세한 내용은 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md) 및 [마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)를 참조하세요.  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>HTTPS를 사용하여 마스터 데이터 관리자 웹 애플리케이션의 보안을 설정하려면  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션이 HTTP로 올바르게 구성되어 있는지 확인한 후 IIS에서 인증서를 만듭니다. 자세한 내용은 [IIS 7에서 서버 인증서 구성](https://technet.microsoft.com/library/cc732230\(WS.10\).aspx)을 참조하십시오.  
  
2.  **연결** 창의 **사이트**에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 호스팅하는 사이트를 클릭합니다.  
  
3.  **동작** 창에서 **바인딩**을 클릭합니다.  
  
4.  **추가**를 클릭합니다.  
  
5.  목록에서 **https**를 선택합니다.  
  
6.  SSL 인증서를 선택합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  (선택 사항) 사용자가 HTTPS를 통해서만 사이트에 액세스할 수 있도록 HTTP를 제거하려면 목록에서 **http**가 포함된 행을 클릭합니다. **제거** 를 클릭하고 확인 대화 상자에서 **예**를 클릭합니다.  
  
    > [!IMPORTANT]  
    >  HTTP를 제거한 후 basicHttp 및 wsHttpBinding 구성을 변경해야 합니다.  
  
9. **사이트 바인딩** 대화 상자를 닫으려면 **닫기**를 클릭합니다.  
  
10. 이제 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication에서 web.config 파일을 엽니다.  
  
11. `<security mode="Message">` 라는 문자열을 찾아 `<security mode="Transport">`로 변경합니다.  

12. Silverlight 클라이언트에서 발생할 수 있는 문제를 방지하기 위해 `<serviceMetadata httpGetEnable="true" httpsGetEnabled="false">`를 `<serviceMetadata httpGetEnable="false" httpsGetEnabled="true">`로 변경합니다.

13. 파일을 저장하고 닫습니다. 오류가 발생하는 경우 UAC를 사용하기 때문일 수 있습니다. 이제 사용자가 HTTPS를 사용하여 사이트에 액세스할 수 있습니다.  

  
## <a name="see-also"></a>관련 항목:  
 [마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
