---
title: 공유 메모리 속성
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f7c8a4dd37c0283fa6c122a7be4a7eb1f6b849fa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306922"
---
# <a name="shared-memory-properties"></a>공유 메모리 속성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  **공유 메모리 속성**대화 상자의 **프로토콜** 페이지를 사용하여 공유 메모리 프로토콜을 활성화 또는 비활성화할 수 있습니다. 공유 메모리는 가장 간단한 프로토콜이며 구성 가능한 설정이 없습니다. 공유 메모리 프로토콜을 사용하는 클라이언트는 동일한 컴퓨터에서 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에만 연결할 수 있으므로 대부분의 데이터베이스 작업에 유용하지 않습니다. 다른 프로토콜이 제대로 구성되지 않는 것으로 의심되는 경우 문제 해결에 공유 메모리 프로토콜을 사용하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다. 공유 메모리 프로토콜은 기본적으로 활성화 상태입니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로토콜 선택](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
