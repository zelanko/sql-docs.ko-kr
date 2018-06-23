---
title: 이진 대형 개체 (Blob)를 읽고 쓰는 UPDATETEXT 문을 수정 | Microsoft Docs
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
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5b0c6df5c9324a35f1f642d366ef8f2780341592
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181722"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>BLOB(Binary Large Object) 읽기/쓰기를 수행하는 UPDATETEXT 문을 수정합니다.
  업그레이드 관리자가 동일한 텍스트 포인터를 사용하여 동일한 BLOB(Binary Large Object) 읽기/쓰기를 수행하는 UPDATETEXT 문을 검색했습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 이러한 방식으로 텍스트 포인터를 사용하는 것을 지원하지 않습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 BLOB을 임시 테이블 또는 테이블 변수로 복사한 다음 이 값을 다시 원래 열에 할당합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
