---
title: allow updates 서버 구성 옵션 | Microsoft Docs
description: 사용되지 않는 SQL Server 구성 옵션인 '업데이트 허용'에 대해 알아봅니다. 이 옵션을 사용하면 RECONFIGURE 문이 어떻게 실패하는지 알아봅니다.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6e4cde898f4b7c95fa3dd46d23d073ba47b5fb43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725261"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 옵션은 **sp_configure** 저장 프로시저에 계속 제공되지만 이 옵션의 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 없습니다(설정의 영향 없음). 시스템 테이블에 대한 직접 업데이트는 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **allow updates** 옵션을 변경하면 RECONFIGURE 문이 실패합니다. **allow updates** 옵션에 대한 변경 내용을 모든 스크립트에서 제거해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
