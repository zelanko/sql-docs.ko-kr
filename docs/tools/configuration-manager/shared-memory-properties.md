---
title: "공유 메모리 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b0642c91c2cd460723b482d079eb9da86b5345b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="shared-memory-properties"></a>공유 메모리 속성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용 하 여는 **프로토콜**페이지에 **공유 메모리 속성** 대화 상자를 사용 하도록 설정 하거나 공유 메모리 프로토콜을 사용 하지 않도록 설정 합니다. 공유 메모리는 가장 간단한 프로토콜이며 구성 가능한 설정이 없습니다. 공유 메모리 프로토콜을 사용하는 클라이언트는 동일한 컴퓨터에서 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에만 연결할 수 있으므로 대부분의 데이터베이스 작업에 유용하지 않습니다. 다른 프로토콜이 제대로 구성되지 않는 것으로 의심되는 경우 문제 해결에 공유 메모리 프로토콜을 사용하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다. 공유 메모리 프로토콜은 기본적으로 활성화 상태입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [네트워크 프로토콜 선택](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
