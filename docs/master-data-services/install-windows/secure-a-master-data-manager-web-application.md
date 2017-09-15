---
title: "마스터 데이터 관리자 웹 응용 프로그램의 보안 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 57399aa2436d8d559e53762a33c594c0f69776bd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="secure-a-master-data-manager-web-application"></a>마스터 데이터 관리자 웹 응용 프로그램의 보안 설정
  HTTPS를 사용하여 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램의 보안을 설정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램은 HTTP 또는 HTTPS 중 하나를 사용할 수 있지만 둘 다 사용할 수는 없습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   사용자가 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 가 설치된 웹 서버의 관리자여야 합니다.  
  
-   MDS가 웹 서버에 설치되어 있으며 웹 응용 프로그램이 있어야 합니다. 자세한 내용은 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md) 및 [마스터 데이터 관리자 웹 응용 프로그램 만들기&#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)를 참조하세요.  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>HTTPS를 사용하여 마스터 데이터 관리자 웹 응용 프로그램의 보안을 설정하려면  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램이 HTTP로 올바르게 구성되어 있는지 확인한 후 IIS에서 인증서를 만듭니다. 자세한 내용은 [IIS 7에서 서버 인증서 구성](http://technet.microsoft.com/library/cc732230\(WS.10\).aspx)을 참조하십시오.  
  
2.  **연결** 창의 **사이트**에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 호스팅하는 사이트를 클릭합니다.  
  
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
  
12. 파일을 저장하고 닫습니다. 오류가 발생하는 경우 UAC를 사용하기 때문일 수 있습니다. 자세한 내용은 [사용자 계정 컨트롤 해제](http://technet.microsoft.com/library/cc709691\(WS.10\).aspx)를 참조하십시오. 이제 사용자가 HTTPS를 사용하여 사이트에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [마스터 데이터 관리자 웹 응용 프로그램 만들기&#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
