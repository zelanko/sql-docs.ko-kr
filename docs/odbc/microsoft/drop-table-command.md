---
title: 드롭 테이블 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303424"
---
# <a name="drop-table-command"></a>DROP TABLE 명령
데이터 원본으로 지정된 데이터베이스에서 테이블을 제거하고 디스크에서 삭제합니다.  
  
 Visual FoxPro ODBC 드라이버는 이 명령에 대한 기본 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 비고를 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>설정  
 *Tablename*  
 데이터 원본으로 지정된 데이터베이스에서 제거하고 디스크에서 삭제하도록 테이블을 지정합니다.  
  
 *파일*  
 디스크에서 삭제할 자유 테이블을 지정합니다.  
  
 ?  
 데이터 원본으로 지정된 데이터베이스에서 제거하고 디스크에서 삭제할 테이블을 선택할 수 있는 제거 대화 상자를 표시합니다.  
  
## <a name="remarks"></a>설명  
 DROP TABLE이 발급되면 테이블과 연결된 모든 기본 인덱스, 기본 값 및 유효성 검사 규칙도 제거됩니다. DROP TABLE은 해당 테이블에 제거되는 테이블과 관련된 규칙이나 관계가 있는 경우 데이터 원본으로 지정된 데이터베이스의 다른 테이블에도 영향을 줍니다. 테이블에서 테이블을 제거할 때 규칙 및 관계식은 더 이상 유효하지 않습니다.  
  
## <a name="driver-remarks"></a>운전자 발언  
 응용 프로그램이 ODBC SQL 문 DROP TABLE을 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 다음 표에 표시된 구문을 사용하여 명령을 Visual FoxProDROP TABLE 명령으로 변환합니다.  
  
|ODBC 구문|데이터 원본|비주얼 폭스프로 구문|  
|-----------------|-----------------|--------------------------|  
|드롭 테이블 *기본 테이블 이름*|데이터베이스(.dbc 파일)|테이블 *테이블 이름* 삭제 제거|  
||무료 테이블 디렉토리(.dbf 파일)|*지우기 dbf이름*<br /><br /> *CDx 이름* 지우기<br /><br /> *지울 fptName*|
