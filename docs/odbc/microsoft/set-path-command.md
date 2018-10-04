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
manager: craigg
ms.openlocfilehash: f3d810e66249779b2d3706e92ea39f89a0f87cff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727551"
---
# <a name="set-path-command"></a>SET PATH 명령
파일 검색에 대 한 경로 지정합니다. 드라이버 관련 정보에 대 한 설명을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>인수  
 에 [ *경로*]  
 Visual FoxPro 검색 하려는 디렉터리를 지정 합니다. 디렉터리를 구분 하려면 쉼표 또는 세미콜론을 사용 합니다.  
  
## <a name="remarks"></a>Remarks  
 설정 경로 사용 하면 저장된 프로시저 내에서 호출할 수 있는 기타 Visual FoxPro 프로그램에 대 한 검색 경로 지정할 수 있습니다. 경로 설정에 연결에 대해 지정한 데이터 원본의 경로 변경 되지 않습니다.  
  
 설정 경로를 발급 하지 않고 *경로* 기본 디렉터리 또는 폴더 경로 복원 합니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 저장된 프로시저에서 SET PATH를 실행 하는 경우 다음 함수 및 명령에 의해 무시 됩니다.  
  
-   와 같은 카탈로그 함수 [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) 하 고 [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 새 경로 무시 하 고 데이터 원본에 의해 지정 된 경로 참조 계속 됩니다 [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) 또는[ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)합니다.  
  
-   SELECT, INSERT, UPDATE, DELETE 및 CREATE TABLE 등의 명령을 새 경로 무시 하 고 데이터 원본에 의해 지정 된 경로 참조 하도록 계속 **SQLPrepare** 하거나 **SQLExecDirect**합니다.  
  
 저장된 프로시저에서 SET PATH를 실행 하 고 경로를 원래 상태로 다시 설정 이후에 하지 하는 경우 데이터베이스에 대 한 다른 연결 (경로 설정 데이터 세션 범위가 지정 되지 않습니다) 때문에 새 경로 사용 합니다.  
  
 만들기 선택 하거나 데이터 원본에서 지정 하는 다른 디렉터리에는 테이블을 업데이트 하려는 경우에 명령을 사용 하 여 파일의 전체 경로 지정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables(Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
