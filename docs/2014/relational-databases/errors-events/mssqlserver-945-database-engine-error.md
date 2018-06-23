---
title: MSSQLSERVER_945 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f06aed5f498ed67b7d9335cb37b62b1edb25327e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088427"
---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|945|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DB_IS_SHUTDOWN|  
|메시지 텍스트|파일에 액세스할 수 없거나 메모리 또는 디스크 공간이 부족하여 데이터베이스 '%.*ls'을(를) 열 수 없습니다.  자세한 내용은 SQL Server 오류 로그를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 파일 또는 기타 리소스가 없어 데이터베이스에 액세스할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 메모리, 디스크 공간 또는 사용 권한 오류에 대한 자세한 내용은 오류 로그를 확인합니다. 영향을 받는 데이터베이스에 대한 .mdf 및 .ndf 파일의 위치를 확인하고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용하는 계정에 해당 .mdf 및 .ndf 파일에 대한 액세스 권한이 있는지 확인합니다. 문제를 수정한 후에는 ALTER DATABASE를 사용하여 데이터베이스를 ONLINE으로 설정하고 데이터베이스를 다시 시작합니다.  
  
  