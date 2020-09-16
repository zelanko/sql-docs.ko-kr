---
description: 전체 텍스트 인덱스 대화 상자(Visual Database Tools)
title: 전체 텍스트 인덱스 대화 상자
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 566239ac238afb66650c50cd9d96c8fa81d3f70c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497146"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>전체 텍스트 인덱스 대화 상자(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
이 대화 상자를 사용하면 전체 텍스트 인덱스를 만들어 데이터베이스 테이블에서 텍스트 기반 열에 대해 전체 텍스트 검색을 수행할 수 있습니다. 전체 텍스트 인덱스는 일반 인덱스를 기반으로 하므로 먼저 일반 인덱스를 만들어야 합니다. 일반 인덱스는 null이 아닌 단일 열에 대해 작성해야 하며, 값이 큰 열보다 값이 작은 열을 선택하는 것이 좋습니다.  
  
> [!NOTE]
> 전체 텍스트 인덱스를 만들려면 우선 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 나 엔터프라이즈 관리자와 같은 외부 도구를 사용하여 데이터베이스의 전체 텍스트 카탈로그를 만들어야 합니다.  
> 
> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에서는 전체 텍스트 인덱스 기능을 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2012 버전에서 지원하는 기능](https://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)을 참조하세요.  
  
## <a name="options"></a>옵션  
**선택한 전체 텍스트 인덱스**  
기존의 전체 텍스트 인덱스를 나열합니다. 인덱스를 선택하면 오른쪽 표에 해당 속성이 표시됩니다. 목록이 비어 있는 경우 테이블에 정의된 전체 텍스트 관계가 없음을 의미합니다.  
  
**추가**  
전체 텍스트 인덱스를 새로 만듭니다.  
  
**Delete**  
**선택한 전체 텍스트 인덱스** 목록에서 선택한 전체 텍스트 인덱스를 삭제합니다.  
  
**일반 범주**  
확장하면 **열** 및 **전체 텍스트 카탈로그 이름**이 표시됩니다.  
  
**열**  
검색 가능한 전체 텍스트 열의 이름 목록을 쉼표로 구분하여 표시합니다. 전체 목록을 보려면 속성 필드의 왼쪽에 있는 줄임표 단추(**...**)를 클릭합니다.  
  
**Full-Text Catalog Name**  
현재 전체 텍스트 인덱스가 저장되어 있는 전체 텍스트 카탈로그의 이름을 표시합니다. 인덱스를 다른 카탈로그에 저장하려면 카탈로그 이름을 클릭하고 드롭다운 목록에서 다른 이름을 선택합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 나 엔터프라이즈 관리자 같은 외부 도구를 사용하여 카탈로그를 먼저 만들어야 합니다.  
  
**ID 범주**  
확장하면 현재 인덱스의 이름 필드가 표시됩니다.  
  
**Name**  
현재 전체 텍스트 인덱스에 대해 자동으로 지정된 이름을 표시합니다.  
  
**테이블 디자이너 범주**  
확장하면 인덱스 수행 방식을 지정하는 속성이 표시됩니다.  
  
**활성**  
현재 전체 텍스트 인덱스를 사용하여 전체 텍스트 검색을 지금 수행할 수 있는지 여부를 나타냅니다.  
  
**추적 설정 변경**  
수동, 자동 또는 해제와 같이 이 인덱스의 변경 내용 추적 상태에 대해 설명합니다.  
  
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
최대, 증분, 업데이트 또는 자동 전파와 같이 현재 또는 가장 최근 탐색의 형식을 표시합니다.  
  
**고유 인덱스 이름**  
현재 데이터베이스에서 고유한 단일 열 인덱스가 있는 열의 이름에 대한 전체 목록을 표시합니다. 이러한 열은 전체 텍스트 인덱스를 만드는 데 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[전체 텍스트 인덱싱 마법사 사용](https://msdn.microsoft.com/3e9d9605-6525-4781-9168-fdaa06db3459)  
[CREATE FULLTEXT INDEX(Transact-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)  
  
