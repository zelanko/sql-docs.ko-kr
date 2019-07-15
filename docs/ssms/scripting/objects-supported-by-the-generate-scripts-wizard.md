---
title: 스크립트 생성 마법사에 지원되는 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 181afad8fbb3961a61b307a1ac74e8a750003f20
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690194"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>스크립트 생성 마법사에 지원되는 개체
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  스크립트 생성 및 게시 마법사는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 지원되는 개체의 하위 집합을 지원합니다.  
  
## <a name="supported-objects"></a>지원되는 개체  
 다음 표에서는 스크립트 생성 및 게시 마법사가 지원하는 개체를 보여 줍니다.  
  
||||||  
|-|-|-|-|-|  
|애플리케이션 역할|데이터베이스 역할|스키마|사용자 정의 집계|보기*|  
|어셈블리|DEFAULT 제약 조건|저장 프로시저*|사용자 정의 데이터 형식|XML 스키마 컬렉션|  
|CHECK 제약 조건|전체 텍스트 카탈로그|동의어|사용자 정의 함수||  
|CLR(공용 언어 런타임) 저장 프로시저*|인덱스|Table|사용자 정의 테이블||  
|CLR 사용자 정의 함수|규칙|사용자**|사용자 정의 형식||  
  
 *암호화하지 않고 게시됩니다.  
  
 **데이터베이스에 있는 시스템 사용자 이외의 모든 사용자는 역할로 게시됩니다.  
  
  
