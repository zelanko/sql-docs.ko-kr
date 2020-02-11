---
title: SET PATH 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57685731bc5eb86381816d0cbb91a4942b5bfeff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063641"
---
# <a name="set-path-command"></a>SET PATH 명령
파일 검색에 대 한 경로를 지정 합니다. 드라이버 관련 정보는 설명 부분을 참조 하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>인수  
 TO [ *Path*]  
 Visual FoxPro에서 검색할 디렉터리를 지정 합니다. 쉼표 또는 세미콜론을 사용 하 여 디렉터리를 구분 합니다.  
  
## <a name="remarks"></a>설명  
 SET PATH를 사용 하면 저장 프로시저 내에서 호출할 수 있는 다른 Visual FoxPro 프로그램의 검색 경로를 지정할 수 있습니다. SET PATH는 연결에 대해 지정한 데이터 원본의 경로를 변경 하지 않습니다.  
  
 *경로를 사용 하지 않고 경로* 를 기본 디렉터리 또는 폴더로 복원 하려면 경로를 사용 하지 않고 경로를 설정 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 저장 프로시저에서 SET PATH를 실행 하는 경우 다음 함수 및 명령에서 무시 됩니다.  
  
-   [Sqltables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) 및 [sqltables](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 와 같은 카탈로그 함수는 새 경로를 무시 하 고 [Sqltables](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) 또는 [sqlexecdirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)에서 데이터 원본에 지정 된 경로를 계속 참조 합니다.  
  
-   SELECT, INSERT, UPDATE, DELETE, CREATE TABLE 등의 명령은 새 경로를 무시 하 고 **Sqlprepare** 또는 **sqlexecdirect**에서 데이터 원본에 지정 된 경로를 계속 참조 합니다.  
  
 저장 프로시저에 경로를 설정 하 고 이후에 경로를 원래 상태로 다시 설정 하지 않은 경우에는 데이터베이스에 대 한 다른 연결이 새 경로를 사용 합니다 (설정 경로 범위는 데이터 세션으로 지정 되지 않았기 때문).  
  
 데이터 원본에 지정 된 것과 다른 디렉터리에서 테이블을 만들거나 선택 하거나 업데이트 하려면 명령을 사용 하 여 파일의 전체 경로를 지정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables(Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
