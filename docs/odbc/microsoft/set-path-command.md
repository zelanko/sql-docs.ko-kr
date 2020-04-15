---
title: 경로 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e44093c3ea18bc995264a8974726f5af0abe3b3a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300823"
---
# <a name="set-path-command"></a>SET PATH 명령
파일 검색 경로를 지정합니다. 드라이버 관련 정보는 비고를 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>인수  
 TO [ *경로]*  
 Visual FoxPro가 검색할 디렉토리를 지정합니다. 쉼표 또는 세미콜론을 사용하여 디렉터리를 분리합니다.  
  
## <a name="remarks"></a>설명  
 SET PATH를 사용하면 저장 프로시저 내에서 호출할 수 있는 다른 Visual FoxPro 프로그램에 대한 검색 경로를 지정할 수 있습니다. SET PATH는 연결에 대해 지정한 데이터 원본의 경로를 변경하지 않습니다.  
  
 *경로* 없이 경로 설정 PATH를 문제하여 경로를 기본 디렉토리 또는 폴더로 복원합니다.  
  
## <a name="driver-remarks"></a>운전자 발언  
 저장 프로시저에서 SET PATH를 발급하면 다음 함수 및 명령에서 무시됩니다.  
  
-   [SQLTable](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) 및 [SQLColumns와](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 같은 카탈로그 함수는 새 경로를 무시하고 [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) 또는 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)의 데이터 원본에서 지정한 경로를 계속 참조합니다.  
  
-   SELECT, INSERT, UPDATE, DELETE 및 CREATE TABLE과 같은 명령은 새 경로를 무시하고 **SQLPrepare** 또는 **SQLExecDirect**의 데이터 원본에서 지정한 경로를 계속 참조합니다.  
  
 저장된 프로시저에서 SET PATH를 발행하고 이후에 경로를 원래 상태로 다시 설정하지 않으면 데이터베이스에 대한 다른 연결에서 새 경로를 사용합니다(SET PATH는 데이터 세션으로 범위가 지정되지 않음).  
  
 데이터 원본에서 지정한 것 이외의 디렉터리에서 테이블을 만들거나 선택하거나 업데이트하려면 명령으로 파일의 전체 경로를 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 비주얼 폭스프로 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQL열(비주얼 폭스프로 ODBC 드라이버)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect(비주얼 폭스프로 ODBC 드라이버)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables(Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
