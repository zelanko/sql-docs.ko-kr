---
title: ODBC 비주얼 폭스프로 설치 대화 상자 | 마이크로 소프트 문서
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
ms.openlocfilehash: ef7ac702a69342833c6dfffa0ffc9cdd0ac2857e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298083"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 설치 대화 상자
**ODBC Visual FoxPro 설치** 설정 대화 상자를 사용하면 Visual FoxPro 데이터 원본을 추가하거나 변경할 수 있습니다.  
  
 드라이버를 다운로드하려면 [Visual FoxPro ODBC 드라이버 다운로드 사이트를](https://go.microsoft.com/fwlink/?LinkId=121318)참조하십시오.  
  
## <a name="dialog-box-options"></a>대화 상자 옵션  
 **데이터 원본 이름**  
 데이터 원본에 사용할 이름을 입력합니다.  
  
 **설명**  
 데이터 원본에 대한 설명을 입력합니다.  
  
 **데이터베이스 유형**  
 데이터 원본에 연결할 데이터베이스 유형을 선택할 수 있습니다.  
  
 **비주얼 폭스프로 데이터베이스(. DBC)**  
 데이터 원본이 Visual FoxPro 데이터베이스(.dbc 파일)와 데이터베이스의 모든 테이블 및 로컬 뷰에 연결되도록 지정합니다. [database](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 **무료 테이블 디렉토리**  
 데이터 원본이 [무료 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)디렉터리에 연결되도록 지정합니다. 동일한 디렉터리에 있는 모든 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md) 테이블은 SQLColumns 또는 [SQLTable](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)과 같은 ODBC 카탈로그 함수에서 [무시됩니다.](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 데이터베이스 테이블은 [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) 및 [SQLExecDirect를](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)통해 전송된 SQL SELECT 문을 사용하여 액세스할 수 있습니다.  
  
 **경로**  
 데이터베이스의 경로와 이름을 표시하거나 데이터 원본이 연결되는 무료 테이블의 디렉토리를 표시합니다.  
  
 **찾아보기**  
 시스템 및 네트워크를 검색하여 데이터 원본을 연결하려는 데이터베이스 또는 디렉터리를 검색할 수 있습니다.  
  
 **옵션**  
 Visual FoxPro ODBC 드라이버 옵션을 설정할 수 있도록 대화 상자를 확장합니다.  
  
## <a name="driver"></a>드라이버  
 **정렬 시퀀스**  
 필드가 정렬되는 시퀀스입니다. 기본 시퀀스는 운영 체제의 언어 버전에서 지원하는 시퀀스를 반영합니다. 지원되는 정렬 시퀀스 목록은 [COLLATE SET을](../../odbc/microsoft/set-collate-command.md)참조하십시오.  
  
 **단독**  
 이 확인란을 선택하면 데이터 원본을 사용하여 데이터에 액세스할 때 드라이버가 Visual FoxPro 데이터베이스를 단독으로 엽니다. 데이터베이스를 단독으로 여는 동안에는 다른 사용자가 데이터베이스 또는 데이터베이스의 테이블에 액세스할 수 없습니다. 단독으로 열린 데이터베이스 내의 테이블은 SHARED로 열립니다. 테이블을 단독으로 열려면 단독 [설정](../../odbc/microsoft/set-exclusive-command.md) 명령을 사용합니다. **데이터베이스 유형이** 사용 가능한 테이블 **디렉터리로**설정되어 있을 때 이 확인란을 사용하지 않도록 설정합니다.  
  
 **Null**  
 ALTER TABLE 및 CREATE TABLE으로 만든 열이 null 값을 허용하는지 여부를 결정합니다. Null ON을 설정하면 INSERT - SQL은 INSERT - SQL에 포함되지 않은 열에 null 값을 삽입합니다. 값 절입니다. Null이 꺼져 있으면 공백이 삽입됩니다. 다음 코드에서와 같이 전달된 연결 문자열을 통해 이 옵션을 제어할 수도 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **삭제**  
 삭제됨으로 표시된 행이 반환되는지 여부를 결정합니다. 다음 코드에서와 같이 전달된 연결 문자열을 통해 이 옵션을 제어할 수도 있습니다.  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **백그라운드에서 데이터 가져오기**  
 레코드를 백그라운드에서 가져올지(프로그레시브 페칭) 또는 결과 집합의 모든 레코드가 가져올 때까지 응용 프로그램이 대기할지 여부를 결정합니다.
