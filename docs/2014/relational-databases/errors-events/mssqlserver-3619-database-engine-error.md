---
title: MSSQLSERVER_3619 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a82902d69a1d5214b29f43d19ded58c76293ec4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914029"
---
# <a name="mssqlserver3619"></a>MSSQLSERVER_3619
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3619|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SYS_NOLOG|  
|메시지 텍스트|로그 공간이 부족하여 데이터베이스 ID %d에 검사점 레코드를 쓸 수 없습니다. 데이터베이스 관리자에게 문의하여 로그를 자르거나 데이터베이스 로그 파일에 더 많은 공간을 할당하십시오.|  
  
## <a name="explanation"></a>설명  
 트랜잭션 로그에 필요한 디스크 공간이 부족합니다.  
  
## <a name="user-action"></a>사용자 동작  
 로그를 잘라 일부 공간을 확보하거나 로그에 더 많은 공간을 할당하십시오. 자세한 내용은 Server SQL 온라인 설명서의 "꽉 찬 트랜잭션 로그 문제 해결(오류 9002)"을 참조하십시오.  
  
  
