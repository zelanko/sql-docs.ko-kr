---
title: MSSQLSERVER_50000 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 594918b167dd00ec21ee755cb302ca5c255092e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082684"
---
# <a name="mssqlserver50000"></a>MSSQLSERVER_50000
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|제품 버전|11.0|  
|이벤트 ID|50000|  
|이벤트 원본|SETUP|  
|구성 요소|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|심볼 이름||  
|메시지 텍스트|'%.*ls' 파일을 읽는 동안 네트워크가 오류가 발생했습니다.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 이미 설치되어 있는 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 설치하거나 업데이트하려 했습니다. 기존 설치는 sqlncli.msi에서 이름이 바뀐 MSI 파일에서 설치되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류를 해결하려면 기존의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 버전을 제거하십시오. 이 오류가 발생하지 않도록 하려면 sqlncli.msi로 이름이 지정되지 않은 MSI 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 설치하지 마십시오.  
  
## <a name="internal-only"></a>내부 전용  
  