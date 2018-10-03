---
title: 예기치 않은 시스템 오류 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 050d7dbf22965cfc3b150f4ff42e3a0e437e7e8b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610361"
---
# <a name="unexpected-system-failures"></a>예기치 않은 시스템 오류
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 컴퓨터 이벤트 로그에서 SYSTEM 이벤트 6008을 검사합니다. 이 이벤트는 예기치 않은 시스템 종료를 나타냅니다. 시스템이 불안정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 호스팅하는 데 필요한 안정성 및 무결성을 제공하지 않을 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 서버가 예기치 않게 다시 시작되는 원인을 찾아 즉시 해결하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다른 컴퓨터로 이동합니다.  
  
  
