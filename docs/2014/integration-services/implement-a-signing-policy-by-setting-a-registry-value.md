---
title: 레지스트리 값을 설정 하 여 서명 정책 구현 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8daa6582f18d9c5279e7539dd9c3740d90e36d2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353206"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>레지스트리 값을 설정하여 서명 정책 구현
  선택적 레지스트리 값을 사용하여 서명된 패키지나 서명되지 않은 패키지를 로드하기 위한 조직의 정책을 관리할 수 있습니다. 이 레지스트리 값을 사용하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 실행하고 정책을 적용할 각 컴퓨터에 이 레지스트리 값을 만들어야 합니다. 레지스트리 값이 설정된 후 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 패키지를 로드하기 전에 서명을 확인합니다.  
  
 이 항목의 절차에서는 선택적 `BlockedSignatureStates` DWORD 값을 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 레지스트리 키에 추가하는 방법에 대해 설명합니다. `BlockedSignatureStates`의 데이터 값은 패키지에 신뢰할 수 없는 서명이나 잘못된 서명이 있거나 패키지가 서명되지 않은 경우에 패키지를 차단해야 하는지 여부를 결정합니다. 패키지 서명에 사용되는 서명 상태와 관련해서 `BlockedSignatureStates` 레지스트리 값은 다음 정의를 사용합니다.  
  
-   *유효한 서명* 이란 성공적으로 읽을 수 있는 서명을 말합니다.  
  
-   *잘못된 서명* 이란 해독된 체크섬(개인 키로 암호화된 패키지 코드의 단방향 해시)이 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 로드하는 과정에 계산하여 해독된 체크섬과 일치하지 않는 서명을 말합니다.  
  
-   *신뢰할 수 있는 서명* 이란 신뢰할 수 있는 루트 인증 기관에서 서명한 디지털 인증서를 사용하여 만든 서명을 말합니다. 이 설정을 사용할 경우 서명자가 사용자의 신뢰할 수 있는 게시자 목록에 없어도 됩니다.  
  
-   *신뢰할 수 없는 서명* 이란 신뢰할 수 있는 루트 인증 기관에서 발급되었는지 확인할 수 없거나 최신 상태가 아닌 서명을 말합니다.  
  
 다음 표에서는 DWORD 데이터의 유효한 값 및 연관된 정책을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|관리 제한이 없습니다.|  
|1|잘못된 서명을 차단합니다.<br /><br /> 이 설정은 서명되지 않은 패키지를 차단하지 않습니다.|  
|2|잘못된 서명과 신뢰할 수 없는 서명을 차단합니다.<br /><br /> 이 설정은 서명되지 않은 패키지를 차단하지 않지만 자체 생성된 서명은 차단합니다.|  
|3|잘못된 서명과 신뢰할 수 없는 서명, 서명되지 않은 패키지를 차단합니다.<br /><br /> 이 설정은 자체 생성된 서명도 차단합니다.|  
  
> [!NOTE]  
>  `BlockedSignatureStates`에 대한 권장 설정은 3입니다. 이 설정은 서명되지 않은 패키지나 잘못된 서명 또는 신뢰할 수 없는 서명에 대해 가장 강력한 보호 기능을 제공합니다. 그러나 권장 설정이 모든 경우에 적합하지는 않습니다. 디지털 자산에 서명하는 방법은 MSDN Library에서 "[코드 서명 소개(Introduction to Code Signing)](https://go.microsoft.com/fwlink/?LinkId=51414)" 항목을 참조하십시오.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>패키지에 대한 서명 정책을 구현하려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  실행 대화 상자에서 입력 `Regedit`를 클릭 하 고 **확인**합니다.  
  
3.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 레지스트리 키를 찾습니다.  
  
4.  **MSDTS**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **DWORD 값**을 클릭합니다.  
  
5.  새 값의 이름을 `BlockedSignatureStates`(으)로 업데이트합니다.  
  
6.  마우스 오른쪽 단추로 클릭 `BlockedSignatureStates` 누릅니다 **수정**합니다.  
  
7.  **DWORD 값 편집** 대화 상자에서 값 0, 1, 2 또는 3을 입력합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **파일** 메뉴에서 **끝내기**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보안 개요&#40;Integration Services&#41;](security/security-overview-integration-services.md)   
 [디지털 서명을 사용하여 패키지 원본 확인](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
