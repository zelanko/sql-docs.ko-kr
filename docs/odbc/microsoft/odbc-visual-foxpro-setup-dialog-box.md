---
title: ODBC Visual FoxPro 설치 대화 상자가 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d9a21f344687878d1a5b63073f1e23078386868
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 설정 대화 상자
**ODBC Visual FoxPro 설정** 대화 상자를 사용 하면 추가 하거나 Visual FoxPro 데이터 원본을 변경할 수 있습니다.  
  
 드라이버를 다운로드 하려면 [Visual FoxPro ODBC 드라이버 다운로드 사이트](http://go.microsoft.com/fwlink/?LinkId=121318)합니다.  
  
## <a name="dialog-box-options"></a>대화 상자 옵션  
 **데이터 원본 이름**  
 데이터 원본에 대해 하는 데 사용할 이름을 입력 합니다.  
  
 **설명**  
 데이터 원본에 대 한 설명을 입력 합니다.  
  
 **데이터베이스 유형**  
 원하는 데이터 원본에 연결 하는 데이터베이스의 유형을 선택할 수 있습니다.  
  
 **Visual FoxPro 데이터베이스 (합니다. DBC)**  
 Visual FoxPro 데이터 원본 연결 되도록 지정 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) (.dbc 파일) 및 모든 테이블 및 데이터베이스의 뷰를 로컬에 있습니다.  
  
 **사용 가능한 테이블 디렉터리**  
 데이터 원본의 디렉터리에 연결 되도록 지정 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. 모든 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) ODBC 카탈로그 함수에서와 같은 동일한 디렉터리에 있는 테이블을 무시 [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 또는 [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)합니다. 통해 전송 하는 SQL SELECT 문을 사용 하 여 데이터베이스 테이블에 액세스할 수 있습니다 [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) 및 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)합니다.  
  
 **경로**  
 데이터베이스 또는 데이터 원본을 연결 하는 사용 가능한 테이블의 디렉터리에 대 한 이름과 경로 표시 합니다.  
  
 **찾아보기**  
 시스템 및 데이터베이스 또는 데이터 원본에 연결 하려는 디렉터리에 대 한 네트워크를 검색할 수 있습니다.  
  
 **옵션**  
 Visual FoxPro ODBC 드라이버 옵션을 설정할 수 있도록 대화 상자를 확장 합니다.  
  
## <a name="driver"></a>드라이버  
 **데이터 정렬 순서**  
 필드 정렬 되는 시퀀스입니다. 기본 순서는 운영 체제의 언어 버전에서 지원 되는 시퀀스를 반영 합니다. 목록이 지원 되는 데이터 정렬 시퀀스에 대 한 참조 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)합니다.  
  
 **단독**  
 이 확인란을 선택 하면 드라이버는 데이터 소스를 사용 하 여 데이터를 액세스 하는 경우에 Visual FoxPro 데이터베이스를 엽니다. 데이터베이스를 단독으로 열은 데이터베이스 또는 데이터베이스의 테이블 다른 사용자가 액세스할 수 없습니다. 단독으로 열려 있는 데이터베이스 내의 테이블 SHARED로 열립니다. 닫도록 테이블을 사용 하 여는 [단독 설정](../../odbc/microsoft/set-exclusive-command.md) 명령입니다. 이 확인란은 사용할 수 없습니다. 때 **데이터베이스 유형** 로 설정 된 **자유 테이블 디렉터리**합니다.  
  
 **Null**  
 ALTER TABLE과 CREATE TABLE을 사용 하 여 만든 열에 null 값이 허용 여부를 결정 합니다. Null ON으로 설정 하면 삽입 – SQL 삽입 – SQL에에서 포함 되지 모든 열에 null 값을 삽입... VALUE 절입니다. Null은 OFF는 빈 값이 삽입 됩니다. 또한 다음 코드 처럼 전달 된 연결 문자열을 통해이 옵션을 제어할 수 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **삭제**  
 삭제 된 것으로 표시 된 행이 반환 되는지 여부를 결정 합니다. 또한 다음 코드 처럼 전달 된 연결 문자열을 통해이 옵션을 제어할 수 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **백그라운드에서 데이터를 인출 합니다.**  
 (점진적 인출) 백그라운드에서 인출 되는 레코드 또는 응용 프로그램 결과 집합의 모든 레코드 인출 될 때까지 기다립니다 있는지 여부를 결정 합니다.
