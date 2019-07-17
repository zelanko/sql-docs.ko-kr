---
title: DROP TABLE 명령은 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071801"
---
# <a name="drop-table-command"></a>DROP TABLE 명령
데이터 소스를 사용 하 여 지정 된 데이터베이스에서 테이블을 제거 하 고 디스크에서 삭제 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보에 대 한 설명을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>설정  
 *TableName*  
 테이블 데이터 소스를 사용 하 여 지정 된 데이터베이스에서 제거 하 고 디스크에서 삭제 되도록 지정 합니다.  
  
 *FileName*  
 디스크에서 삭제 하려는 사용 가능한 테이블을 지정 합니다.  
  
 ?  
 데이터 소스를 사용 하 여 지정 된 데이터베이스에서 제거 하 고 디스크에서 삭제 되도록 테이블을 선택할 수 있는 제거 대화 상자를 표시 합니다.  
  
## <a name="remarks"></a>설명  
 DROP TABLE을 실행 하면 모든 기본 인덱스, 기본값 및 테이블에 연결 된 유효성 검사 규칙도 제거 됩니다. DROP TABLE은 해당 테이블에는 규칙이 있는 경우 데이터 소스를 사용 하 여 지정 된 데이터베이스를 제거 하 고 테이블에 연결 된 관계의 다른 테이블을도 영향을 줍니다. 데이터베이스에서 테이블 제거 되 면 규칙 및 관계와 유효한 없습니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램의 데이터 원본에는 ODBC SQL 문을 DROP TABLE 보내면 Visual FoxPro ODBC 드라이버 명령은 다음 표에 표시 된 구문을 사용 하 여 Visual FoxProDROP 테이블 명령으로 변환 합니다.  
  
|ODBC 구문|데이터 원본|Visual FoxPro 구문|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *기본 테이블 이름*|데이터베이스 (.dbc 파일)|테이블 제거 *TableName* 삭제|  
||사용 가능한 테이블 (.dbf 파일)의 디렉터리|지울 *dbfName*<br /><br /> 지울 *cdxName*<br /><br /> 지울 *fptName*|
