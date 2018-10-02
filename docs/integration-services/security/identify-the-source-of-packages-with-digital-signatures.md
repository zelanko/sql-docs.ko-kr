---
title: 디지털 서명을 사용하여 패키지 원본 확인 | Microsoft Docs
ms.custom: security
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.digitalsigning.f1
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ee92e9c8873a65dd6f35da970e2bb2223a4649e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798036"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>디지털 서명을 사용하여 패키지 원본 확인
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 해당 원본을 식별하는 디지털 인증서를 사용하여 서명할 수 있습니다. 디지털 인증서를 사용하여 패키지에 서명하면 패키지를 로드하기 전에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 디지털 서명을 확인하도록 할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 서명을 확인하도록 하려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 유틸리티(dtexec.exe)에서 옵션을 설정하거나 선택적 레지스트리 값을 설정합니다.  
  
## <a name="sign-a-package-with-a-digital-certificate"></a>디지털 인증서를 사용하여 패키지 서명  
 디지털 인증서를 사용하여 패키지에 서명하려면 먼저 인증서를 만들거나 가져와야 합니다. 인증서가 있으면 이 인증서를 사용하여 패키지에 서명할 수 있습니다. 인증서를 가져오고 해당 인증서를 사용하여 패키지에 서명하는 방법에 대한 자세한 내용은 [디지털 인증서를 사용하여 패키지 서명](#cert)을 참조하세요.  
  
## <a name="set-an-option-to-check-the-package-signature"></a>패키지 서명을 확인하는 옵션 설정  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 **dtexec** 유틸리티 모두에는 서명된 패키지의 디지털 서명을 확인하도록 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 구성하는 옵션이 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 유틸리티 중 무엇을 사용할지는 다음과 같이 모든 패키지를 확인할지 또는 특정 패키지만 확인할지에 따라 결정합니다.  
  
-   디자인 타임에 패키지를 로드하기 전에 모든 패키지의 디지털 서명을 확인하려면 **에서** 패키지 로드 시 디지털 서명 확인 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]옵션을 설정합니다. 이 옵션은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 모든 패키지에 대한 전역 설정입니다.
  
-   개별 패키지의 디지털 서명을 확인하려면 **dtexec** 유틸리티를 사용하여 패키지를 실행할 때 **/VerifyS[igned]** 옵션을 지정합니다. 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
## <a name="set-a-registry-value-to-check-package-signature"></a>패키지 서명을 확인하는 레지스트리 값 설정  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 서명되거나 서명되지 않은 패키지에 대한 조직의 정책을 관리하는 데 사용할 수 있는 선택적 레지스트리 값인 **BlockedSignatureStates**도 지원합니다. 이 레지스트리 값을 사용하면 패키지에 서명이 없거나 패키지의 서명이 잘못되거나 신뢰할 수 없는 경우 패키지를 로드하지 못하게 할 수 있습니다. 이 레지스트리 값을 설정하는 방법에 대한 자세한 내용은 [레지스트리 값을 설정하여 서명 정책 구현](#registry)을 참조하세요.  
  
> **참고:** 선택적 **BlockedSignatureStates** 레지스트리 값은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 명령줄에서 설정한 디지털 서명 옵션보다 더 제한적인 설정을 지정할 수 있습니다. 이 경우 더 제한적인 설정이 다른 설정보다 우선합니다.  

## <a name="registry"></a> 레지스트리 값을 설정하여 서명 정책 구현
  선택적 레지스트리 값을 사용하여 서명된 패키지나 서명되지 않은 패키지를 로드하기 위한 조직의 정책을 관리할 수 있습니다. 이 레지스트리 값을 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하고 정책을 적용할 각 컴퓨터에 이 레지스트리 값을 만들어야 합니다. 레지스트리 값이 설정된 후 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지를 로드하기 전에 서명을 확인합니다.  
  
 이 항목의 절차에서는 선택적 **BlockedSignatureStates** DWORD 값을 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 레지스트리 키에 추가하는 방법을 설명합니다. **BlockedSignatureStates** 의 데이터 값은 패키지에 신뢰할 수 없는 서명이나 잘못된 서명이 있거나 패키지가 서명되지 않은 경우에 패키지를 차단해야 하는지 여부를 결정합니다. 패키지 서명에 사용되는 서명 상태와 관련해서 **BlockedSignatureStates** 레지스트리 값은 다음 정의를 사용합니다.  
  
