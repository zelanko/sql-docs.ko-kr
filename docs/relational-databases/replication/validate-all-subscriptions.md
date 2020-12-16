---
description: 모든 구독 유효성 검사
title: 모든 구독 유효성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: a050ee7d8f018277f4bb55726cd1e674c0ee7e68
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475634"
---
# <a name="validate-all-subscriptions"></a>모든 구독 유효성 검사
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  **모든 구독 유효성 검사** 대화 상자를 사용하여 각 구독에 대한 병합 에이전트가 다음에 실행될 때 병합 게시에 대한 모든 구독의 유효성을 검사할 것인지를 지정할 수 있습니다. 유효성 검사 결과는 복제 모니터에 표시됩니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)을 참조하세요.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 구독을 마우스 오른쪽 단추로 클릭하고 **구독 유효성 검사** 를 클릭하여 단일 구독의 유효성을 검사할 수도 있습니다.  
  
## <a name="options"></a>옵션  
 **행 개수만 확인**  
 구독자의 테이블 행 개수가 게시자의 테이블 행 개수와 같은지 확인하려면 선택합니다. 이 방법은 행 내용이 일치하는지 여부는 확인하지 않습니다. 행 개수 유효성 검사에서는 최소 수준의 데이터 문제 인식을 위한 검사만 수행됩니다.  
  
 **행 개수를 확인하고 체크섬을 비교하여 행 데이터 확인**  
 게시자 및 구독자에서 행 개수를 확인하고 이진 체크섬 알고리즘을 사용하여 모든 데이터의 체크섬을 계산합니다. 행 개수 확인을 실패하면 체크섬 계산이 수행되지 않습니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)]에는 이 옵션이 유효하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
