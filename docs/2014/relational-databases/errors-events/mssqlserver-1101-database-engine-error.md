---
title: MSSQLSERVER_1101 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce6210f9ab083315fdd99af5c7559a6b98300644
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553948"
---
# <a name="mssqlserver_1101"></a>MSSQLSERVER_1101
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1101|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|NOALLOCPG|  
|메시지 텍스트|파일 그룹 '%.\*ls'에 디스크 공간이 부족하여 데이터베이스 '%1!s!'에 새 페이지를 할당할 수 없습니다. 파일 그룹의 개체를 삭제하거나, 파일 그룹에 파일을 추가하거나, 파일 그룹의 기존 파일에 대해 자동 증가를 설정하여 필요한 공간을 만드십시오.|  
  
## <a name="explanation"></a>설명  
 파일 그룹에 사용 가능한 디스크 공간이 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 다음 동작으로 파일 그룹에 사용 가능한 공간을 만들 수 있습니다.  
  
-   AUTOGROW를 설정합니다.  
  
-   파일에 파일 추가  
  
-   불필요한 인덱스나 파일 그룹 내의 테이블을 삭제하여 디스크 공간을 확보합니다.  
  
  