-   *유효한 서명* 이란 성공적으로 읽을 수 있는 서명을 말합니다.  
  
-   *잘못된 서명* 이란 해독된 체크섬(개인 키로 암호화된 패키지 코드의 단방향 해시)이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 로드하는 과정에 계산하여 해독된 체크섬과 일치하지 않는 서명을 말합니다.  
  
-   *신뢰할 수 있는 서명* 이란 신뢰할 수 있는 루트 인증 기관에서 서명한 디지털 인증서를 사용하여 만든 서명을 말합니다. 이 설정을 사용할 경우 서명자가 사용자의 신뢰할 수 있는 게시자 목록에 없어도 됩니다.  
  
-   *신뢰할 수 없는 서명* 이란 신뢰할 수 있는 루트 인증 기관에서 발급되었는지 확인할 수 없거나 최신 상태가 아닌 서명을 말합니다.  
  
 다음 표에서는 DWORD 데이터의 유효한 값 및 연관된 정책을 나열합니다.  
  
|값|설명|  
|-----------|-----------------|  
|0|관리 제한이 없습니다.|  
|1|잘못된 서명을 차단합니다.<br /><br /> 이 설정은 서명되지 않은 패키지를 차단하지 않습니다.|  
|2|잘못된 서명과 신뢰할 수 없는 서명을 차단합니다.<br /><br /> 이 설정은 서명되지 않은 패키지를 차단하지 않지만 자체 생성된 서명은 차단합니다.|  
|3|잘못된 서명과 신뢰할 수 없는 서명, 서명되지 않은 패키지를 차단합니다.<br /><br /> 이 설정은 자체 생성된 서명도 차단합니다.|  
  
> [!NOTE]  
>  **BlockedSignatureStates** 에 대한 권장 설정은 3입니다. 이 설정은 서명되지 않은 패키지나 잘못된 서명 또는 신뢰할 수 없는 서명에 대해 가장 강력한 보호 기능을 제공합니다. 그러나 권장 설정이 모든 경우에 적합하지는 않습니다. 디지털 자산에 서명하는 방법은 MSDN Library에서 "[코드 서명 소개(Introduction to Code Signing)](http://go.microsoft.com/fwlink/?LinkId=51414)" 항목을 참조하십시오.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>패키지에 대한 서명 정책을 구현하려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  실행 대화 상자에서 **Regedit**을(를) 입력한 다음 **확인**을 클릭합니다.  
  
3.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 레지스트리 키를 찾습니다.  
  
4.  **MSDTS**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **DWORD 값**을 클릭합니다.  
  
5.  새 값의 이름을 **BlockedSignatureStates**(으)로 업데이트합니다.  
  
6.  **BlockedSignatureStates** 를 마우스 오른쪽 단추로 클릭하고 **수정**을 클릭합니다.  
  
7.  **DWORD 값 편집** 대화 상자에서 값 0, 1, 2 또는 3을 입력합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **파일** 메뉴에서 **끝내기**를 클릭합니다.    

## <a name="cert"></a> 디지털 인증서를 사용하여 패키지 서명
  이 항목에서는 디지털 인증서를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 서명하는 방법을 설명합니다. 디지털 서명을 다른 설정과 함께 사용하여 잘못된 패키지를 로드하거나 실행하지 못하게 할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 서명하려면 먼저 다음 태스크를 수행해야 합니다.  
  
