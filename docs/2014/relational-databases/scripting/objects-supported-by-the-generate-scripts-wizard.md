---
title: 스크립트 생성 마법사에 지원되는 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: 5
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f102fa4366106581c5f3ec4ff141d537531dbaa4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081058"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>스크립트 생성 마법사에 지원되는 개체
  스크립트 생성 및 게시 마법사는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 지원되는 개체의 하위 집합을 지원합니다.  
  
## <a name="supported-objects"></a>지원되는 개체  
 다음 표에서는 스크립트 생성 및 게시 마법사가 지원하는 개체를 보여 줍니다.  
  
||||||  
|-|-|-|-|-|  
|응용 프로그램 역할|데이터베이스 역할|스키마|사용자 정의 집계|보기<sup>1</sup>|  
|어셈블리|DEFAULT 제약 조건|저장 프로시저<sup>1</sup>|사용자 정의 데이터 형식|XML 스키마 컬렉션|  
|CHECK 제약 조건|전체 텍스트 카탈로그|동의어|사용자 정의 함수||  
|CLR (공용 언어 런타임) 저장 프로시저<sup>1</sup>|인덱스|Table|사용자 정의 테이블||  
|CLR 사용자 정의 함수|규칙|사용자<sup>2</sup>|사용자 정의 형식||  
  
 <sup>1</sup> 암호화 하지 않고 게시 합니다.  
  
 <sup>2</sup> 데이터베이스에 있는 모든 시스템이 아닌 사용자는 역할로 게시 됩니다.  
  
  