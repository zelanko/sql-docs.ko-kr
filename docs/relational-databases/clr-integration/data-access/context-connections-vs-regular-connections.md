---
title: 일반 연결 및 컨텍스트 연결 Microsoft Docs
description: SQL Server에서 Transact-sql 문에 대 한 일반 연결을 사용 해야 하는 경우도 있지만, 컨텍스트 연결은 성능 및 리소스 사용 이점을 제공 합니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: 6417a0121a7e290d711690fb0150fdbe908827dd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637516"
---
# <a name="context-connections-vs-regular-connections"></a>컨텍스트 연결 및 일반 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  원격 서버에 연결할 때는 컨텍스트 연결 대신 항상 일반 연결을 사용하십시오. 컨텍스트 연결은 대개 저장 프로시저나 함수가 실행 중인 동일한 서버에 연결해야 하는 경우 사용합니다. 컨텍스트 연결을 사용하면 동일한 트랜잭션 공간에서 실행되므로 다시 인증할 필요가 없다는 장점이 있습니다.  
  
 또한 성능이 향상되고 리소스 사용량이 줄어드는 이점도 있습니다. 컨텍스트 연결은 in-process 전용 연결 이므로 네트워크 프로토콜 및 전송 계층을 무시 하 여 서버에 "직접 연결" 하 여 Transact-sql 문을 보내고 결과를 받을 수 있습니다. 인증 프로세스도 무시됩니다. 다음 그림에서는 일반 연결을 사용 하는 경우와 컨텍스트 연결을 사용 하는 경우 각 구성 요소가 서로 상호 작용 하는 방법 뿐만 아니라 **SqlClient** 관리 공급자의 기본 구성 요소를 보여 줍니다.  
  
 ![컨텍스트 및 일반 연결의 코드 경로](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "컨텍스트 및 일반 연결의 코드 경로")  
  
 컨텍스트 연결은 보다 짧은 코드 경로를 따르고 관련되는 구성 요소가 적으므로 일반 연결보다 빠르게 서버로 요청을 보내고 결과를 받을 수 있습니다. 서버의 쿼리 실행 시간은 컨텍스트 연결을 사용할 때와 일반 연결을 사용할 때 모두 같습니다.  
  
 동일한 서버에 대해 별도의 일반 연결을 열어야 하는 경우도 있습니다. 예를 들어 [일반 및 컨텍스트 연결에 대 한 제한 사항](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)에 설명 된 대로 컨텍스트 연결 사용에 대 한 특정 제한 사항이 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
