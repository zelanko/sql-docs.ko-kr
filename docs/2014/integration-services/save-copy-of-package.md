---
title: 패키지 복사본 저장 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1c9018dcf8ae02d939f7ba3bc29d46231ef39d1f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545554"
---
# <a name="save-copy-of-package"></a>패키지 복사본 저장
  **에서 사용할 수 있는** 패키지 복사본 저장 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]대화 상자를 통해 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 패키지 복사본을 다른 위치에 저장하고 필요에 따라 패키지의 보호 수준을 수정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **패키지 위치**  
 패키지 복사본을 저장할 스토리지 위치 유형을 선택합니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
 **SQL Server**  
  
 **파일 시스템**  
  
 **SSIS 패키지 저장소**  
  
 **Server**  
 서버 이름을 입력하거나 목록에서 서버를 선택합니다. 이 옵션은 스토리지 위치가 **SQL Server** 또는 **SSIS 패키지 저장소**인 경우에만 사용할 수 있습니다.  
  
 **인증**  
 Windows 인증 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 선택합니다. 이 옵션은 스토리지 위치가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인 경우에만 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하십시오.  
  
 **인증 유형**  
 인증 유형을 선택합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 암호를 입력합니다.  
  
 **패키지 경로**  
 패키지 경로 입력 하거나 찾아보기 **(...)**  단추 및 패키지를 저장할 폴더를 찾습니다.  
  
 **보호 수준**  
 찾아보기 **(...)**  단추를에서 보호 수준을 업데이트 합니다 **패키지 보호 수준** 대화 상자. 자세한 내용은 [패키지 및 프로젝트 보호 수준 대화 상자](../../2014/integration-services/package-and-project-protection-level-dialog-box.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 가져오기 대화 상자 UI 참조](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [패키지 내보내기 대화 상자 UI 참조](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [패키지 저장](save-packages.md)   
 [패키지 가져오기 및 내보내기&#40;SSIS 서비스&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
