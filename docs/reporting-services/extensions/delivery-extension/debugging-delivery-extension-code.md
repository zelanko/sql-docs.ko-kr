---
title: "배달 확장 프로그램 코드 디버깅 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e2d2162167123c152cbbeb58739f25ee06ec692a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="debugging-delivery-extension-code"></a>배달 확장 프로그램 코드 디버깅
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 수 있는 몇 가지 디버깅 도구는 배달 확장 프로그램 코드를 분석 하 고 오류를 찾는 제공 합니다. 작업하기 가장 좋은 도구는 수행하려는 작업에 따라 달라집니다. 이 예에서는 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]를 사용합니다.  
  
#### <a name="to-debug-your-delivery-extension-code"></a>배달 확장 프로그램 코드를 디버깅하려면  
  
1.  시작 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] 배달 확장 프로그램 프로젝트를 엽니다.  
  
2.  프로젝트를 빌드하고 배달 확장 프로그램 어셈블리 및 해당하는 .pdb 파일을 보고서 서버 및 보고서 관리자에 배포합니다. 배포에 대 한 자세한 내용은 참조 [Deploying a Delivery Extension](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)합니다.  
  
3.  구독 사용자 인터페이스를 작성하여 보고서 관리자를 확장한 경우에는 배달 확장 프로그램 코드가 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 열려 있는 상태에서 Internet Explorer를 열고 보고서 관리자로 이동합니다. 보고서 관리자에 대해 배포된 구독 사용자 인터페이스가 없는 경우에는 SOAP API를 사용하여 배달 확장 프로그램을 호출하는 위치인 클라이언트 응용 프로그램을 열면 됩니다.  
  
4.  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 및 배달 확장 프로그램 프로젝트로 이동하고 코드에서 중단점을 설정합니다.  
  
5.  배달 확장 프로젝트를 활성 창 상태로 두고 클릭 **프로세스에 연결** 에 **디버그** 메뉴.  
  
     **프로세스에 연결** 대화 상자가 열립니다.  
  
6.  프로세스 목록에서 aspnet_wp.exe 프로세스 (또는 응용 프로그램을 IIS 6.0에서 배포할 경우 w3wp.exe)를 선택 하 고 클릭 **연결**합니다.  
  
7.  배달 확장 프로그램을 사용하여 새 구독을 정의합니다. 대부분의 경우 보고서 관리자 또는 SOAP API를 사용합니다. 그러면 디버거가 호출되고 중단점에 해당하는 코드가 실행됩니다.  
  
8.  사용 하 여 코드를 단계별로 **F11** 키입니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]를 사용하여 디버깅하는 방법은 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
