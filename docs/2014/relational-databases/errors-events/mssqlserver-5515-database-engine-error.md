---
title: MSSQLSERVER_5515 | Microsoft 문서
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
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c719c62ecc805be3c3102b0e3457596ab2561817
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088436"
---
# <a name="mssqlserver5515"></a>MSSQLSERVER_5515
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|5515|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|FS_OPEN_CONTAINER_FAILED|  
|메시지 텍스트|FILESTREAM 파일의 컨테이너 디렉터리 ''%.*ls''을(를) 열 수 없습니다. 운영 체제에서 Windows 상태 코드 0x%x을(를) 반환했습니다.|  
  
## <a name="explanation"></a>설명  
 FILESTREAM 파일에 대해 지정된 컨테이너 디렉터리를 열 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 오류의 원인은 해당 Windows 상태 코드를 참조하십시오. 자세한 내용은 참조는 [이벤트 및 오류 메시지 센터](http://go.microsoft.com/fwlink/?linkid=47660)합니다.  
  
  