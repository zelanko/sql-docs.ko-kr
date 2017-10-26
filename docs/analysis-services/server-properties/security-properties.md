---
title: "보안 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0233cd9c2e9eff5cc776b921e092206524546a52
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="security-properties"></a>보안 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 보안 서버 속성을 지원합니다. 추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 및 테이블 형식 서버 모드  
  
## <a name="properties"></a>속성  
 **RequireClientAuthentication**  
 클라이언트 인증이 필요한지 여부를 나타내는 부울 속성입니다.  
  
 이 속성의 기본값은 True이며, 이 경우 클라이언트 인증이 필요합니다.  
  
 **SecurityPackageList**  
 클라이언트 인증을 위해 서버에서 사용하는 쉼표로 구분된 SSPI 패키지 목록을 포함하는 문자열 속성입니다.  
  
 **DisableClientImpersonation**  
 클라이언트 가장을 해제할지 여부(예: 저장 프로시저에서)를 나타내는 부울 속성입니다.  
  
 이 속성의 기본값은 False이며, 이 경우 클라이언트 가장이 설정됩니다.  
  
 **BuiltinAdminsAreServerAdmins**  
 로컬 시스템 관리자 그룹의 멤버가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자인지 여부를 나타내는 부울 속성입니다.  
  
 **ServiceAccountIsServerAdmin**  
 서비스 계정이 서버 관리자인지 여부를 나타내는 부울 값입니다.  
  
 이 속성의 기본값은 True이며, 이 경우 서비스 계정이 서버 관리자입니다.  
  
 **ErrorMessageMode**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataProtection\ RequiredProtectionLevel**  
 모든 클라이언트 요청에 대해 필요한 보호 수준을 정의하는 부호 있는 32비트 정수 속성입니다. 이 속성은 다음 표에 나열된 값 중 하나를 취합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|*0*|없음. 일반 텍스트가 허용됩니다.|  
|*1.*|(기본값)암호화 필요. 일반 텍스트 로깅은 없습니다.|  
|*2*|일반 텍스트 요청이 허용되지만 반드시 서명이 있어야 합니다(암호화보다 약한 보호 수준).|  
  
 **AdministrativeDataProtection\ RequiredProtectionLevel**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  

