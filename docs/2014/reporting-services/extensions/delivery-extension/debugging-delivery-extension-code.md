---
title: 배달 확장 프로그램 코드 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0d289b3d4c4177ed885a3153bb758d0052286bec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63164337"
---
# <a name="debugging-delivery-extension-code"></a>배달 확장 프로그램 코드 디버깅
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에서는 배달 확장 프로그램 코드를 분석하여 오류를 찾는 데 유용한 디버깅 도구를 다수 제공합니다. 작업하기 가장 좋은 도구는 수행하려는 작업에 따라 달라집니다. 이 예에서는 [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]를 사용합니다.  
  
#### <a name="to-debug-your-delivery-extension-code"></a>배달 확장 프로그램 코드를 디버깅하려면  
  
1.  [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]를 시작하고 배달 확장 프로젝트를 엽니다.  
  
2.  프로젝트를 빌드하고 배달 확장 프로그램 어셈블리 및 해당하는 .pdb 파일을 보고서 서버 및 보고서 관리자에 배포합니다. 배포에 대한 자세한 내용은 [배달 확장 프로그램 배포](deploying-a-delivery-extension.md)를 참조하세요.  
  
3.  구독 사용자 인터페이스를 작성하여 보고서 관리자를 확장한 경우에는 배달 확장 프로그램 코드가 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 열려 있는 상태에서 Internet Explorer를 열고 보고서 관리자로 이동합니다. 보고서 관리자에 대해 배포된 구독 사용자 인터페이스가 없는 경우에는 SOAP API를 사용하여 배달 확장 프로그램을 호출하는 위치인 클라이언트 애플리케이션을 열면 됩니다.  
  
4.  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 및 배달 확장 프로그램 프로젝트로 이동하고 코드에서 중단점을 설정합니다.  
  
5.  배달 확장 프로젝트를 활성 창 상태로 두고 **디버그** 메뉴에서 **프로세스에 연결**을 클릭합니다.  
  
     **프로세스에 연결** 대화 상자가 열립니다.  
  
6.  프로세스 목록에서 aspnet_wp.exe 프로세스(애플리케이션을 IIS 6.0에서 배포할 경우 w3wp.exe)를 선택하고 **연결**을 클릭합니다.  
  
7.  배달 확장 프로그램을 사용하여 새 구독을 정의합니다. 대부분의 경우 보고서 관리자 또는 SOAP API를 사용합니다. 그러면 디버거가 호출되고 중단점에 해당하는 코드가 실행됩니다.  
  
8.  **F11** 키를 사용하여 코드를 단계별로 실행합니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]를 사용하여 디버깅하는 방법은 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [배달 확장 프로그램 구현](implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
