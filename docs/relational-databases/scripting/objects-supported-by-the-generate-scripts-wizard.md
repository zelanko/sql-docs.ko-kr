---
title: "스크립트 생성 마법사에 지원되는 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a4f4804fbc59d9744eaa819ba8f39e1be79de647
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>스크립트 생성 마법사에 지원되는 개체
  스크립트 생성 및 게시 마법사는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 지원되는 개체의 하위 집합을 지원합니다.  
  
## <a name="supported-objects"></a>지원되는 개체  
 다음 표에서는 스크립트 생성 및 게시 마법사가 지원하는 개체를 보여 줍니다.  
  
||||||  
|-|-|-|-|-|  
|응용 프로그램 역할|데이터베이스 역할|스키마|사용자 정의 집계|보기*|  
|어셈블리|DEFAULT 제약 조건|저장 프로시저*|사용자 정의 데이터 형식|XML 스키마 컬렉션|  
|CHECK 제약 조건|전체 텍스트 카탈로그|동의어|사용자 정의 함수||  
|CLR(공용 언어 런타임) 저장 프로시저*|인덱스|테이블|사용자 정의 테이블||  
|CLR 사용자 정의 함수|규칙|사용자**|사용자 정의 형식||  
  
 *암호화하지 않고 게시됩니다.  
  
 **데이터베이스에 있는 시스템 사용자 이외의 모든 사용자는 역할로 게시됩니다.  
  
  
