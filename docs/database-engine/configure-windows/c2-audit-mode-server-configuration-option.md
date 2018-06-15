---
title: c2 audit mode 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ce99919ae03853e35768d21c00a4a096217f1f21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32863668"
---
# <a name="c2-audit-mode-server-configuration-option"></a>c2 audit mode 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  C2 Audit Mode는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 통해 구성하거나 **sp_configure** 에 **c2 audit mode**옵션을 사용하여 구성할 수 있습니다. 이 옵션을 선택하면 문과 개체에 대해 실패한 액세스 시도와 성공한 액세스 시도를 모두 기록하도록 서버가 구성됩니다. 이 정보는 시스템 동작을 파악하고 보안 정책 위반을 추적하는 데 도움이 됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] C2 보안 표준은 Common Criteria 인증으로 대체되었습니다. [common criteria compliance enabled 서버 구성 옵션](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)을 참조하세요.  
  
## <a name="audit-log-file"></a>감사 로그 파일  
 C2 Audit Mode 데이터는 인스턴스의 기본 데이터 디렉터리에 파일로 저장됩니다. 감사 로그 파일 크기가 제한 크기(200MB)에 도달하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 새 파일을 만들고 기존 파일을 닫은 후 새로운 감사 기록을 모두 새 파일에 작성합니다. 이러한 프로세스는 감사 데이터 디렉터리가 꽉 차거나 감사 옵션이 해제될 때까지 계속됩니다. C2 추적의 상태를 확인하려면 sys.traces 카탈로그 뷰를 쿼리합니다.  
  
> [!IMPORTANT]  
>  C2 Audit Mode를 사용하면 로그 파일에 많은 양의 이벤트 정보가 저장되어 파일의 크기가 빠르게 커집니다. 로그 파일이 저장되는 데이터 디렉터리의 공간이 부족하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자동으로 종료됩니다. 감사가 자동으로 시작되도록 설정되어 있으면 감사 프로세스를 생략하도록 하는 **-f** 플래그를 사용하여 인스턴스를 다시 시작하거나 감사 로그를 저장할 수 있는 디스크 공간을 추가로 확보해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 C2 Audit Mode를 설정합니다.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
