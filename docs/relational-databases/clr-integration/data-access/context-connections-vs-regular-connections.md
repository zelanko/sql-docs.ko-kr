---
title: 일반 vs입니다. 컨텍스트 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 96d2b5962ee5925140b7e84e658500b17f20b8bd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="context-connections-vs-regular-connections"></a>컨텍스트 연결 vs입니다. 일반 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  원격 서버에 연결할 때는 컨텍스트 연결 대신 항상 일반 연결을 사용하십시오. 컨텍스트 연결은 대개 저장 프로시저나 함수가 실행 중인 동일한 서버에 연결해야 하는 경우 사용합니다. 컨텍스트 연결을 사용하면 동일한 트랜잭션 공간에서 실행되므로 다시 인증할 필요가 없다는 장점이 있습니다.  
  
 또한 성능이 향상되고 리소스 사용량이 줄어드는 이점도 있습니다. 컨텍스트 연결은 in-process 전용 연결이므로 네트워크 프로토콜 및 전송 계층을 무시하고 "직접" 서버에 연결하여 Transact-SQL 문을 보내고 결과를 받을 수 있습니다. 인증 프로세스도 무시됩니다. 다음 그림은의 기본 구성 요소는 **SqlClient** 일반 연결을 사용 하는 경우 및 컨텍스트 연결을 사용 하는 경우 다른 구성 요소가 서로 상호 작용 방법을 뿐만 아니라 공급자를 관리 합니다.  
  
 ![코드 경로 컨텍스트 및 일반 연결입니다. ] (../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "컨텍스트 및 일반 연결의 코드 경로입니다.")  
  
 컨텍스트 연결은 보다 짧은 코드 경로를 따르고 관련되는 구성 요소가 적으므로 일반 연결보다 빠르게 서버로 요청을 보내고 결과를 받을 수 있습니다. 서버의 쿼리 실행 시간은 컨텍스트 연결을 사용할 때와 일반 연결을 사용할 때 모두 같습니다.  
  
 동일한 서버에 대해 별도의 일반 연결을 열어야 하는 경우도 있습니다. 예를 들어에 설명 된 컨텍스트 연결을 사용 하 여 특정 제한 사항이 [일반 연결 및 컨텍스트 연결에 대 한 제한](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
