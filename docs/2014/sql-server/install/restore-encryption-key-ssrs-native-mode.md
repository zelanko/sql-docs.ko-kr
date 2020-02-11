---
title: 복원 암호화 키 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 111e44275922149949cd7e252e112d95cef65076
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952030"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>복원 암호화 키(SSRS 기본 모드)
  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 암호화 키를 사용하여 보고서 서버 데이터베이스에 저장된 중요한 데이터를 보호합니다. 암호화된 데이터에 대한 지속적인 액세스를 보장하려면 서비스 계정이 변경된 경우, 또는 계획된 마이그레이션에 따라 암호화 키를 복원해야 하는 경우에 대비하여 암호화 키 백업을 만들어야 합니다. 이 항목은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용해서 키를 복원하는 방법에 대해 설명합니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 키를 복원하려면 암호로 보호된 파일에 키의 백업 복사본을 미리 저장해 두어야 합니다. 키 복원 과정에서 보고서 서버는 기존 키를 암호로 보호된 파일에 있는 키로 바꿉니다. 이 파일에 있는 키는 데이터를 암호화 및 암호 해독하는 데 사용하는 키와 동일해야 합니다.  
  
 올바른 키를 복원했는지 확인하려면 보고서 관리자를 사용하여 저장된 자격 증명을 사용하는 데이터 원본이 있는 보고서 또는 구독을 확인합니다. 구독 정의 페이지를 열려고 시도할 때 "보고서 서버에서 암호화된 데이터에 액세스할 수 없습니다." 오류가 나타나거나, 이전에 보고서 데이터 원본에 대해 저장된 자격 증명을 사용한 보고서를 열 때 자격 증명을 입력하라는 메시지가 표시되면 잘못된 키를 복원한 것입니다.  
  
 데이터를 암호화하는 데 사용한 키와 다른 잘못된 키를 복원한 경우 현재 보고서 서버 데이터베이스에 저장된 데이터를 해독할 수 없습니다. 잘못된 키를 복원한 경우 올바른 키의 백업 복사본이 있으면 즉시 이 복사본을 복원해야 합니다. 데이터를 암호화하는 데 사용한 키의 백업 복사본이 없으면 암호화된 데이터를 모두 삭제해야 합니다. 
  **암호화 키** 페이지에서 [삭제](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) 단추를 클릭하여 이 단계를 수행합니다. 암호화된 내용을 삭제한 후에는 모든 구독을 수동으로 업데이트하고 보고서 서버에서 보고서 및 데이터 기반 구독에 정의된 모든 저장된 자격 증명을 다시 지정해야 합니다.  
  
## <a name="restore-encryption-key-dialog"></a>암호화 키 복원 대화 상자  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager를 찾을 수 있는 위치에 대 한 자세한 내용은 [Reporting Services 구성 관리자 &#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)를 참조 하세요.  
  
 암호화 키 복원 대화 상자를 열려면 **구성 관리자의 탐색 창에서** 암호화 키 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 클릭한 다음 **복원**을 클릭합니다. 이 대화 상자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자의 서비스 계정 페이지를 사용하여 서비스 계정을 업데이트할 때도 나타납니다. 자세한 내용은 다음을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **파일 위치**  
 대칭 키 복사본이 있는 암호로 보호된 파일을 선택합니다. 기본 파일 확장명은 .snk입니다.  
  
 **암호**  
 파일의 잠금을 해제하는 암호를 입력합니다. 암호를 아는 사용자만 키를 복원할 수 있습니다. 이처럼 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 강력한 암호 정책을 적용합니다. 암호는 8자 이상이어야 하며 대/소문자 조합과 하나 이상의 기호를 포함해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services 암호화 키 백업 및 복원](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [암호화 키 삭제 및 다시 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [SSRS Configuration Manager &#40;보고서 서버를 초기화&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [SSRS Configuration Manager &#40;암호화 된 보고서 서버 데이터 저장&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [SSRS 기본 모드 &#40;암호화 키&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
