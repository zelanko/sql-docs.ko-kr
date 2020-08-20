---
description: MSSQLSERVER_5515
title: MSSQLSERVER_5515 | Microsoft 문서
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: aecbc4ad6ee5c3f8a0ebcf596dca0a06392acedf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470913"
---
# <a name="mssqlserver_5515"></a>MSSQLSERVER_5515
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|5515|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|FS_OPEN_CONTAINER_FAILED|  
|메시지 텍스트|FILESTREAM 파일의 컨테이너 디렉터리 ''%.*ls''을(를) 열 수 없습니다. 운영 체제에서 Windows 상태 코드 0x%x을(를) 반환했습니다.|  
  
## <a name="explanation"></a>설명  
FILESTREAM 파일에 대해 지정된 컨테이너 디렉터리를 열 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
오류의 원인은 해당 Windows 상태 코드를 참조하십시오.  
  
