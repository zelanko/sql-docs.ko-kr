---
title: 암호화 키 (SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16ac264f89c541f0a864f8b47ed008fa254f181c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095421"
---
# <a name="encryption-keys-ssrs-native-mode"></a>암호화 키(SSRS 기본 모드)
  암호화 키 페이지를 사용하여 보고서 서버의 데이터를 암호화 및 암호 해독하는 데 사용되는 대칭 키를 관리할 수 있습니다. 암호화 키 관리는 보고서 서버 구성에 있어 매우 중요합니다. 대칭 키는 보고서 서버 데이터베이스를 만들 때 자동으로 만들어지고 적용됩니다. 일상적인 유지 관리 작업을 수행할 수 있도록 대칭 키의 백업 복사본을 만드십시오. 다음 유지 관리 태스크를 수행하려면 올바른 대칭 키 복사본이 있어야 합니다.  
  
-   보고서 서버 서비스의 서비스 계정 변경  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 다른 컴퓨터로 마이그레이션  
  
-   기존 보고서 서버 데이터베이스를 공유 또는 사용하도록 새 보고서 서버 인스턴스 구성  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
> [!IMPORTANT]  
>  Reporting Services 암호화 키를 주기적으로 변경하는 것은 최상의 보안 권장 방법입니다. Reporting Services의 중요 버전 업그레이드 직후에 키를 변경하는 것이 가장 좋습니다. 업그레이드 후에 키를 변경하면 업그레이드 주기를 벗어나 Reporting Services 암호화 키를 변경할 경우에 발생하는 추가 서비스 중단이 최소화됩니다.  
  
 보고서 서버 서비스의 사용자 계정을 업데이트했으며 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자 이외의 도구를 사용하여 계정을 변경한 경우 또는 보고서 서버 설치를 새 서버로 마이그레이션하고 있는 경우 대칭 키를 복원해야 합니다.  
  
 대칭 키에 대한 무단 액세스를 방지하기 위해 대칭 키는 보고서 서버 서비스의 프라이빗 키를 사용하여 암호화되어 있습니다. 보고서 서버 서비스에서만 중요한 데이터를 보고서 서버 데이터베이스에 저장하기 위해 대칭 키를 잠금 해제하고 사용할 수 있습니다. 보고서 서버 서비스의 ID를 변경하거나 보고서 서버를 새 컴퓨터로 마이그레이션할 경우 보고서 서버 서비스의 프라이빗 키는 더 이상 대칭 키의 잠금을 해제할 수 없습니다. 대칭 키에 대한 액세스를 복원하려면 새 보고서 서버 서비스의 프라이빗 키를 사용하여 대칭 키를 다시 암호화합니다. 대칭 키 복원 프로세스에서 다시 암호화가 발생합니다.  
  
 대칭 키가 보고서 서버 데이터베이스의 데이터를 암호화 및 암호 해독하는 데 현재 사용되는 동일한 키인 경우에만 대칭 키를 복원합니다. 올바르지 않은 대칭 키를 복원하면 더 이상 중요 데이터에 액세스할 수 없습니다. 이 경우 해당 키를 삭제하고 다시 만듭니다.  
  
> [!IMPORTANT]  
>  대칭 키 삭제 및 다시 만들기 동작은 되돌리거나 실행 취소할 수 없습니다. 키를 삭제 또는 다시 만들기는 현재 설치에 중요한 결과를 가져올 수 있습니다. 키를 삭제하면 대칭 키로 암호화된 모든 기존 데이터도 삭제됩니다. 삭제된 데이터에는 외부 보고서 데이터 원본에 대한 연결 문자열, 저장된 연결 문자열 및 일부 구독 정보가 포함되어 있습니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 시작한 다음 탐색 창에서 링크를 클릭합니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **Backup**  
 대칭 키를 지정한 파일에 복사합니다. 대칭 키는 일반 텍스트로 저장되지 않습니다. 해당 파일을 보호하려면 암호를 입력해야 합니다.  
  
 **복원**  
 이전에 저장한 대칭 키 복사본을 보고서 서버 데이터베이스에 적용합니다. 해당 파일의 잠금을 해제하려면 암호를 입력해야 합니다.  
  
 현재 연결된 보고서 서버 인스턴스에 대한 대칭 키의 이전 복사본은 복원된 버전으로 덮어쓰여집니다. 대칭 키를 복원한 다음에는 해당 보고서 서버 데이터베이스를 사용하는 모든 보고서 서버를 초기화해야 합니다. 보고서 서버를 초기화 하는 방법에 대 한 자세한 내용은 참조 하세요. [보고서 서버 초기화 &#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)합니다.  
  
 **Change**  
 대칭 키를 다시 만들고 보고서 서버 데이터베이스에 암호화된 모든 값을 다시 암호화합니다. 대칭 키를 다시 만들기 전에 보고서 서버 서비스를 중지해야 합니다.  
  
 스케일 아웃 배포의 경우 대칭 키의 모든 복사본은 새 버전으로 바뀝니다. 대칭 키를 변경하기 전에 스케일 아웃 배포에 참가한 서버 목록을 검토하여 올바른 보고서 서버 인스턴스에만 새 키에 대한 액세스 권한이 부여되도록 합니다. 스케일 아웃 배포에 포함되는 서버는 **스케일 아웃 배포** 페이지에 나열되어 있습니다. 키를 다시 만들기 전에 배포의 각 보고서 서버에서 서비스를 중지하십시오.  
  
 데이터 원본 및 구독이 많을 경우 대칭 키를 다시 생성하는 프로세스에 많은 시간이 소요될 수 있습니다.  
  
 **Delete**  
 대칭 키는 물론 연결 문자열, 저장된 자격 증명 등의 암호화된 모든 내용을 삭제합니다. 복원할 수 없는 경우에는 대칭 키만 삭제해야 합니다.  
  
 대칭 키를 삭제한 다음에는 이제 보고서 및 공유 데이터 원본에 없는 연결 문자열 및 저장된 자격 증명을 다시 입력해야 합니다. 암호화된 데이터를 저장하는 배달 확장 프로그램을 사용하는 모든 구독도 업데이트해야 합니다. 여기에는 파일 공유 배달 확장 프로그램 및 암호화된 값을 사용하는 모든 타사 배달 확장 프로그램이 포함됩니다.  
  
 이러한 정보를 자동으로 업데이트하는 방법은 없습니다. 저장된 자격 증명 및 연결 문자열을 사용하는 각 보고서, 구독 및 공유 데이터 원본을 한 번에 하나씩 업데이트해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 F1 도움말 항목 &#40;SSRS 기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services 암호화 키 백업 및 복원](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [암호화 키 삭제 및 다시 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
