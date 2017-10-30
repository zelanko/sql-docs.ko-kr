---
title: "사용자의 사용 권한 테스트(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
caps.latest.revision: 4
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 6e3a240837692dbe8ea3cdfdcba42035e0317e78
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="test-a-user39s-permissions-master-data-services"></a>사용자의 사용 권한 테스트(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 테스트 사용자를 만들고 사용 권한을 테스트하기 위해 웹 응용 프로그램에 로그인할 수 있습니다. 사용자가 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] URL에 액세스하려고 시도할 때 사용자의 자격 증명이 인증됩니다. Internet Explorer의 보안 설정에 따라 인증이 자동으로 진행되는지, 아니면 사용자 이름 및 암호를 입력해야 하는지 여부가 결정됩니다. 이 설정을 변경하려면 다음 단계를 수행하십시오.  
  
### <a name="to-test-a-users-security"></a>사용자의 보안을 테스트하려면  
  
1.  Internet Explorer 7 이상에서 **도구**, **인터넷 옵션**을 차례로 클릭한 다음 **보안** 탭을 클릭합니다.  
  
2.  **로컬 인트라넷** 을 클릭한 다음 **사용자 지정 수준** 단추를 클릭합니다.  
  
3.  **사용자 인증** 섹션에서 **사용자 이름 및 암호 확인**을 선택합니다.  
  
4.  다음에 브라우저 창을 열면 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  

