---
title: 서버 속성(프로세서 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 42eaf4bc1742c5d9ff101c308d6c120ceb8f3ef8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68026124"
---
# <a name="server-properties---processors-page"></a>서버 속성 - 프로세서 페이지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 프로세서 옵션을 확인하거나 수정할 수 있습니다. 프로세서 선호도 설정은 프로세서가 두 개 이상 설치되어 있는 경우에만 활성화됩니다.  
  
## <a name="options"></a>옵션  
 **프로세서 선호도**  
 특정 스레드에 프로세서를 할당하여 프로세서를 다시 로드해야 하는 필요성을 없애고 프로세스 간의 스레드 마이그레이션을 줄입니다. 자세한 내용은 [affinity mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)을 참조하세요.  
  
 **I/O 선호도**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O를 지정된 CPU 하위 집합에 바인딩합니다. 자세한 내용은 [affinity Input-Output mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)을 참조하세요.  
  
 **모든 프로세서에 대해 자동으로 프로세서 선호도 마스크 설정**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 프로세서 선호도를 자동으로 설정하도록 합니다.  
  
 **모든 프로세서에 대해 자동으로 I/O 선호도 마스크 설정**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 I/O 선호도를 자동으로 설정하도록 합니다.  
  
 **최대 작업자 스레드 수**  
 0으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 작업자 스레드 수를 동적으로 설정합니다. 이 설정은 대부분의 시스템에 적합합니다. 그러나 시스템 구성에 따라 이 옵션을 특정 값으로 설정하면 성능이 향상되기도 합니다. 자세한 내용은 [Configure the max worker threads Server Configuration Option](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)을 참조하세요.  
  
 **SQL Server 우선 순위 높임**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 일정 예약 우선 순위를 같은 컴퓨터의 다른 프로세스보다 높여서 실행할지 여부를 지정합니다. 자세한 내용은 [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)을 참조하세요.  
  
 **Windows 파이버(경량 풀링) 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 스레드 대신 Windows 파이버를 사용합니다. 이 옵션은 Windows 2003 Server Edition에서만 사용할 수 있습니다. 자세한 내용은 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 참조하세요.  
  
 **구성 값**  
 이 창의 옵션에 대해 구성된 값을 표시합니다. 이러한 값을 변경한 후에는 **실행 값** 을 클릭하여 변경 사항이 적용되었는지 여부를 확인합니다. 변경 사항이 적용되지 않은 경우 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야 합니다.  
  
 **실행 값**  
 이 창의 옵션에 대한 현재 실행 값을 볼 수 있습니다. 이 값은 읽기 전용입니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
