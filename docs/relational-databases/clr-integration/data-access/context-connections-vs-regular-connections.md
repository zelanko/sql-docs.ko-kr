---
title: 일반 및 컨텍스트 연결 | 마이크로 소프트 문서
description: SQL Server에서 Transact-SQL 문에 일반 연결을 사용해야 하는 경우가 있지만 컨텍스트 연결은 성능 및 리소스 사용 이점을 제공합니다.
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
ms.openlocfilehash: 881b7463400665d22baaa9b19f13cb5949df0830
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485280"
---
# <a name="context-connections-vs-regular-connections"></a>컨텍스트 연결 과 일반 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  원격 서버에 연결할 때는 컨텍스트 연결 대신 항상 일반 연결을 사용하십시오. 컨텍스트 연결은 대개 저장 프로시저나 함수가 실행 중인 동일한 서버에 연결해야 하는 경우 사용합니다. 컨텍스트 연결을 사용하면 동일한 트랜잭션 공간에서 실행되므로 다시 인증할 필요가 없다는 장점이 있습니다.  
  
 또한 성능이 향상되고 리소스 사용량이 줄어드는 이점도 있습니다. 컨텍스트 연결은 프로세스 전용 연결이므로 네트워크 프로토콜을 우회하여 서버에 "직접" 연락하고 계층을 전송하여 Transact-SQL 문을 보내고 결과를 받을 수 있습니다. 인증 프로세스도 무시됩니다. 다음 그림은 **SqlClient** 관리 공급자의 기본 구성 요소와 일반 연결을 사용할 때 및 컨텍스트 연결을 사용할 때 서로 다른 구성 요소가 상호 작용하는 방법을 보여 주며, 서로 상호 작용하는 방법을 보여 주며,  
  
 ![컨텍스트 및 일반 연결의 코드 경로](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "컨텍스트 및 일반 연결의 코드 경로")  
  
 컨텍스트 연결은 보다 짧은 코드 경로를 따르고 관련되는 구성 요소가 적으므로 일반 연결보다 빠르게 서버로 요청을 보내고 결과를 받을 수 있습니다. 서버의 쿼리 실행 시간은 컨텍스트 연결을 사용할 때와 일반 연결을 사용할 때 모두 같습니다.  
  
 동일한 서버에 대해 별도의 일반 연결을 열어야 하는 경우도 있습니다. 예를 들어 일반 및 컨텍스트 연결에 대한 [제한에](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)설명된 컨텍스트 연결 사용에 대한 특정 제한 사항이 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
