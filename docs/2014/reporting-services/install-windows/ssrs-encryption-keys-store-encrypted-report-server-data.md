---
title: 암호화된 보고서 서버 데이터 저장(SSRS 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], encryption
- credentials [Reporting Services]
- cryptography [Reporting Services]
- confidential reports [Reporting Services]
- encryption [Reporting Services]
- databases [Reporting Services], encryption
ms.assetid: ac0f4d4d-fc4b-4c62-a693-b86e712e75f2
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 8b3bcd87abe4efd22f8330c8b7dca7d111fb93f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079236"
---
# <a name="store-encrypted-report-server-data-ssrs-configuration-manager"></a>암호화된 보고서 서버 데이터 저장(SSRS 구성 관리자)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 암호화된 값을 보고서 서버 데이터베이스와 구성 파일에 저장합니다. 암호화된 대부분의 값은 보고서에 데이터를 제공하는 외부 데이터 원본에 액세스하기 위한 자격 증명입니다. 이 항목에서는 암호화된 값, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 사용되는 암호화 기능 및 사용자가 알아야 할 기타 저장되는 기밀 데이터 유형에 대해 설명합니다.  
  
## <a name="encrypted-values"></a>암호화된 값  
 다음 목록에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치할 때 저장되는 값에 대해 설명합니다.  
  
-   내부 서버 데이터를 저장하는 보고서 서버 데이터베이스에 연결하기 위해 보고서 서버에서 사용하는 연결 정보 및 자격 증명  
  
     이러한 값은 설치 또는 보고서 서버 구성 중에 지정되고 암호화됩니다. Reporting Services 구성 도구나 **rsconfig** 유틸리티를 사용하여 언제든지 연결 정보를 업데이트할 수 있습니다. 구성 설정은 모든 사용자가 사용할 수 있는 로컬 컴퓨터의 컴퓨터 수준 키를 사용하여 암호화됩니다. 암호화된 보고서 서버 연결 정보는 rsreportserver.config 파일에 저장되며 다른 구성 파일에는 암호화된 설정이 포함되지 않습니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하세요.  
  
-   보고서에 데이터를 제공하는 외부 데이터 원본에 연결하기 위해 보고서 서버에서 사용하는 저장된 자격 증명  
  
     이러한 값은 보고서에 대한 데이터 원본 정보를 구성할 때 정의된 후 보고서 서버 데이터베이스에 암호화된 값으로 저장됩니다. 보고서 서버는 대칭 키를 사용하여 이 데이터를 암호화 및 해독합니다. 저장 된 자격 증명에 대 한 자세한 내용은 참조 [자격 증명을 지정 하 고 보고서 데이터 원본에 대 한 연결 정보](../../integration-services/connection-manager/data-sources.md) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서.  
  
-   보고서에 사용되는 외부 이미지 파일이나 외부 데이터를 검색하기 위해 보고서 서버에서 다른 컴퓨터에 연결하는 데 사용하는 무인 사용자 계정  
  
     원격 컴퓨터에 연결해야 하고 연결하는 데 다른 자격 증명을 사용할 수 없는 경우 이 계정을 사용합니다. 이 계정은 주로 데이터 원본에 액세스하는 데 자격 증명을 사용하지 않는 보고서에 대해 무인 보고서 처리를 지원하기 위해 사용됩니다. 데이터에 액세스할 때 자격 증명을 필요로 하지 않거나 자격 증명을 사용하지 않는 데이터 원본을 기반으로 하는 보고서를 만드는 경우 사용할 보고서 서버에 대해 이 계정을 구성해야 합니다.  
  
     이 계정은 특정 환경에 필요하며 Reporting Services 구성 도구나 **rsconfig**를 사용해야만 만들 수 있습니다. 이 값은 rsreportserver.config 파일에도 저장됩니다. 이 계정은 수동으로 만들어야 합니다. 이 계정 및 사용 방법에 대한 자세한 내용은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.  
  
-   암호화에 사용되는 대칭 키  
  
     이 값은 설치 또는 서버 구성 중에 생성된 후 보고서 서버 데이터베이스에 암호화된 값으로 저장됩니다. 보고서 서버 Windows 서비스는 이 키를 사용하여 보고서 서버 데이터베이스에 저장된 데이터를 암호화 및 해독합니다.  
  
## <a name="encryption-functionality-in-reporting-services"></a>Reporting Services의 암호화 기능  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 Windows 운영 체제에 포함되어 있는 암호화 기능을 사용합니다. 대칭 암호화와 비대칭 암호화가 모두 사용됩니다.  
  
 보고서 서버 데이터베이스의 데이터는 대칭 키를 사용하여 암호화됩니다. 보고서 서버 데이터베이스마다 단일 대칭 키가 있습니다. 이 대칭 키는 Windows에서 생성하는 비대칭 키 쌍의 공개 키를 사용하여 자체적으로 암호화됩니다. 개인 키는 보고서 서버 Windows 서비스 계정이 보유합니다.  
  
 여러 보고서 서버 인스턴스가 동일한 보고서 서버 데이터베이스를 공유하는 보고서 서버 스케일 아웃 배포에서는 모든 보고서 서버 노드가 단일 대칭 키를 사용합니다. 노드마다 공유 대칭 키의 복사본을 갖습니다. 대칭 키의 복사본은 스케일 아웃 배포가 구성될 때 각 노드에 대해 자동으로 만들어집니다. 각 노드에서는 해당 Windows 서비스 계정과 관련된 키 쌍의 공개 키를 사용하여 대칭 키의 복사본을 암호화합니다. 단일 인스턴스 및 스케일 아웃 배포에 대해 대칭 키를 생성하는 방법은 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](ssrs-encryption-keys-initialize-a-report-server.md)를 참조하세요.  
  
> [!NOTE]  
>  보고서 서버 Windows 서비스 계정을 변경하면 비대칭 키가 무효화되고 서버 작동이 중단됩니다. 이 문제를 방지하려면 항상 Reporting Services 구성 도구를 사용하여 서비스 계정 설정을 수정합니다. 구성 도구를 사용하면 해당 키가 자동으로 업데이트됩니다. 자세한 내용은 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)을 참조하세요.  
  
## <a name="other-sources-of-confidential-data"></a>기밀 데이터의 다른 원본  
 보고서 서버는 암호화되지 않은 다른 데이터를 저장하지만 보호해야 할 중요한 정보가 포함될 수도 있습니다. 특히 보고서 기록 스냅숏 및 보고서 실행 스냅숏에는 허가된 사용자를 위한 데이터를 포함할 수 있는 쿼리 결과가 들어 있습니다. 기밀 데이터가 들어 있는 보고서에 스냅숏 기능을 사용하는 경우에는 보고서 서버 데이터베이스의 테이블을 열 수 있는 사용자가 테이블 내용을 검사하여 저장된 보고서의 일부를 볼 수 있으므로 주의해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 사용자의 보안 ID를 기반을 둔 매개 변수를 사용하는 보고서에 대한 캐싱 또는 보고서 기록을 지원하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [암호화 키 구성 및 관리 &#40;SSRS 구성 관리자&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  