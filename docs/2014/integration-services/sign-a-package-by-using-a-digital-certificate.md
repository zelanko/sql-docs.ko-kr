---
title: 디지털 인증서를 사용 하 여 패키지 서명 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- digital signatures [Integration Services]
- signing packages [Integration Services]
- signatures [Integration Services]
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 31da686dbf25922205ea4d1b03ecaa3758457573
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055622"
---
# <a name="sign-a-package-by-using-a-digital-certificate"></a>디지털 인증서를 사용하여 패키지 서명
  이 항목에서는 디지털 인증서를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에 서명하는 방법을 설명합니다. 디지털 서명을 다른 설정과 함께 사용하여 잘못된 패키지를 로드하거나 실행하지 못하게 할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지에 서명하려면 먼저 다음 태스크를 수행해야 합니다.  
  
-   인증서와 연결할 프라이빗 키를 만들거나 가져오고 이 프라이빗 키를 로컬 컴퓨터에 저장합니다.  
  
-   신뢰할 수 인증 기관에서 코드 서명에 사용할 인증서를 가져옵니다. 다음 방법 중 하나를 사용하여 인증서를 가져오거나 만들 수 있습니다.  
  
    -   인증서를 발급하는 상업적 공용 인증 기관에서 인증서를 가져옵니다.  
  
    -   조직에서 내부적으로 인증서를 발급할 수 있도록 인증서 서버에서 인증서를 가져옵니다. 인증서에 서명하는 데 사용하는 루트 인증서를 **신뢰할 수 있는 루트 인증 기관** 저장소에 추가해야 합니다. 루트 인증서를 추가하려면 MMC( [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console)에 대한 인증서 스냅인을 사용할 수 있습니다. 자세한 내용은 MSDN Library에서 "[Certificate Services](https://go.microsoft.com/fwlink/?LinkId=100755)" 항목을 참조하십시오.  
  
    -   테스트용으로만 사용할 자체의 인증서를 만듭니다. 인증서 작성 도구(Makecert.exe)를 사용하면 테스트용 X.509 인증서를 생성할 수 있습니다. 자세한 내용은 MSDN Library에서 "[인증서 작성 도구(Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)" 항목을 참조하세요.  
  
     인증서에 대한 자세한 내용은 인증서 스냅인의 온라인 도움말을 참조하십시오. 디지털 자산에 서명하는 방법에 대한 자세한 내용은 MSDN Library에서 "[Signing and Checking Code with Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)" 항목을 참조하십시오.  
  
-   인증서를 코드 서명에 사용할 수 있는지 확인합니다. 코드 서명에 인증서를 사용할 수 있는지 여부를 확인하려면 인증서 스냅인에서 인증서 속성을 검토합니다.  
  
-   인증서를 개인 저장소에 저장합니다.  
  
 위의 태스크를 완료한 후 다음 절차에 따라 패키지에 서명할 수 있습니다.  
  
### <a name="to-sign-a-package"></a>패키지에 서명하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 서명할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 **SSIS** 메뉴에서 **디지털 서명**을 클릭합니다.  
  
4.  **디지털 서명** 대화 상자에서 **서명**을 클릭합니다.  
  
5.  **인증서 선택** 대화 상자에서 인증서를 선택합니다.  
  
6.  필요에 따라 **인증서 보기**를 클릭하여 인증서 정보를 봅니다.  
  
7.  **확인** 을 클릭하여 **인증서 선택** 대화 상자를 닫습니다.  
  
8.  **확인** 을 클릭하여 **디지털 서명** 대화 상자를 닫습니다.  
  
9. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
     패키지에 서명했더라도 패키지를 로드하기 전에 디지털 서명을 확인하도록 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 를 구성해야 합니다. 자세한 내용은 [디지털 서명을 사용하여 패키지 원본 확인](security/identify-the-source-of-packages-with-digital-signatures.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [보안 개요&#40;Integration Services&#41;](security/security-overview-integration-services.md)  
  
  
