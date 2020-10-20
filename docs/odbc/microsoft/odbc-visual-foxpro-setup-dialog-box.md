---
description: ODBC Visual FoxPro 설치 대화 상자
title: ODBC Visual FoxPro 설정 대화 상자 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60d65d23a3a72f0194145c9a567f274e2e07ff74
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194328"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 설치 대화 상자
**ODBC Visual Foxpro 설정** 대화 상자를 사용 하 여 visual foxpro 데이터 원본을 추가 하거나 변경할 수 있습니다.  
  
 드라이버를 다운로드 하려면 [Visual FOXPRO ODBC 드라이버 다운로드 사이트](/previous-versions/visualstudio/foxpro/mt490121(v=msdn.10))를 참조 하세요.  
  
## <a name="dialog-box-options"></a>대화 상자 옵션  
 **데이터 원본 이름**  
 데이터 원본에 사용할 이름을 입력 합니다.  
  
 **설명**  
 데이터 원본에 대 한 설명을 입력 합니다.  
  
 **데이터베이스 유형**  
 를 사용 하 여 데이터 원본을 연결 하려는 데이터베이스 유형을 선택할 수 있습니다.  
  
 **Visual FoxPro 데이터베이스 (. DBC**  
 데이터 원본이 Visual FoxPro [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) (dbc 파일)와 데이터베이스의 모든 테이블 및 로컬 뷰에 연결 하도록 지정 합니다.  
  
 **Free 테이블 디렉터리**  
 데이터 원본을 [사용 가능한 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)의 디렉터리에 연결 하도록 지정 합니다. [Sqlcolumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 또는 [SQLCOLUMNS](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)와 같은 ODBC 카탈로그 함수는 동일한 디렉터리에 있는 모든 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 테이블을 무시 합니다. [Sqlexecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) 및 [sqlexecdirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)를 통해 전송 되는 SQL SELECT 문을 사용 하 여 데이터베이스 테이블에 액세스할 수 있습니다.  
  
 **Path**  
 데이터베이스의 경로와 이름 또는 데이터 원본이 연결 된 free 테이블의 디렉터리를 표시 합니다.  
  
 **찾아보기**  
 를 사용 하면 데이터 원본에 연결 하려는 데이터베이스 또는 디렉터리에 대 한 시스템 및 네트워크를 검색할 수 있습니다.  
  
 **옵션**  
 Visual FoxPro ODBC 드라이버 옵션을 설정할 수 있도록 대화 상자를 확장 합니다.  
  
## <a name="driver"></a>드라이버  
 **데이터 정렬 순서**  
 필드가 정렬 되는 순서입니다. 기본 시퀀스는 운영 체제의 언어 버전에서 지원 되는 시퀀스를 반영 합니다. 지원 되는 데이터 정렬 순서 목록은 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)을 참조 하세요.  
  
 **전용**  
 이 확인란을 선택 하면 데이터 원본을 사용 하 여 데이터에 액세스할 때 드라이버가 Visual FoxPro 데이터베이스를 독점적으로 엽니다. 데이터베이스가 단독으로 열리는 동안에는 다른 사용자가 데이터베이스 또는 데이터베이스의 테이블에 액세스할 수 없습니다. 단독으로 열린 데이터베이스 내의 테이블은 공유로 열립니다. 테이블을 독점적으로 열려면 [SET EXCLUSIVE](../../odbc/microsoft/set-exclusive-command.md) 명령을 사용 합니다. **데이터베이스 유형** 을 **Free 테이블 디렉터리로**설정한 경우에는이 확인란을 사용할 수 없습니다.  
  
 **Null**  
 ALTER TABLE 및 CREATE TABLE를 사용 하 여 만든 열에 null 값을 사용할 수 있는지 여부를 결정 합니다. 에 Null을 설정 하는 경우 INSERT sql은 INSERT-SQL에 포함 되지 않은 모든 열에 null 값을 삽입 합니다. 값 절입니다. Null이 해제 되어 있으면 빈가 삽입 됩니다. 다음 코드와 같이 전달 된 연결 문자열을 통해이 옵션을 제어할 수도 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **삭제됨**  
 삭제 된 것으로 표시 된 행이 반환 되는지 여부를 결정 합니다. 다음 코드와 같이 전달 된 연결 문자열을 통해이 옵션을 제어할 수도 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **백그라운드에서 데이터 페치**  
 백그라운드에서 레코드를 페치할 지 (점진적 페치) 아니면 응용 프로그램이 결과 집합의 모든 레코드가 인출 될 때까지 대기 하는지 결정 합니다.