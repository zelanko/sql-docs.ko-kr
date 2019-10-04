---
title: 백업 암호화 키 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a0b2c2e597ef7069bcc51fb885a2e810871bfbb5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952654"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>백업 암호화 키(SSRS 기본 모드)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 암호화 키를 사용하여 보고서 서버 데이터베이스에 저장된 중요한 데이터를 보호합니다. 암호화된 연결 문자열 및 자격 증명에 계속 액세스하려 이 키를 백업해야 합니다. 보고서 서버 데이터베이스를 다른 컴퓨터로 이동하거나 보고서 서버 서비스 계정의 사용자 이름 또는 암호를 변경할 경우 이 키의 복사본을 백업해야 합니다. 두 작업을 수행하려면 이전에 만든 백업 복사본에서 키를 복원해야 합니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
 암호화 키 백업 대화 상자를 열려면 **구성 관리자의 탐색 창에서** 암호화 키 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 클릭한 다음 **백업**을 클릭합니다. 이 대화 상자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자의 서비스 계정 페이지를 사용하여 서비스 계정을 업데이트할 때도 나타납니다. @No__t-0 Configuration Manager에 대 한 자세한 내용은 [ &#40;Reporting Services 구성 관리자 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)를 참조 하세요.  
  
## <a name="options"></a>변수  
 **파일 위치**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 파일 이름과 위치를 대칭 키에 지정합니다. 대칭 키는 일반 텍스트로 저장되지 않습니다. 해당 파일을 보호하려면 암호를 입력해야 합니다.  
  
 **암호**  
 무단 액세스로부터 파일을 보호하는 암호를 입력합니다. 암호를 아는 사용자만 파일 내에서 잠긴 키를 복원할 수 있습니다. 이처럼 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 강력한 암호 정책을 적용합니다. 암호는 8자 이상이어야 하며 대/소문자 조합과 하나 이상의 기호를 포함해야 합니다.  
  
 **암호 확인**  
 입력한 암호를 다시 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services 암호화 키 백업 및 복원](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [암호화 키 삭제 및 다시 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [암호화 키 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
