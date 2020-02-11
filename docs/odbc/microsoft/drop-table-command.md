---
title: DROP TABLE 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 278950bac7589b8a6b02d894c8133a699c3bd1ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071801"
---
# <a name="drop-table-command"></a>DROP TABLE 명령
데이터 원본을 사용 하 여 지정 된 데이터베이스에서 테이블을 제거 하 고 디스크에서 삭제 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다. 드라이버 관련 정보는 설명 부분을 참조 하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>설정  
 *TableName*  
 데이터 원본을 사용 하 여 지정 된 데이터베이스에서 제거할 테이블을 지정 하 고 디스크에서 삭제 합니다.  
  
 *이름도*  
 디스크에서 삭제할 free 테이블을 지정 합니다.  
  
 ?  
 데이터 원본으로 지정 된 데이터베이스에서 제거 하 고 디스크에서 삭제할 테이블을 선택할 수 있는 제거 대화 상자를 표시 합니다.  
  
## <a name="remarks"></a>설명  
 DROP TABLE을 실행 하면 테이블에 연결 된 모든 주 인덱스, 기본값 및 유효성 검사 규칙도 제거 됩니다. DROP TABLE은 제거 되는 테이블과 연결 된 규칙 또는 관계가 있는 경우 데이터 원본에 지정 된 데이터베이스의 다른 테이블에도 영향을 줍니다. 테이블이 데이터베이스에서 제거 되 면 규칙 및 관계가 더 이상 유효 하지 않습니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문 DROP 테이블을 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 다음 표에 나와 있는 구문을 사용 하 여 명령을 Visual FoxProDROP TABLE 명령으로 변환 합니다.  
  
|ODBC 구문|데이터 원본|Visual FoxPro 구문|  
|-----------------|-----------------|--------------------------|  
|테이블 *기본 테이블 이름* 삭제|데이터베이스 (dbc 파일)|테이블 *TableName* 삭제 제거|  
||자유 테이블 (.dbf 파일)의 디렉터리|*Dbfname* 지우기<br /><br /> *CDXNAME* 지우기<br /><br /> *Fptname* 지우기|
