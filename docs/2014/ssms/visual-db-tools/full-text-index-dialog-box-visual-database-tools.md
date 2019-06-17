---
title: 전체 텍스트 인덱스 대화 상자(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adb00f8b0e7cb009420e9843532c3f3d4deb0833
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028420"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>전체 텍스트 인덱스 대화 상자(Visual Database Tools)
  이 대화 상자를 사용하면 전체 텍스트 인덱스를 만들어 데이터베이스 테이블에서 텍스트 기반 열에 대해 전체 텍스트 검색을 수행할 수 있습니다. 전체 텍스트 인덱스는 일반 인덱스를 기반으로 하므로 먼저 일반 인덱스를 만들어야 합니다. 일반 인덱스는 null이 아닌 단일 열에 대해 작성해야 하며, 값이 큰 열보다 값이 작은 열을 선택하는 것이 좋습니다.  
  
> [!NOTE]  
>  전체 텍스트 인덱스를 만들려면 우선 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 나 엔터프라이즈 관리자와 같은 외부 도구를 사용하여 데이터베이스의 전체 텍스트 카탈로그를 만들어야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에서는 전체 텍스트 인덱스 기능을 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="options"></a>변수  
 **선택한 전체 텍스트 인덱스**  
 기존의 전체 텍스트 인덱스를 나열합니다. 인덱스를 선택하면 오른쪽 표에 해당 속성이 표시됩니다. 목록이 비어 있는 경우 테이블에 정의된 전체 텍스트 관계가 없음을 의미합니다.  
  
 **추가**  
 전체 텍스트 인덱스를 새로 만듭니다.  
  
 **Delete**  
 **선택한 전체 텍스트 인덱스** 목록에서 선택한 전체 텍스트 인덱스를 삭제합니다.  
  
 **일반 범주**  
 확장하면 **열** 및 **전체 텍스트 카탈로그 이름**이 표시됩니다.  
  
 **열**  
 검색 가능한 전체 텍스트 열의 이름 목록을 쉼표로 구분하여 표시합니다. 전체 목록을 보려면 속성 필드의 왼쪽에 있는 줄임표 단추( **...** )를 클릭합니다.  
  
 **Full-Text Catalog Name**  
 현재 전체 텍스트 인덱스가 저장되어 있는 전체 텍스트 카탈로그의 이름을 표시합니다. 인덱스를 다른 카탈로그에 저장하려면 카탈로그 이름을 클릭하고 드롭다운 목록에서 다른 이름을 선택합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 나 엔터프라이즈 관리자 같은 외부 도구를 사용하여 카탈로그를 먼저 만들어야 합니다.  
  
 **ID 범주**  
 확장하면 현재 인덱스의 이름 필드가 표시됩니다.  
  
 **이름**  
 현재 전체 텍스트 인덱스에 대해 자동으로 지정된 이름을 표시합니다.  
  
 **테이블 디자이너 범주**  
 확장하면 인덱스 수행 방식을 지정하는 속성이 표시됩니다.  
  
 **활성**  
 현재 전체 텍스트 인덱스를 사용하여 전체 텍스트 검색을 지금 수행할 수 있는지 여부를 나타냅니다.  
  
 **추적 설정 변경**  
 다음 인덱스에 대한 변경 내용 추적 상태를 설명합니다. 수동, 자동 또는 해제.  
  
 **탐색 완료**  
 가장 최근의 탐색이 완료되었는지 여부를 표시합니다. 이 속성 값이 No이면 탐색이 아직 진행 중임을 의미합니다.  
  
 **현재 또는 마지막 탐색의 종료 날짜 및 시간**  
 가장 최근 탐색이 종료된 날짜와 시간을 표시합니다.  
  
 **현재 또는 마지막 탐색의 오류**  
 현재 또는 가장 최근 탐색에서 발생한 오류 개수를 표시합니다.  
  
 **인덱스 버전**  
 탐색을 시작할 당시 테이블의 스키마 버전을 표시합니다.  
  
 **현재 또는 마지막 탐색의 행**  
 현재 또는 가장 최근 탐색에서 업데이트된 행 수를 표시합니다.  
  
 **현재 또는 마지막 탐색의 시작 날짜 및 시간**  
 현재 또는 가장 최근 탐색을 시작한 날짜와 시간을 표시합니다.  
  
 **다음 탐색에 대한 타임스탬프**  
 다음 탐색을 시작할 날짜와 시간을 표시합니다.  
  
 **현재 또는 마지막 탐색의 형식**  
 현재 또는 가장 최근 크롤링 유형을 다음과 같이 표시합니다. 최대 사용, 증분, 업데이트 또는 자동 전파.  
  
 **고유 인덱스 이름**  
 현재 데이터베이스에서 고유한 단일 열 인덱스가 있는 열의 이름에 대한 전체 목록을 표시합니다. 이러한 열은 전체 텍스트 인덱스를 만드는 데 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 인덱싱 마법사 사용](../../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
  