-   인증서와 연결할 개인 키를 만들거나 가져오고 이 개인 키를 로컬 컴퓨터에 저장합니다.  
  
-   신뢰할 수 인증 기관에서 코드 서명에 사용할 인증서를 가져옵니다. 다음 방법 중 하나를 사용하여 인증서를 가져오거나 만들 수 있습니다.  
  
    -   인증서를 발급하는 상업적 공용 인증 기관에서 인증서를 가져옵니다.  
  
    -   조직에서 내부적으로 인증서를 발급할 수 있도록 인증서 서버에서 인증서를 가져옵니다. 인증서에 서명하는 데 사용하는 루트 인증서를 **신뢰할 수 있는 루트 인증 기관** 저장소에 추가해야 합니다. 루트 인증서를 추가하려면 MMC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console)에 대한 인증서 스냅인을 사용할 수 있습니다. 자세한 내용은 MSDN Library에서 "[Certificate Services](http://go.microsoft.com/fwlink/?LinkId=100755)" 항목을 참조하십시오.  
  
    -   테스트용으로만 사용할 자체의 인증서를 만듭니다. 인증서 작성 도구(Makecert.exe)를 사용하면 테스트용 X.509 인증서를 생성할 수 있습니다. 자세한 내용은 MSDN Library에서 "[인증서 작성 도구(Makecert.exe)](http://go.microsoft.com/fwlink/?LinkId=100756)" 항목을 참조하세요.  
  
     인증서에 대한 자세한 내용은 인증서 스냅인의 온라인 도움말을 참조하십시오. 디지털 자산에 서명하는 방법에 대한 자세한 내용은 MSDN Library에서 "[Signing and Checking Code with Authenticode](http://go.microsoft.com/fwlink/?LinkId=78100)" 항목을 참조하십시오.  
  
-   인증서를 코드 서명에 사용할 수 있는지 확인합니다. 코드 서명에 인증서를 사용할 수 있는지 여부를 확인하려면 인증서 스냅인에서 인증서 속성을 검토합니다.  
  
-   인증서를 개인 저장소에 저장합니다.  
  
 위의 태스크를 완료한 후 다음 절차에 따라 패키지에 서명할 수 있습니다.  
  
### <a name="to-sign-a-package"></a>패키지에 서명하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 서명할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 **SSIS** 메뉴에서 **디지털 서명**을 클릭합니다.  
  
4.  **디지털 서명** 대화 상자에서 **서명**을 클릭합니다.  
  
5.  **인증서 선택** 대화 상자에서 인증서를 선택합니다.  
  
6.  필요에 따라 **인증서 보기**를 클릭하여 인증서 정보를 봅니다.  
  
7.  **확인** 을 클릭하여 **인증서 선택** 대화 상자를 닫습니다.  
  
8.  **확인** 을 클릭하여 **디지털 서명** 대화 상자를 닫습니다.  
  
9. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
     패키지에 서명했더라도 패키지를 로드하기 전에 디지털 서명을 확인하도록 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 구성해야 합니다.  

## <a name="signing_dialog"></a> 디지털 서명 대화 상자 UI 참조
  **디지털 서명** 대화 상자를 사용하여 패키지를 디지털 서명으로 서명하거나 서명을 제거할 수 있습니다. **디지털 서명** 대화 상자는 **의** SSIS **메뉴에 있는** 디지털 서명 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]옵션에서 사용할 수 있습니다.  
  
 자세한 내용은 [디지털 인증서를 사용하여 패키지 서명](#cert)을 참조하세요.  
  
### <a name="options"></a>Options  
 **서명**  
 클릭하여 **인증서 선택** 대화 상자를 열고 사용할 인증서를 선택합니다.  
  
 **제거**  
 디지털 서명을 제거하려면 클릭합니다.  

## <a name="see-also"></a>관련 항목:  
 [Integration Services&#40;SSIS&#41; 패키지](../../integration-services/integration-services-ssis-packages.md)   
 [보안 개요&#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  
