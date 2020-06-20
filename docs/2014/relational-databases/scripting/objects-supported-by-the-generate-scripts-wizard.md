---
title: 스크립트 생성 마법사에 지원되는 개체
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ddc1da0d2f87fc12dfbe034a683802f54b7d34f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85009749"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>스크립트 생성 마법사에 지원되는 개체
  스크립트 생성 및 게시 마법사는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 지원되는 개체의 하위 집합을 지원합니다.  
  
## <a name="supported-objects"></a>지원되는 개체  
 다음 표에서는 스크립트 생성 및 게시 마법사가 지원하는 개체를 보여 줍니다.  
  
||||||  
|-|-|-|-|-|  
|애플리케이션 역할|데이터베이스 역할|스키마|사용자 정의 집계|보기<sup>1</sup>|  
|어셈블리|DEFAULT 제약 조건|저장 프로시저<sup>1</sup>|사용자 정의 데이터 형식|XML 스키마 컬렉션|  
|CHECK 제약 조건|전체 텍스트 카탈로그|동의어|사용자 정의 함수||  
|CLR (공용 언어 런타임) 저장 프로시저<sup>1</sup>|인덱스|테이블|사용자 정의 테이블||  
|CLR 사용자 정의 함수|규칙|사용자<sup>2</sup>|사용자 정의 형식||  
  
 <sup>1</sup> 암호화 하지 않고 게시 됩니다.  
  
 <sup>2</sup> 데이터베이스에 있는 시스템 사용자 이외의 모든 사용자는 역할로 게시 됩니다.  
  
  
