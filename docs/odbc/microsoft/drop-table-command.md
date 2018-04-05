---
title: DROP TABLE 명령을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c6b38eeeba42f1a24520c176fb2f49caac1712e2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="drop-table-command"></a>DROP TABLE 명령
데이터 소스와 지정 된 데이터베이스에서 테이블을 제거 하 고 디스크에서 삭제 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 주의 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>설정  
 *테이블 이름*  
 디스크에서 삭제 하 고 데이터 소스와 지정 된 데이터베이스에서 제거 하는 테이블을 지정 합니다.  
  
 *FileName*  
 디스크에서 삭제 하는 무료 테이블을 지정 합니다.  
  
 ?  
 디스크에서 삭제 하 고 데이터 소스와 지정 된 데이터베이스에서 제거 하는 테이블을 선택할 수 있는 제거 대화 상자를 표시 합니다.  
  
## <a name="remarks"></a>주의  
 DROP TABLE이 실행 되 면 모든 기본 인덱스, 기본값 및 테이블에 연결 된 유효성 검사 규칙도 제거 됩니다. DROP TABLE를 규칙 포함 하는 경우 데이터 소스와 지정 된 데이터베이스 또는 제거 하 고 해당 테이블과 연결 된 관계의 다른 테이블을도 영향을 줍니다. 이 테이블은 데이터베이스에서 제거 하는 경우는 규칙 및 관계가 유효 구분 됩니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램의 데이터 원본에는 ODBC SQL 문을 DROP TABLE 보내면 Visual FoxPro ODBC 드라이버는 다음 표에 표시 된 구문을 사용 하 여 시각적 FoxProDROP TABLE 명령의 명령을 변환 합니다.  
  
|ODBC 구문|데이터 원본|Visual FoxPro 구문|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *기본 테이블 이름*|데이터베이스 (.dbc 파일)|테이블 제거 *TableName* 삭제|  
||사용 가능한 테이블 (.dbf 파일)의 디렉터리|ERASE *dbfName*<br /><br /> ERASE *cdxName*<br /><br /> ERASE *fptName*|
