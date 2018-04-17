---
title: SET 경로 명령을 | Microsoft Docs
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
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 695325b486b485aabc8c28ec439d74cfdaf16fff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="set-path-command"></a>SET 경로 명령
파일 검색에 대 한 경로 지정합니다. 드라이버 관련 정보는 주의 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>인수  
 [ *경로*]  
 Visual FoxPro 검색할 원하는 디렉터리를 지정 합니다. 디렉터리 구분 하려면 쉼표 또는 세미콜론을 사용 합니다.  
  
## <a name="remarks"></a>주의  
 설정 경로 사용 하면 저장된 프로시저 내에서 호출할 수 있는 기타 Visual FoxPro 프로그램에 대 한 검색 경로 지정할 수 있습니다. 경로 설정에 연결에 대해 지정한 데이터 원본의 경로 변경 되지 않습니다.  
  
 설정 경로를 발급 하지 않고 *경로* 기본 디렉터리 또는 폴더 경로 복원 하려면.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 저장된 프로시저에서 설정 경로 실행 하는 경우 다음 함수 및 명령은 무시 됩니다.  
  
-   와 같은 카탈로그 함수 [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) 및 [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) 새 경로 무시 하 고 데이터 원본에 의해 지정 된 경로 참조 하도록 계속 [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) 또는 [ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)합니다.  
  
-   SELECT, INSERT, UPDATE, DELETE 및 CREATE TABLE 등의 명령을 새 경로 무시 하 고 데이터 원본에 의해 지정 된 경로 참조 하도록 계속 **SQLPrepare** 또는 **SQLExecDirect**합니다.  
  
 저장된 프로시저에서 SET PATH를 발급 하 고 원래 상태로 되돌리려면 이후에 경로 설정 하지 않으면 경우에 데이터베이스에 대 한 다른 연결 (데이터 세션 범위로 경로 설정 지정 되지 않은) 이므로 새 경로 사용 합니다.  
  
 만들기, 선택, 또는 데이터 소스에서 지정 된 디렉터리에 있는 테이블을 업데이트 하려는 경우 명령으로는 파일의 전체 경로 지정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC Visual FoxPro 설정 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables(Visual FoxPro ODBC 드라이버)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
