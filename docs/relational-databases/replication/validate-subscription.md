---
description: 구독 유효성 검사
title: 구독 유효성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2e80697f75a6234b913e0784b0110873b3c848ac
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88470150"
---
# <a name="validate-subscription"></a>구독 유효성 검사
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  **구독 유효성 검사** 대화 상자를 사용하여 다음에 구독에 대한 병합 에이전트가 실행될 때 병합 게시에 대한 해당 구독의 유효성을 검사하도록 지정할 수 있습니다. 유효성 검사 결과는 복제 모니터에 표시됩니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)을 참조하세요.  
  
 또한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시를 마우스 오른쪽 단추로 클릭하고 **모든 구독 유효성 검사** 를 클릭하여 병합 게시에 대한 모든 구독의 유효성을 검사할 수 있습니다.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>옵션  
 **마지막으로 유효성 검사를 시도한 날짜**  
 유효성 검사의 성공 여부에 상관없이 구독 유효성 검사가 포함된 마지막 병합 에이전트 세션의 날짜입니다.  
  
 **마지막으로 유효성 검사를 성공한 날짜**  
 성공한 구독 유효성 검사가 포함된 마지막 병합 에이전트 세션의 날짜입니다.  
  
 **이 구독 유효성 검사**  
 구독 유효성을 검사하려면 선택합니다.  
  
 **Options**  
 **구독 유효성 검사 옵션** 대화 상자에 액세스하려면 클릭합니다. 이 대화 상자를 사용하여 행 개수 유효성 검사 또는 이진 체크섬 유효성 검사를 사용할지 여부를 지정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
