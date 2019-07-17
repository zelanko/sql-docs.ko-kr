---
title: ODBC Visual FoxPro 설치 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9aa8954cd42ac715b3e6e67e0b0add69d07a570
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915659"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 설치 대화 상자
합니다 **ODBC Visual FoxPro 설치** 대화 상자에서는 추가 하거나 Visual FoxPro 데이터 원본을 변경할 수 있습니다.  
  
 드라이버를 다운로드 하려면 [Visual FoxPro ODBC 드라이버 다운로드 사이트](https://go.microsoft.com/fwlink/?LinkId=121318)합니다.  
  
## <a name="dialog-box-options"></a>대화 상자 옵션  
 **데이터 원본 이름**  
 데이터 원본에 대해 사용 하려는 이름을 입력 합니다.  
  
 **설명**  
 데이터 원본에 대 한 설명을 입력 합니다.  
  
 **데이터베이스 유형**  
 데이터 원본에 연결할 데이터베이스의 유형을 선택할 수 있습니다.  
  
 **Visual FoxPro 데이터베이스 (합니다. DBC)**  
 데이터 원본 Visual FoxPro에 연결 되도록 지정 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) (.dbc 파일) 및 모든 테이블 및 데이터베이스의 로컬 뷰.  
  
 **사용 가능한 테이블 디렉터리**  
 데이터 원본 디렉터리에 연결 되도록 지정 [테이블을 무료](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. 모든 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 와 같은 동일한 디렉터리에는 테이블 ODBC 카탈로그 함수에 의해 무시 됩니다 [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 하거나 [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)합니다. 데이터베이스 테이블을 통해 전송 하는 SQL SELECT 문을 사용 하 여 액세스할 수 있습니다 [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) 하 고 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)합니다.  
  
 **경로**  
 데이터베이스 또는 데이터 원본을 연결 하는 사용 가능한 테이블의 디렉터리에 대 한 이름과 경로 표시 합니다.  
  
 **찾아보기**  
 사용자 시스템 및 데이터베이스 또는 데이터 원본에 연결 하려는 디렉터리에 대 한 네트워크를 검색할 수 있습니다.  
  
 **옵션**  
 Visual FoxPro ODBC 드라이버 옵션을 설정할 수 있도록 대화 상자를 확장 합니다.  
  
## <a name="driver"></a>드라이버  
 **정렬 순서**  
 필드 정렬 되는 시퀀스입니다. 기본 순서는 운영 체제의 언어 버전에서 지원 되는 시퀀스를 반영 합니다. 지원 되는 데이터 정렬 시퀀스의 목록을 참조 하세요 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)합니다.  
  
 **전용**  
 이 확인란을 선택 하면 드라이버는 데이터 소스를 사용 하 여 데이터를 액세스 하는 경우에 Visual FoxPro 데이터베이스를 엽니다. 다른 사용자 데이터베이스는 단독으로 열려 있는 동안 데이터베이스 또는 데이터베이스의 테이블을 액세스할 수 없습니다. 단독으로 열려 데이터베이스 내의 테이블이 SHARED로 열립니다. 닫도록 테이블을 사용 합니다 [전용 설정](../../odbc/microsoft/set-exclusive-command.md) 명령입니다. 이 확인란이 비활성화 되어 때 **데이터베이스 유형** 로 설정 된 **무료 테이블 디렉터리**합니다.  
  
 **Null**  
 ALTER TABLE 및 CREATE TABLE을 사용 하 여 만든 열에서 null 값 허용 여부를 결정 합니다. Null ON으로 설정한 경우 INSERT-SQL INSERT-SQL에에서 포함 되지 않은 모든 열에 null 값을 삽입 하는 중... VALUE 절입니다. 빈 값을 Null가 OFF 이면 삽입 됩니다. 또한 다음 코드와 같이 전달 된 연결 문자열을 통해이 옵션을 제어할 수 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **삭제**  
 삭제 된 것으로 표시 된 행이 반환 되는지 여부를 결정 합니다. 또한 다음 코드와 같이 전달 된 연결 문자열을 통해이 옵션을 제어할 수 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **백그라운드에서 데이터 가져오기**  
 (점진적 인출) 백그라운드에서 인출 되는 레코드 또는 응용 프로그램 결과 집합의 모든 레코드는 인출 될 때까지 대기할 여부를 결정 합니다.
