---
title: 암호화 키 구성 및 관리(SSRS 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16a1851a46b6602bc9d92d5c7e0111ece8701d43
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222513"
---
# <a name="configure-and-manage-encryption-keys-ssrs-configuration-manager"></a>암호화 키 구성 및 관리(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 암호화 키를 사용하여 보고서 서버 데이터베이스에 저장된 연결 정보 및 자격 증명을 보호합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 암호화는 중요한 데이터를 보호하는 데 사용되는 공개 키, 개인 키 및 대칭 키의 조합을 통해 지원됩니다. 대칭 키는 보고서 서버의 설치 또는 구성 과정에서 보고서 서버를 초기화하는 동안 생성되며, 보고서 서버에서 이 서버에 저장된 중요한 데이터를 암호화하는 데 사용됩니다. 공개 키 및 개인 키는 운영 체제에서 생성되며 대칭 키를 보호하는 데 사용됩니다. 보고서 서버 데이터베이스의 중요한 데이터를 저장하는 각 보고서 서버 인스턴스당 하나의 공개 키 및 개인 키 쌍이 생성됩니다.  
  
 암호화 키 관리는 대칭 키 백업 복사본을 만들고 키를 복원, 삭제 또는 변경하는 시기와 방법을 이해하는 작업으로 구성됩니다. 보고서 서버 설치를 마이그레이션하거나 수평적 스케일 아웃 배포를 구성하는 경우 새 설치에 적용할 수 있도록 대칭 키의 백업 복사본이 있어야 합니다.  
  
> [!IMPORTANT]  
>  Reporting Services 암호화 키를 주기적으로 변경하는 것은 최상의 보안 권장 방법입니다. Reporting Services의 중요 버전 업그레이드 직후에 키를 변경하는 것이 가장 좋습니다. 업그레이드 후에 키를 변경하면 업그레이드 주기를 벗어나 Reporting Services 암호화 키를 변경할 경우에 발생하는 추가 서비스 중단이 최소화됩니다.  
  
 대칭 키를 관리하기 위해 Reporting Services 구성 도구나 **rskeymgmt** 유틸리티를 사용할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 포함된 도구는 대칭 키 관리에만 사용됩니다(공개 키 및 개인 키는 운영 체제에서 관리됨). Reporting Services 구성 도구 및 **rskeymgmt** 유틸리티는 모두 다음 태스크를 지원합니다.  
  
-   보고서 서버 설치를 복구하는 데 사용할 수 있도록 또는 계획된 마이그레이션의 일환으로 대칭 키의 복사본을 백업합니다.  
  
-   이전에 저장한 대칭 키를 보고서 서버 데이터베이스로 복원하여 새 보고서 서버 인스턴스가 원래 암호화하지 않았던 기존 데이터에 액세스할 수 있도록 합니다.  
  
-   암호화된 데이터에 더 이상 액세스할 수 없는 경우에 보고서 서버 데이터베이스에서 암호화된 데이터를 삭제합니다.  
  
-   대칭 키가 노출되는 경우에 대칭 키를 다시 만들고 데이터를 다시 암호화합니다. 최상의 보안을 위해 대칭 키를 주기적으로(예: 몇 달에 한 번씩) 다시 만들어 키 해독을 시도하는 사이버 공격으로부터 보고서 서버 데이터베이스를 보호해야 합니다.  
  
-   여러 보고서 서버가 단일 보고서 서버 데이터베이스 및 해당 데이터베이스에 대해 해독 가능한 암호화를 제공하는 대칭 키를 공유하는 보고서 서버 스케일 아웃 배포에서 보고서 서버 인스턴스를 추가하거나 제거합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [보고서 서버 초기화 &#40;SSRS 구성 관리자&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
 암호화 키의 생성 방법을 설명합니다.  
  
 [Reporting Services 암호화 키 백업 및 복원](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 암호화 키를 백업한 후 복원하여 보고서 서버 설치를 복구 또는 마이그레이션하는 방법을 설명합니다.  
  
 [암호화 된 보고서 서버 데이터 저장 &#40;SSRS 구성 관리자&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 보고서 서버의 암호화에 대해 설명합니다.  
  
 [삭제 및 다시 암호화 키를 만들기 &#40;SSRS 구성 관리자&#41;](ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 대칭 키를 새 버전으로 바꾸는 방법과 대칭 키의 유효성을 검사할 수 없는 경우 다시 시작하는 방법을 설명합니다.  
  
 [추가 하 고 스케일 아웃 배포에 대 한 암호화 키를 제거 &#40;SSRS 구성 관리자&#41;](add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 암호화 키를 추가 및 제거하여 스케일 아웃 배포에 속하는 보고서 서버를 제어하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [암호화 된 보고서 서버 데이터 저장 &#40;SSRS 구성 관리자&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
