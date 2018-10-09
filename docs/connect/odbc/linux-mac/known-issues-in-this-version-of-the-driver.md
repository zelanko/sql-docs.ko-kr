---
title: SQL Server 용 드라이버의이 버전의 알려진 문제 | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25ebc4837eb37604a45e98112fa5fc24bdb3e69b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743001"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>이 버전의 드라이버에서 알려진 문제

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에서는 Linux 및 macOS에서 Microsoft ODBC Driver 13, 13.1 및 17 for SQL Server를 사용 하 여 알려진된 문제 목록이 포함 되어 있습니다.

추가 문제는 [Microsoft ODBC 드라이버 팀 블로그](http://blogs.msdn.com/b/sqlnativeclient/)에 게시됩니다.  

- Windows, Linux 및 macOS는 PUA(사용자 지정 영역) 또는 EUDC(최종 사용자 정의)의 문자를 다르게 변환합니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 내에서 서버에 수행되는 변환은 Windows 변환 라이브러리를 사용합니다. 드라이버의 변환은 Windows, Linux 또는 macOS 변환 라이브러리를 사용 합니다. 이러한 변환을 수행할 때 각 라이브러리는 다른 결과를 생성할 수 있습니다. 자세한 내용은 [최종 사용자 정의 및 개인 사용자 영역 문자](/windows/desktop/Intl/end-user-defined-characters)를 참조하세요.

- 인코딩이 u t F-8 인 경우 드라이버 관리자를 변환 하지 않습니다 올바르게 항상 u t F-8에서 u t F-16으로. 현재 데이터 손상이 문자열에 하나 이상의 문자가 올바른 utf-8 문자가 없을 때 발생 합니다. ASCII 문자에 대 한 연결이 올바르게 매핑됩니다. ODBC API의 SQLCHAR 버전(예: SQLDriverConnectA)을 호출할 때 드라이버 관리자가 이 변환을 시도합니다. ODBC API의 SQLWCHAR 버전(예: SQLDriverConnectW)을 호출할 때 드라이버 관리자가 이 변환을 시도하지 않습니다.  

- *ColumnSize* 의 매개 변수 **SQLBindParameter** SQL 형식에 있는 문자의 수를 의미 하는 동안 *BufferLength* 응용 프로그램의 바이트 수 버퍼입니다. 그러나 SQL 데이터 형식이 `varchar(n)` 또는 `char(n)`이고, 응용 프로그램이 매개 변수를 SQL_C_CHAR 또는 SQL_C_VARCHAR로 바인딩하고, 클라이언트의 문자 인코딩이 UTF-8인 경우, *ColumnSize*의 값이 서버에서 데이터 형식의 크기와 정렬되는 경우에도 드라이버에서 "문자열 데이터의 오른쪽이 잘렸습니다"라는 오류를 받을 수 있습니다. 이 오류는 문자 인코딩 간 변환에는 데이터의 길이가 변경 될 수 있으므로 발생 합니다. 예를 들어, 오른쪽 아포스트로피 문자 (U + 2019) CP-1252 싱글바이트 0x92, 하지만 u t F-8에서 3 바이트 시퀀스 0xe2로 인코딩된 0x80 0x99 합니다.

예를 들어, 인코딩을 u t F-8 이며 둘 다에 대해 1을 지정 하는 경우 *BufferLength* 하 고 *ColumnSize* 에서 **SQLBindParameter** out 매개 변수 및 다음 시도 앞에 오는 문자가에 저장 된 검색을 `char(1)` 열 (CP-1252를 사용 하 여) 서버의 드라이버 3 바이트 utf-8 인코딩으로 변환 하려고 하지만 1 바이트 버퍼에 결과 맞출 수 없습니다. 비교 하는 반대 방향의 *ColumnSize* 사용 하 여는 *BufferLength* 에서 **SQLBindParameter** 에 서로 다른 코드 페이지 사이 변환을 수행 하기 전에 클라이언트 및 서버입니다. 예를 들어 *ColumnSize* 1은 *BufferLength* 3보다 작기 때문에 드라이버가 오류를 생성합니다. 이 오류를 방지 하려면 되도록 데이터의 길이 지정 된 버퍼 또는 열에 적합 한 변환 후 합니다. 사실은 *ColumnSize* 에 대해 8000 보다 클 수 없습니다는 `varchar(n)` 형식입니다.

## <a name="see-also"></a>참고 항목  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)  

