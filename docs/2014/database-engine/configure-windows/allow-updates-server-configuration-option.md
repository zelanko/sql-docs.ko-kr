---
title: allow updates 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6cf28b18bcad06be7383b98dee72810c4e6157c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62786992"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates 서버 구성 옵션
  이 옵션은 **sp_configure** 저장 프로시저에 계속 제공되지만 이 옵션의 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 없습니다(설정의 영향 없음). 시스템 테이블에 대한 직접 업데이트는 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **allow updates** 옵션을 변경하면 RECONFIGURE 문이 실패합니다. **allow updates** 옵션에 대한 변경 내용을 모든 스크립트에서 제거해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
