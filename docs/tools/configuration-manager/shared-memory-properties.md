---
title: "공유 메모리 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71ed92d7b9ceffa23b89082526b69a10504c7ef6
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="shared-memory-properties"></a>공유 메모리 속성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
**공유 메모리 속성**대화 상자의 **프로토콜** 페이지를 사용하여 공유 메모리 프로토콜을 활성화 또는 비활성화할 수 있습니다. 공유 메모리는 가장 간단한 프로토콜이며 구성 가능한 설정이 없습니다. 공유 메모리 프로토콜을 사용하는 클라이언트는 동일한 컴퓨터에서 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에만 연결할 수 있으므로 대부분의 데이터베이스 작업에 유용하지 않습니다. 다른 프로토콜이 제대로 구성되지 않는 것으로 의심되는 경우 문제 해결에 공유 메모리 프로토콜을 사용하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다. 공유 메모리 프로토콜은 기본적으로 활성화 상태입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [네트워크 프로토콜 선택](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [공유 메모리 프로토콜을 사용 하 여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
