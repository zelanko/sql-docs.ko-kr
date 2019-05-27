---
title: 지원 되지 않는 전체 텍스트 검색 속성을 사용 하는 저장된 프로시저 수정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093845"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>지원되지 않는 전체 텍스트 검색 속성을 사용하는 저장 프로시저를 수정합니다.
  저장 프로시저가 올바로 수행되도록 하려면 기존 프로시저를 편집하고 제거되었거나 지원되지 않는 전체 텍스트 관련 속성 및 설정을 제거해야 합니다.  
  
## <a name="component"></a>구성 요소  
 전체 텍스트 검색  
  
## <a name="description"></a>Description  
 제거된 전체 텍스트 검색 관련 속성 및 설정은 다음과 같습니다.  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 제거되었거나 지원되지 않는 전체 텍스트 검색 관련 속성 및 설정은 다음과 같습니다.  
  
-   전체 텍스트 카탈로그의 '경로'. 전체 텍스트 카탈로그는 특정 파일 시스템 경로가 없는 논리 개체입니다.  
  
-   SP_FULLTEXT_DATABASE의 설정/해제 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서는 데이터베이스에 대해 전체 텍스트 검색이 기본적으로 항상 사용되도록 설정되기 때문에 이 설정의 영향을 더 이상 받지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 이러한 속성을 제거하도록 저장 프로시저를 수정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
