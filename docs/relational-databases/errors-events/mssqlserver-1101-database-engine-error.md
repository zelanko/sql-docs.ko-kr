---
title: MSSQLSERVER_1101 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 676f0d1d131e8cc1a1c5265384bcd53cf11e9dab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116190"
---
# <a name="mssqlserver1101"></a>MSSQLSERVER_1101
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
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
  
